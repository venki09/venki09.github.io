This is where I will record what I read and take notes for it.

Distributed Log:
* [Reference](https://blog.twitter.com/engineering/en_us/topics/infrastructure/2015/building-distributedlog-twitter-s-high-performance-replicated-log-servic.html)
* Twitter's implementation of a distributed log.
* Twitter has an eventually consistent key-value store, and this log will help with performing updates on the eventually consistent database. 
* Whenever a write happens, it will be written to the log so that we can see them ordered.
* Non-Functional Requirements
  * Scalability
  * Worload isolation - If different workloads are trying to access our log service, it should perform well.
  * Simplicity
* They used Apache BookKeeper for log management.
* Apache Kafka seems to be doing more than just distributed log management so BookKeeper was chosen by them.
* Although bookkeeper has the features that they needed, they had to add somethings on top of it so that it works with their twitter distributed system.
* DistributedLog does things like Abstraction, API, Batch updates etc.