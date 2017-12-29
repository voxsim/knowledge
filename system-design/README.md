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
* [Uncertainty patterns](https://github.com/voxsim/knowledge/blob/master/system-design/uncertainty-patterns.md)
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
* [Back of the envelope](https://github.com/voxsim/knowledge/blob/master/system-design/back-of-the-envelope.md)

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
