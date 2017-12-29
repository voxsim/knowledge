# Consistency patterns

With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data.  Recall the definition of consistency from the [CAP theorem](#cap-theorem) - Every read receives the most recent write or an error.

## Types of consistency

### Weak consistency

After a write, reads may or may not see it.  A best effort approach is taken.

This approach is seen in systems such as memcached.  Weak consistency works well in real time use cases such as VoIP, video chat, and realtime multiplayer games.  For example, if you are on a phone call and lose reception for a few seconds, when you regain connection you do not hear what was spoken during connection loss.

### Eventual consistency

After a write, reads will eventually see it (typically within milliseconds).  Data is replicated asynchronously.

This approach is seen in systems such as DNS and email.  Eventual consistency works well in highly available systems.

### Strong consistency

After a write, reads will see it.  Data is replicated synchronously.

This approach is seen in file systems and RDBMSes.  Strong consistency works well in systems that need transactions.

## Why we force consistency transactions?
* Correctness
* Enforce invariants
* ACID

## Why we force concistency across datacenters?
* Catastrophic failures
* Expected failures
* Routine maintenance
* Geolocality
* CDNs, edge caching

## Multihoming
Multihoming is the practice of connecting a host or a computer network to more than one network/source of data. This can be done in order to increase reliability or performance, or to reduce cost. Multihoming is an hard problem and it's even harder if we think to do consistently and with real time writes.

### Option 1: Don't do it
* ...instead, bunkerize.
  * Most common
  * Microsoft Azure (tables)
  * Amazon SimpleDB
* Bad at catastrophic failure
  * Large scale data loss
  * Example: SVColo
* Not great for serving
  * No geolocation

### Option 2: Primary with hot failover(s)
Better, but not ideal
* Mediocre at catastrophic failure
* Window of lost data
* Failover data may be inconsistent
* Geolocated for reads, not for writes

### Option 3: True multihoming
* Simultaneous writes in different DCs
* Two way: hard
* N way: harder
* Handle catastrophic failure, geolocality
* ...but pay for it in latency

## Transactions across data centers		
|            |Backups|Master/Slave|Multi Master|2PC   |Paxos |		
|------------|-------|------------|------------|------|------|		
|Consistency |Weak	 |Eventual	  |Eventual    |Strong|Strong|		
|Transactions|No	   |Full	      |Local 	     |Full  |Full  |		
|Latency	   |Low	   |Low         |Low         |High  |High  |		
|Throughput	 |High	 |High        |High        |Low	  |Medium|		
|Data loss	 |Lots	 |Some	      |Some        |None  |None  |		
|Failover	   |Down	 |Read only	  |Read/write  |Read/write|Read/write|
