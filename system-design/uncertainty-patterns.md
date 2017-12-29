# Uncertainty patterns

In programming we are often dealing with an uncertainity. We don’t know, we are not sure if something happened or not. Or we are not sure about the result. Especially when it comes to networking/distributed systems but also in other contexts. What I find interesting is that in many cases the techniques used to handle such problems are very similar.

## Retries / At least once delivery
You tried to send something from computer A to computer B. It didn’t work. What do we do? One of the most often technique is to try to do it again. Very simple isn’t it?

We say at least once delivery because computer B can receive our message multiple times in case 1st time already worked but computer A wasn’t sure about it so it sent it again.

## Confirmations / Acknowledges
Sometimes it is enough that we know a message reached point B. But often it is not enough. We also need to know that the message was successfully recognized and processed. When it worked point B sends a confirmation to point A.

Notice that what is just a delivery on a higher level (message reached point B) requires a delivery and confirmation on a lower level (packets consisting the message reached point B and acknowledge of it reached point A back).

## At most once delivery
Sometimes we prefer speed and smaller usage of resources over certainty or reliability. In such case, we always send the message only once. Either it will reach its destination or not. So the strategy is based on lack of retries.

This can be used in many scenarios where the transmitted value is only valid for a very short time anyway and next transmission will include a new version anyway.

A mobile phone sending GPS positions every second. A computer game sending player’s positions constantly. A thermometer sending current temp. In such cases, the logic behind those systems can probably use a previous value as a good enough substitute of the new one, if it wasn’t received. A new value will be sent quickly anyway.

## Timeouts
We need timeouts because we cannot wait indefinitely for a confirmation of a message. If the message was lost or the confirmation of it was lost waiting longer won’t change the situation.

When we reach the timeout we can schedule a retry or just move on depending on the previously discussed strategies.

Of course, timeouts can cause false negatives. Our system reports a timeout which is treated as a failure and one second later we can receive a message saying that everything went OK. But we received it too late. In such case sometimes we don’t need to do anything (retry was already scheduled) but sometimes we might need to compensate. We cancelled an order and now that we received a payment confirmation after a timeout we need to also refund the payment. That is an example of a compensation.

## Idempotence
Idempotence is a way to correctly handle duplicated messages received due to retries and at least once delivery strategy. The idea is that when we receive the same message multiple times it does not cause additional important side-effects and the client is informed that the operation was successful.

The repeated message may cause minor, unimportant side-effects. Maybe it will be logged again, maybe some technical metrics will be increased again but business-wise there is no visible effect.

For example, you can receive an information that a payment was successful. So you trigger a state transition in your app, schedule order delivery, email to customer etc. And 1 second later you receive from payment gateway the same information that the payment was successful. You don’t send to the customer the products twice, you don’t report twice that much revenue for your startup and you don’t send another email. You silently ignore the information, but you respond with information that everything was OK.

Sometimes idempotence can be achieved easily (state machine that can go from state X to X without doing anything), but usually, it requires the effort to detect such situation and handle it properly.

## Exponential backoff
There is often no point in continuing to retry at the same rate i.e. every second. If the situation does not improve, with every retry it is less likely that the system that we try to cooperate with will self-heal. It’s better to back off and keep trying but less and less often. 1 second, 1 minute, 1 hour, 1 day, etc…

Also, some systems randomize retries to avoid a situation where thousands of affected devices try to repeat something at the same time causing a self-denial of service attack. Imagine a networking problem which causes millions of devices running a chat application to disconnect immediately. If they all try to reconnect instantaneously at the same time with the same non-randomized strategy then your servers may not be able to handle it. But when some retry after a second, another group after two seconds, and another after three seconds, then the load on your server might be more tolerable. Especially considering that initiating a connection can often be one of the most expensive operation when systems try to sync their state.

## Commit log / Persistance
RAM is volatile, our application/database processes can die, servers can be turned off. That’s why for really important data before sending it over the wire we first save it into a more safe space. A disc.

That way in the worst case we can have a list of messages that we wanted to send but never had the time to, or were not yet confirmed. If something bad happens, we can re-read the list of messages and send them again.

Almost every messaging system that is supposed to be reliable will send messages to either a disc or replicas running on other machines first before confirming that the message was queued.

## Sequence numbers
When we keep sending messages over the wire we can number them incrementally. One, Two, Three, Four, Five…

When the other part receives them it can spot gaps and out of order messages and request replies or re-order them. It can also confirm multiple messages up to certain number with one reply (i am at 5) instead of confirming each one separately (got 1, got 2, got 3…). Sequence numbers don’t need to be global. They can be defined per connection, session, stream, etc.

## Client side generated UUIDs
Often the content of a message does not uniquely identify it. For example, we may receive an order for 2 iPhones. Many people could order 2 iPhones. So to handle idempotency it might greatly help if every message/request is sent with unique client side generated UUID. If the client repeats the message it will use the same UUID. That makes the recipient’s job of detecting duplicates much easier.

## Correlation numbers
Correlation numbers are a mix of sequence numbers and UUIDs. Say a client sends an order (UUID 321), and later informs about a successful payment (UUID 609 caused by UUID 321) but both messages can get lost.

When the server receives UUID 609 and sees that it is correlated to something with UUID 321 but it has not yet received 321 it knows that it cannot process 609 immediately. It can save that information and wait for retry of 321 and only when it receives it, the server will process 321 and then process 609.

In other words, correlation numbers can help you with retries/duplicates/out-of-order messages which are related to the same business process.

## Reconciliation
Imagine a payment gateway. Your e-commerce system assumes that certain transactions were successful. But that may be an incorrect or incomplete list. If your system was down or had reliability problems it could have dropped some messages about successful payments. If your system was down too long maybe all retries failed and you will never know about this payment (which you probably should refund, or deliver or pay taxes of).

Unless there is a reconciliation process. It means that the payment gateway system exposes API or downloadable file with a list of all transactions. Ideally, as immutable, append-only list of transactions. In such case even long time later you can compare the list of payments in your system, the list in their system and find discrepancies.

## Conflict-free replicated data types
This is a way of keeping and synchronizing data in your system in a special way. Multiple independent nodes can even disconnect completely and when they reconnect later and merge their data together you can be sure that all will reach the same state. I think that if we, as humanity, ever go into stars we will need more of such structures to effectively exchange data after disconnecting and reconnecting between multiple space ships :)

## Time to live (TTL)
Time to live (TTL) or hop limit is a mechanism that limits the lifespan or lifetime of data in a computer or network. TTL may be implemented as a counter or timestamp attached to or embedded in the data. Once the prescribed event count or timespan has elapsed, data is discarded. In computer networking, TTL prevents a data packet from circulating indefinitely. In computing applications, TTL is used to improve performance of caching or to improve privacy.

## Load shedding
Writing to storage is normally the operation that is the bottleneck, especially on remote storage. You can imagine the queue backing up.

Under heavy load you may end up with a queue that gets quite large. The problem with this is that write operations time out to callers, if you had a queue that had 8 seconds of operations in it and a five second timeout the storage writer would constantly be doing work that the result had already been sent for.

Instead each write request is given a time to live (slightly before the timeout). If the TTL is in the future the storage writer will process the write, else it will drop it on the floor and move forward in the queue until it finds one in the future. This prevents it from working on work items that have already been timed out.

This is a form of at-most-once messaging. The difference is it is based on time and not on a buffer being full on insert. Both are forms of load shedding.
