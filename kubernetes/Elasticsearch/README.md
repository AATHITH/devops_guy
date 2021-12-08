# Elastic Stack Deployment in k8s with operator[Quick Deployment]:

### Install the ElasticSearch Operator:
Install ECK for a first install, run the following commands:

```
kubectl create -f https://download.elastic.co/downloads/eck/1.8.0/crds.yaml
kubectl apply -f https://download.elastic.co/downloads/eck/1.8.0/operator.yaml
```
Check the [Official Download page](https://www.elastic.co/downloads/elastic-cloud-kubernetes) for latest version and instruction.

### Deploy an Elasticsearch cluster

```
cat <<EOF | kubectl apply -f -
apiVersion: elasticsearch.k8s.elastic.co/v1
kind: Elasticsearch
metadata:
  name: quickstart
spec:
  version: 7.15.2
  nodeSets:
  - name: default
    count: 1
    config:
      node.store.allow_mmap: false
EOF
```
You can check all the other configuration like adding a PV with more storage(by default its 1Gi), Hot storage, etc. in [official docs](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-elasticsearch-specification.html).

### Check the installation

`kubectl get elasticsearch`<br>
The Above command will show 

You can see that one Pod is in the process of being started:

`kubectl get pods --selector='elasticsearch.k8s.elastic.co/cluster-name=quickstart'`

Check the service:<br>
`kubectl get service quickstart-es-http`


### Access the ElasticSearch:

#### Get the credentials.

A default user named elastic is automatically created with the password stored in a Kubernetes secret:

PASSWORD=$(`kubectl get secret quickstart-es-elastic-user -o go-template='{{.data.elastic | base64decode}}'`)

#### Request the Elasticsearch endpoint.

From inside the Kubernetes cluster:

`curl -u "elastic:$PASSWORD" -k "https://quickstart-es-http:9200"`

From your local workstation, use the following command in a separate terminal:

`kubectl port-forward service/quickstart-es-http 9200`

Then request localhost:

`curl -u "elastic:$PASSWORD" -k "https://localhost:9200"`


### Reference:
[Quick Start Guide by Elastic Search](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-deploy-elasticsearch.html)<br>
[Elasticsearch on Kubernetes: DIY vs. Elasticsearch Operator](https://cloud.netapp.com/blog/cvo-blg-elasticsearch-on-kubernetes-diy-vs.-elasticsearch-operator)<br>
[Elasticsearch deployment with operator | Youtube](https://www.youtube.com/watch?v=Wf6E3vkvEFM)<br>