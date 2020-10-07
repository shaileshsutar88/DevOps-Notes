#### K8s Notes as taught by Mumshad

## ETCD Server.
etcd is distributed reliable key-value store that is simple, secure & fast. It stores information such as the nodes, pods, configs, secretes
accounts, roles, bindings and others. Every information we see from kubectl command comes from etcd server.
ETCDCTL is the CLI tool used to interact with ETCD. ETCDCTL can interact with ETCD Server using 2 API versions - Version 2 and Version 3.  By default its set to use Version 2. Each version has different sets of commands.

## Kube-API Server.
It is a primary management component in K8s. The kube-apiserver is at the center of all the different tasks that needs to be performed to make a
change in the cluster. The kube-api server is responsible for Authenticating and validating requests, retrieving and updating data in ETCD data store. In fact, kube-api server is the only component that interacts directly with the etcd datastore.

## Kube controller manager
There are several sub controllers in Kube controller manager.

1. Node controller
   The node controller checks the status of the nodes every 5 seconds. That way the node controller can monitor the health of the nodes if it stops receiving heartbeat from a node the node is marked as unreachable but it waits for 40 seconds before marking it unreachable after a node is marked unreachable it gives it five minutes to come back up if it doesn’t, it removes the PODs assigned to that node and provisions them on the healthy ones.

2. Replication controller
   If the PODs are part of a replica set the next controller is the replication controller. It is responsible for monitoring the status of replica sets and ensuring that the desired number of PODs are available at all times within the set.


## Kube scheduler
The scheduler is only responsible for deciding which pod goes on which node. It doesn’t actually place the pod on the nodes. the scheduler decides which nodes the pods are placed on depending on certain criteria. You may have PODs with different resource requirements, You can have nodes in the cluster dedicated to certain applications.

## Kubelet
Kubelet is respsonsible for loading and unloading of the containers on worker node as instructed by scheduler on master. It also monitors
the state of pod and containers in it and reports it to kube-api server on timely basis.

## Kube Proxy
The Kube-proxy is an implementation of a network proxy and a load balancer, and it supports the service abstraction along with other networking operation. It is responsible for routing traffic to the appropriate container based on IP and port number of the incoming request.
