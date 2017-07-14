When you have an infrastucture, you can scale:
- Out: Replicate your infrastructure
- Up: Use less hardware per machine
- Dev Team: For velocity and productivity

## Scale out
When you scale out an infrastructure, you can replicate:
- the storage, that needs to be consistent across data centers
- computing, it's driven by user traffic, can be achieved by the storage

Usually when you replicate something it can be:
* stateless if the state is always outside (cache, database, storage, ecc..).
This can be scale out geographically without any problems.
In front off of each app you can place a load balancer, that can move the traffic in base at some rules (for example round robin)

* Master-Slave replica, this is the case of database, you have one master where you usually write and multiple slave where you can read on.
Usually for failure it is useful to have an odd number of instances, because every time the master became unavailable, the system can elect a new master.

* Master-Master replica, there are multiple masters. This is a complex scenario and when this happens, every write has a timestamp to understand 
what wins at last and every time there is an algorithm to understand on how to solve conflicts

Usually when you scale out an application, a cache is placed between the application and the database because the cache is much faster.
One big problem is to understand when invalid that cache:
- You can invalid at each write on db
- You can invalid on some actions
- etc..

## Scale Up
To scale up an application you can use a profiling system to understand how much cpu/memory use the application.
Based on this data you can understand and choose what to do in you application

## Scale dev team
When multiple engineers works on the same application, you need to grow the application so it can be developed by multiple hands without problems.
To resolve this you can:
1) Create multiple modules
2) Create mutilple services
3) Create different branches when you use a source control

For the point (3) is better to do Continuous Integration and work on the same branch.
