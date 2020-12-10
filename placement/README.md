# Demonstrate placement algorithm
## Tool Requirements
- OpenShift CLI Version >= 4.3.0<br>_Needed for kustomize_
```bash
oc version
```

## This example allows you to demonstrate moving an application from one cluster to another
### CLI: Activate a subscription (ONLY RUN ONCE)
1. Add the subscription to your hub cluster
```
clone https://github.com/open-cluster-management/demo-subscription-gitops.git
oc apply -k demo-subscription-gitops/placement/subscription/
```
### Application Console: Create a new subscription
Check out the development and production topology for for your cluster. Using the console, you can easily create an application that runs one version of the application on your development clusters, and a different version on your production clusters.

#### Prerequisite
More than one cluster, each with a unique label. One cluster represents your development cluster, and the other represents your production cluster.
#### Console
1. Navigate in the menu to `Managed applications`.
2. Choose `Create application`.
3. Enter the following values:
  * **Name:** `nginx`
  * **Namespace:** `nginx`
  * **Repository types** `Git`
  * **URL** `https://github.com/open-cluster-management/demo-subscription-gitops.git`
  * **Branch** `master`
  * **Path** `placement/nginx
  * Select `Deploy application resources only on clusters matching specified labels`
  * Enter the label information for your development cluster
4. Select `Add another repository`
  * **Repository types** `Git`
  * **URL** `https://github.com/open-cluster-management/demo-subscription-gitops.git`
  * **Branch** `production`
  * ** Path** `placement/nginx
  * Select `Deploy application resources only on clusters matching specified labels`
  * Enter the label information for your production cluster
5. Click `Save`

### Viewing
- Navigate to the **Manage applications** in the UI. Click the `nginx-placement` application name.
- View the Topology, look around, by default the application should have deployed to `vendor: OpenShift` clusters.
- Click the `Resources` tab.
- Edit the placement rule, and change `vendor: OpenShift` to `cloud: Amazon` and your application will be migrated to any cluster with the `cloud: Amazon` label. You need to adjust this key and value pair, based on what is seen in your Cluster List page as available labels.
- To spread the app to all clusters, change the YAML as follows:
```yaml
  clusterSelector:
    matchLabels: {}
```
