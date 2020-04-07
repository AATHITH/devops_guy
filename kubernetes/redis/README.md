# Create a Stateful Redis with statefulset:

#### Step 1: create the config for redis.conf
```
kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/redis/redis.conf
```
#### Step 2: create the Persistent Volume Claim
```
kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/redis/pvc.yaml
```
#### Step 3: create the Statefulset
```
kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/redis/statefulset.yaml
```
#### Step 4: create the service to access the redis pod
```
kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/redis/service.yaml
```
#### Step 5: access the redis-cli
Access the redis-cli with the following command
`kubectl exec -it redis-0 -- redis-cli`
