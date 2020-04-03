# Demonstrate Blue-Green deployment of NGINX via Git Ops
## Tool Requirements
- OpenShift CLI Version >= 4.3.0<br>_Needed for kustomize_
```bash
oc version
```

## This repo is setup to manage the Blue / Green deployment of nginx
### Activate a subscription (ONLY RUN ONCE)
1. Create a fork the repository and create two branches.
  a. Create two branches, `blue-nginx` and `green-nginx`
  b. Modify `subscription/channel.yaml`, changing the value of `spec.pathname` to that of your fork of this repository
2. Create the file `subscriptions/secret.yaml`
```yaml
---
apiVersion: v1
kind: Secret
metadata:
  name: my-github-secret
  namespace: baremetal-assets
data:
  user: BASE64_ENCRYPTED_USERNAME
  accessToken: BASE64_ENCRYPTED_PASSWORD
```
  - Base64 encode your git username, and replace `BASE64_ENCRYPED_USERNAME`
  - Base64 encode your git access token, and replace `BASE64_ENCRYPTED_PASSWORD`
3. Add the subscription to your Red Hat Advanced Cluster Management for Kubernetes HUB
```
oc apply -k subscription/
```
### How it works
- Three namespaces are created on the hub: `demo` for the channel and `nginx-blue` and `nginx-green` for the subscriptions
- Four subscriptions are created
  1. The ingress & service resources from `master` branch, in `nginx-blue` and `nginx-green`
  2. The blue deployment from `blue-nginx` branch
  3. The green deployment from `green-nginx` branch
### How to upgrade green to v1.14.2
- The default configuration:
  - `blue` is nginx `v1.12.2`
  - `green` is nginx `v1.12.2`
- Modify the `blueGreen/nginx/deployment/deployment.yaml` to 1.14.2 in the `blue-nginx` branch
- Commit the change a push it to the remote repo
_*Note:* That you can apply Git branch controls, where approvals(reviews) are required and not even admin's can merge without approval.
- This will cause the nginx pods in the `nginx-blue` namespace to be updated to 1.14.2
- Now make a pull request from `nginx-blue` to `nginx-green` this merges the version changes from Blue to Green.  You can apply branch control to require a review and use a CI system to validate the deployment YAML and image tag.
- Once you `merge` the pull request, the pods in the `nginx-green` namespace will upgrade to 1.14.2
- A ReplicaSet is used to guarantee zero downtime during updates. If you watch the pods in the deployment, you will see that new pods go into the Running state, before the original pods are Terminated.


