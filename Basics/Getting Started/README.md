# Getting Started with Argo CD

<h2>1. Install Argo CD</h2>
This will create a new namespace, argocd, where Argo CD services and application resources will live.

`$ kubectl create namespace argocd`<br>

`$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
<br> 

If you are not interested in UI, SSO, multi-cluster features then you can install core Argo CD components only:
kubectl create namespace argocd.<br>

`$ kubectl create namespace argocd`
`$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml`

<br>
<h2>2. Download Argo CD CLI</h2>
By default, the Argo CD API server is not exposed with an external IP. To access the API server, choose one of the following techniques to expose the Argo CD API server:

`$ brew install argocd`

<br>
<h2>3. Access the Argo CD API Server</h2>
By default, the Argo CD API server is not exposed with an external IP. To access the API server, choose one of the following techniques to expose the Argo CD API server:

<br>
<h3><u>Service Type Load Balancer</u></h3>
Change the argocd-server service type to LoadBalancer:

`$ kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'`

<br>
<h3><u>Port Forwarding</u></h3>

Kubectl port-forwarding can also be used to connect to the API server without exposing the service.


`$ kubectl port-forward svc/argocd-server -n argocd 8080:443`
<br>
The API server can then be accessed using https://localhost:8080

<br>
<h2>4. Login Using The CLI</h2>
The initial password for the admin account is auto-generated and stored as clear text in the field password in a secret named argocd-initial-admin-secret in your Argo CD installation namespace. You can simply retrieve this password using the argocd CLI:
<br>

`$ argocd admin initial-password -n argocd`

<br>
Using the username admin and the password from above, login to Argo CD's IP or hostname:


`$ argocd login <ARGOCD_SERVER>`

<br>
Change the password using the command:


`$ argocd account update-password`

<br>
<h2>5. Register a Cluster To Deploy Apps To</h2>

First list all clusters contexts in your current kubeconfig: <br>
`$ kubectl config get-contexts -o name`

<br>
Choose a context name from the list and supply it to argocd cluster add CONTEXTNAME. For example, for docker-desktop context, run:


`$ argocd cluster add docker-desktop`

<br>
<h2>6. Create an Application from a Git Repository</h2>
First we need to set the current namespace to argocd running the following command:<br>

`$ kubectl config set-context --current --namespace=argocd`

<br>
Create the example guestbook application with the following command:
<br>

`$ argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default`

<br>
<h2>7. Sync (Deploy) The Application</h2>
Once the guestbook application is created, you can now view its status:

`$ argocd app get guestbook`

The application status is initially in OutOfSync state since the application has yet to be deployed, and no Kubernetes resources have been created. To sync (deploy) the application, run:


argocd app sync guestbook
This command retrieves the manifests from the repository and performs a kubectl apply of the manifests. The guestbook app is now running and you can now view its resource components, logs, events, and assessed health status.