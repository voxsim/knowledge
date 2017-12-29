## Index of system design topics

> Summaries of various system design topics, including pros and cons.  **Everything is a trade-off**.
>
> Each section contains links to more in-depth resources.

<p align="center">
  <img src="http://i.imgur.com/jrUBAF7.png">
  <br/>
</p>

* [How to approach a system design interview question](https://github.com/voxsim/knowledge/blob/master/system-design/interview.md)
* [Performance vs scalability](#performance-vs-scalability)
* [Scaling](https://github.com/voxsim/knowledge/blob/master/system-design/scaling.md)
* [Latency vs throughput](#latency-vs-throughput)
* [CAP theorem](https://github.com/voxsim/knowledge/blob/master/system-design/cap.md)
* [Consistency patterns](https://github.com/voxsim/knowledge/blob/master/system-design/consistency-patterns.md)
* [Availability patterns](https://github.com/voxsim/knowledge/blob/master/system-design/availability-patterns.md)
* [Domain name system](https://github.com/voxsim/knowledge/blob/master/system-design/dns.md)
* [Content delivery network](https://github.com/voxsim/knowledge/blob/master/system-design/cdn.md)
* [Load balancer](https://github.com/voxsim/knowledge/blob/master/system-design/load-balancer.md)
* [Reverse proxy (web server)](https://github.com/voxsim/knowledge/blob/master/system-design/reverse-proxy.md)
* [Application layer](https://github.com/voxsim/knowledge/blob/master/system-design/application-layer.md)
* [Database](https://github.com/voxsim/knowledge/blob/master/system-design/database.md)
* [Cache](https://github.com/voxsim/knowledge/blob/master/system-design/cache.md)
* [Asynchronism](https://github.com/voxsim/knowledge/blob/master/system-design/asynchronism.md)
* [Networking](https://github.com/voxsim/knowledge/blob/master/system-design/networking.md)
* [Security](#security)
* [Appendix](#appendix)
    * [Powers of two table](#powers-of-two-table)
    * [Latency numbers every programmer should know](#latency-numbers-every-programmer-should-know)
    * [Additional system design interview questions](#additional-system-design-interview-questions)
    * [Real world architectures](#real-world-architectures)
    * [Company architectures](#company-architectures)
    * [Company engineering blogs](#company-engineering-blogs)
* [Under development](#under-development)
* [Credits](#credits)
* [Contact info](#contact-info)
* [License](#license)

Keep in mind that **everything is a trade-off**.

Then we'll dive into more specific topics such as DNS, CDNs, and load balancers.

## Performance vs scalability

A service is **scalable** if it results in increased **performance** in a manner proportional to resources added. Generally, increasing performance means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow.<sup><a href=http://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html>1</a></sup>

Another way to look at performance vs scalability:

* If you have a **performance** problem, your system is slow for a single user.
* If you have a **scalability** problem, your system is fast for a single user but slow under heavy load.

## Latency vs throughput

**Latency** is the time to perform some action or to produce some result.

**Throughput** is the number of such actions or results per unit of time.

Generally, you should aim for **maximal throughput** with **acceptable latency**.

## Security

Security is a broad topic.  Unless you have considerable experience, a security background, or are applying for a position that requires knowledge of security, you probably won't need to know more than the basics:

* Encrypt in transit and at rest.
* Sanitize all user inputs or any input parameters exposed to user to prevent [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) and [SQL injection](https://en.wikipedia.org/wiki/SQL_injection).
* Use parameterized queries to prevent SQL injection.
* Use the principle of [least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## Appendix

You'll sometimes be asked to do 'back-of-the-envelope' estimates.  For example, you might need to determine how long it will take to generate 100 image thumbnails from disk or how much memory a data structure will take.  The **Powers of two table** and **Latency numbers every programmer should know** are handy references.

### Powers of two table

```
Power           Exact Value         Approx Value        Bytes
---------------------------------------------------------------
7                             128
8                             256
10                           1024   1 thousand           1 KB
16                         65,536                       64 KB
20                      1,048,576   1 million            1 MB
30                  1,073,741,824   1 billion            1 GB
32                  4,294,967,296                        4 GB
40              1,099,511,627,776   1 trillion           1 TB
```

#### Source(s) and further reading

* [Powers of two](https://en.wikipedia.org/wiki/Power_of_two)

### Latency numbers every programmer should know

```
Latency Comparison Numbers
--------------------------
L1 cache reference                           0.5 ns
Branch mispredict                            5   ns
L2 cache reference                           7   ns                      14x L1 cache
Mutex lock/unlock                          100   ns
Main memory reference                      100   ns                      20x L2 cache, 200x L1 cache
Compress 1K bytes with Zippy            10,000   ns       10 us
Send 1 KB bytes over 1 Gbps network     10,000   ns       10 us
Read 4 KB randomly from SSD*           150,000   ns      150 us          ~1GB/sec SSD
Read 1 MB sequentially from memory     250,000   ns      250 us
Round trip within same datacenter      500,000   ns      500 us
Read 1 MB sequentially from SSD*     1,000,000   ns    1,000 us    1 ms  ~1GB/sec SSD, 4X memory
Disk seek                           10,000,000   ns   10,000 us   10 ms  20x datacenter roundtrip
Read 1 MB sequentially from 1 Gbps  10,000,000   ns   10,000 us   10 ms  40x memory, 10X SSD
Read 1 MB sequentially from disk    30,000,000   ns   30,000 us   30 ms 120x memory, 30X SSD
Send packet CA->Netherlands->CA    150,000,000   ns  150,000 us  150 ms

Notes
-----
1 ns = 10^-9 seconds
1 us = 10^-6 seconds = 1,000 ns
1 ms = 10^-3 seconds = 1,000 us = 1,000,000 ns
```

Handy metrics based on numbers above:

* Read sequentially from disk at 30 MB/s
* Read sequentially from 1 Gbps Ethernet at 100 MB/s
* Read sequentially from SSD at 1 GB/s
* Read sequentially from main memory at 4 GB/s
* 6-7 world-wide round trips per second
* 2,000 round trips per second within a data center

#### Latency numbers visualized

![](https://camo.githubusercontent.com/77f72259e1eb58596b564d1ad823af1853bc60a3/687474703a2f2f692e696d6775722e636f6d2f6b307431652e706e67)

**Don't focus on nitty gritty details for the following articles, instead:**

* Identify shared principles, common technologies, and patterns within these articles
* Study what problems are solved by each component, where it works, where it doesn't
* Review the lessons learned


## Transactions across data centers
|            |Backups|Master/Slave|Multi Master|2PC   |Paxos |
|------------|-------|------------|------------|------|------|
|Consistency |Weak	 |Eventual	  |Eventual    |Strong|Strong|
|Transactions|No	   |Full	      |Local 	     |Full  |Full  |
|Latency	   |Low	   |Low         |Low         |High  |High  |
|Throughput	 |High	 |High        |High        |Low	  |Medium|
|Data loss	 |Lots	 |Some	      |Some        |None  |None  |
|Failover	   |Down	 |Read only	  |Read/write  |Read/write|Read/write|

For more info: https://snarfed.org/transactions_across_datacenters_io.html

## Lesson learned
You must change your mentality to build really scalable systems. Approach chaos in a probabilistic sense that things will work well. In traditional systems we present a perfect world where nothing goes down and then we build complex algorithms (agreement technologies) on this perfect world. Instead, take it for granted stuff fails, that's
reality, embrace it. For example, go more with a fast reboot and fast recover approach. With a decent spread of data and services you might get close to 100%. Create self-healing, self-organizing lights out operations.

Create a shared nothing infrastructure. Infrastructure can become a shared resource for development and deployment with the same downsides as shared resources in your logic and data tiers. It can cause locking and blocking and dead lock. A service oriented architecture allows the creation of a parallel and isolated development process that scales feature development to match your growth.

Open up you system with APIs and you'll create an ecosystem around your application.

Only way to manage as large distributed system is to keep things as simple as possible. Keep things simple by making sure there are no hidden requirements and hidden dependencies in the design. Cut technology to the minimum you need to solve the problem you have. It doesn't help the company to create artificial and unneeded layers of complexity.

Organizing around services gives agility. You can do things in parallel is because the output is a service. This allows fast time to market. Create an infrastructure that allows services to be built very fast. 

There's bound to be problems with anything that produces hype before real implementation

Use SLAs internally to manage services.

Anyone can very quickly add web services to their product. Just implement one part of your product as a service and start using it.

Build your own infrastructure for performance, reliability, and cost control reasons. By building it yourself you never have to say you went down because it was company X's fault. Your software may not be more reliable than others, but you can fix, debug, and deployment much quicker than when working with a 3rd party.

Use measurement and objective debate to separate the good from the bad. I've been to several presentations by ex-Amazoners and this is the aspect of Amazon that strikes me as uniquely different and interesting from other companies. Their deep seated ethic is to expose real customers to a choice and see which one works best and to make decisions based on those tests.

Avinash Kaushik calls this getting rid of the influence of the HiPPO's, the highest paid people in the room. This is done with techniques like A/B testing and Web Analytics. If you have a question about what you should do code it up, let people use it, and see which alternative gives you the results you want.

Create a frugal culture. Amazon used doors for desks, for example.

Know what you need. Amazon has a bad experience with an early recommender system that didn't work out: "This wasn't what Amazon needed. Book recommendations at Amazon needed to work from sparse data, just a few ratings or purchases. It needed to be fast. The system needed to scale to massive numbers of customers and a huge catalog. And it needed to enhance discovery, surfacing books from deep in the catalog that readers wouldn't find on their own."

People's side projects, the one's they follow because they are interested, are often ones where you get the most value and innovation. Never underestimate the power of wandering where you are most interested.

Involve everyone in making dog food. Go out into the warehouse and pack books during the Christmas rush. That's teamwork.

Create a staging site where you can run thorough tests before releasing into the wild. 

A robust, clustered, replicated, distributed file system is perfect for read-only data used by the web servers.

Have a way to rollback if an update doesn't work. Write the tools if necessary.

Switch to a deep services-based architecture (http://webservices.sys-con.com/read/262024.htm).

Look for three things in interviews: enthusiasm, creativity, competence. The single biggest predictor of success at Amazon.com was enthusiasm.

Hire a Bob. Someone who knows their stuff, has incredible debugging skills and system knowledge, and most importantly, has the stones to tackle the worst high pressure problems imaginable by just leaping in.

Innovation can only come from the bottom. Those closest to the problem are in the best position to solve it. any organization that depends on innovation must embrace chaos. Loyalty and obedience are not your tools. 

Creativity must flow from everywhere.

Everyone must be able to experiment, learn, and iterate. Position, obedience, and tradition should hold no power. For innovation to flourish, measurement must rule.

Embrace innovation. In front of the whole company, Jeff Bezos would give an old Nike shoe as "Just do it" award to those who innovated.

Don't pay for performance. Give good perks and high pay, but keep it flat. Recognize exceptional work in other ways. Merit pay sounds good but is almost impossible to do fairly in large organizations. Use non-monetary awards, like an old shoe. It's a way of saying thank you, somebody cared.

Get big fast. The big guys like Barnes and Nobel are on your tail. Amazon wasn't even the first, second, or even third book store on the web, but their vision and drive won out in the end.

In the data center, only 30 percent of the staff time spent on infrastructure issues related to value creation, with the remaining 70 percent devoted to dealing with the "heavy lifting" of hardware procurement, software management, load balancing, maintenance, scalability challenges and so on.

Prohibit direct database access by clients. This means you can make you service scale and be more reliable without involving your clients. This is much like Google's ability to independently distribute improvements in their stack to the benefit of all applications.

Create a single unified service-access mechanism. This allows for the easy aggregation of services, decentralized request routing, distributed request tracking, and other advanced infrastructure techniques.

Making Amazon.com available through a Web services interface to any developer in the world free of charge has also been a major success because it has driven so much innovation that they couldn't have thought of or built on their own.

Developers themselves know best which tools make them most productive and which tools are right for the job.

Don't impose too many constraints on engineers. Provide incentives for some things, such as integration with the monitoring system and other infrastructure tools. But for the rest, allow teams to function as independently as possible. 

Developers are like artists; they produce their best work if they have the freedom to do so, but they need good tools. Have many support tools that are of a self-help nature. Support an environment around the service development that never gets in the way of the development itself.

You build it, you run it. This brings developers into contact with the day-to-day operation of their software. It also brings them into day-to-day contact with the customer. This customer feedback loop is essential for improving the quality of the service.

Developers should spend some time with customer service every two years. Their they'll actually listen to customer service calls, answer customer service e-mails, and really understand the impact of the kinds of things they do as technologists.

Use a "voice of the customer," which is a realistic story from a customer about some specific part of your site's experience. This helps managers and engineers connect with the fact that we build these technologies for real people. Customer service statistics are an early indicator if you are doing something wrong, or what the real pain points are for your customers.

Infrastructure for Amazon, like for Google, is a huge competitive advantage. They can build very complex applications out of primitive services that are by themselves relatively simple. They can scale their operation independently, maintain unparalleled system availability, and introduce new services quickly without the need for massive reconfiguration.
