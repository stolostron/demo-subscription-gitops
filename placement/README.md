# Demonstrate placement algorithm
## Tool Requirements
- OpenShift CLI Version >= 4.3.0<br>_Needed for kustomize_
```bash
oc version
```

## This example, allows you to demonstrate moving an application from one cluster to another
### Activate a subscription (ONLY RUN ONCE)
1. Add the subscription to your Red Hat Advanced Cluster Management for Kubernetes HUB
```
oc apply -k subscription/
```
### Using
- Navigate to the Manage applications in the UI. Click the `nginx-placement` Application name.
- View the Topology, look around, by default the application should have deployed to `cloud: Amazon` clusters
- Click the `Resources` tab
- 
- Edit the placement rule, and change `cloud: Google` to `cloud: Amazon` and your application will be migrated. You need to adjust this key and value pair, based on what is seen in your Cluster List page as available labels
