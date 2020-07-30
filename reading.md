This is where I will record what I read and take notes for it.

## Distributed Log
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

## Java parallelism - In progress
* https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html
* http://cr.openjdk.java.net/~rpressler/loom/loom/sol1_part1.html

## Kubernetes Authentication
* I have been working with kubernetes for a while now and I wanted to understand how their authentication scheme works. 
* K8s API server is the one responsible for orchestrating the whole cluster using its API ofcourse. Each node will have a process called kubelet which will enable them to communicate with the other pods.
* When a human user accesses the k8s cluster, its user credentials are not directly managed by k8s. An external identity provider and authenticator can manage that access which will be trusted by k8s. Example: Github. As long as the user presents a valid certificate which is recognized by the k8s certificate authority, we will be authenticated.
* But when a process inside k8s wants to access the API, like for ex: A pod, this will be authenticated by the k8s API server. Each resource will be assigned a system account and their credentials are stored inside the pod so that they can use it to authenticate with the API server.
* K8s has many authn schemes such as bearer token, http bases authn, authn proxy etc. 
* You can also integrate external authn protocol like LDAP, SAML using the authn proxy.
