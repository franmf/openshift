## How to replace a master Machine by a new master MachineSet

1. Create a new master MachineSet based on this template:
   * https://github.com/secobau/openshift/blob/master/install/machineSet.yaml
1. Delete the master Machine you want to replace.
1. Monitor the pods for all projects until the cluster is stable.
Only etcd-quorum-guard Pod should remain in a pending state. 
It is also normal that etcd ClusterOperator is in a degraded state with one member down.
1. Connect to any openshift-etcd Pod and run the following commands to identify the deleted master Node and remove it from the list:
   
   ```
   etcdctl member list
   etcdctl member remove <ID>   
   ```
1. Edit the Machine Count for the new master MachineSet from 0 to 1.
1. Monitor the pods for all projects until the cluster is stable.
1. Repeat the process with the next master Machine you want to substitute.