# How to add Kubernetes Dashboard to your cluster:

#### Step 1: Deploy the Kubernetes Dashboard
The Dashboard UI is not deployed by default. To deploy it, run the following command.

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta5/aio/deploy/recommended.yaml

#### Step 2: Create users to access the Dashboard
Create a new user using Service Account mechanism of Kubernetes.

    kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/dashboard/sa.yaml

#### Step 3: Create a Role
Create a role with admin privileges.
> **Warning:** The sample role in here have admin privileges and it is for educational purposes only.

    kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/dashboard/cluster-role.yaml

#### Step 4: Create a Role-Binding
Create a Role-binding to bind the service account and roles created above.

    kubectl create -f https://raw.githubusercontent.com/AATHITH/blog/master/kubernetes/dashboard/role-binding.yaml
#### Step 5: Get the bearer token

    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
This will print:
```
Name:         admin-user-token-v57nw
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 0303243c-4040-4a58-8a47-849ee9ba79c1

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1066 bytes
namespace:  20 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLXY1N253Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIwMzAzMjQzYy00MDQwLTRhNTgtOGE0Ny04NDllZTliYTc5YzEiLCJzdWIiOiJzeXN0ZW06c2Vydmls6

```
#### Step 6: Exposing the Dashboard
You can access Dashboard using two methods:
1) Kubectl command-line tool:
```
kubectl proxy
```
view your dashboard [here.](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login)

> **Warning:** The UI can  _only_  be accessed from the machine where the command is executed.

2) Kubernetes service NodePort:
   
```
   mkdir $HOME/certscd
   $HOME/certs
   openssl genrsa -out dashboard.key 2048openssl rsa -in dashboard.key -out dashboard.key
   openssl req -sha256 -new -key dashboard.key -out dashboard.csr -subj '/CN=localhost'
   openssl x509 -req -sha256 -days 365 -in dashboard.csr -signkey dashboard.key -out dashboard.crt
   kubectl delete secret kubernetes-dashboard-certs -n kubernetes-dashboard
   kubectl create secret generic kubernetes-dashboard-certs --**from**-file=dashboard.key --**from**-file=dashboard.crt -n kubernetes-dashboard
```
**If you get an error like:**  
Can’t load /root/.rnd into RNG  
140212358259136:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:88:Filename=/root/.rnd
solve this by commenting`# RANDFILE               = $ENV::HOME/.rnd` in `vi /etc/ssl/openssl.cnf`

Change the service type to NodePort
```
kubectl edit service kubernetes-dashboard -n kubernetes-dashboard
...
type: ClusterIp --> type: NodePort
...
```

#### Step 7: Get Bearer Token

    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

Now copy the token and paste it into  `Enter token`  field on [login screen.](https://ip:nodeport/#/login)

![login](/kubernetes/dashboard/login.PNG)

Thats it. You have now successfully created a Dashboard for your Kubernetes cluster with a Bearer token.
![ui-dashboard.png](/kubernetes/dashboard/ui-dashboard.png)

#### Reference links:
[https://medium.com/@sondnpt00343/deploying-a-publicly-accessible-kubernetes-dashboard-v2-0-0-betax-8e39680d4067](https://medium.com/@sondnpt00343/deploying-a-publicly-accessible-kubernetes-dashboard-v2-0-0-betax-8e39680d4067)
[https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
[https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)
