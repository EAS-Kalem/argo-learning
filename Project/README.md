# Practice Project
<h4></h4>
<br>
<h2>Problem Statement</h2>
An organisation needs on demand CICD infrastructure and does not have the time/funds to up skill its own staff to create it themselves. Our solution is too create a helm chart for this organisation that they can use to spin up the needed architecture on demand. This architecture should include, a pipeline orchestrator, push detection, static code analysis, image analysis, secret storage, artefact storage,  and is deployed in kubernetes. Use ArgoCD
<br><br>
<h2>Solution</h2>

![Alt text](image.png)<br>
<h2>Steps</h2>
1. Download kubernetes <br>
2. Download tools (kubectl) <br>
3. Create a Namespace, application, CI/CD, argo, hashicorp using kubectl <br>
4. Create kubernetes cluster <br>
5. Pod definition file for each of the machines needed (Tekton, Buildah, Trivy, ArgoCd, SonarQube, Hashicorp Vault, Nexus Repository) <br>
6. Install argo CD <br>
7. Download ArgoCD CLI <br>
8. Change the argocd-server service type to LoadBalancer <br>
9. Login Using The CLI <br>
10. Go to https://artifacthub.io/packages/helm/hashicorp/vault and get a chart for vault, mssql and nexus
11. Register A Cluster To Deploy Apps <br>
12. Create your GO Application in A Git Repository <br>
13. Sync/Deploy The Application <br>

