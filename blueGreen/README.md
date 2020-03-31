# Demonstrate Blue-Green deployment of NGINX via Git Ops

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
### Using
- Two namespaces are created: `demo-gitops` for the channel and `nginx` for the subscriptions
- Three subscriptions are created in project `nginx`
  1. The ingress resource from `master` branch, also includes the blue/green services
  2. The blue deployment from `blue-nginx` branch
  3. The green deployment from `green-nginx` branch
### How to upgrade green to v1.14.2
- The default configuration:
  - `green` as nginx `v1.12.2`
  - `blue` is nginx `v1.14.2`
- Modify the `blueGreen/nginx/green/deployment.yaml` to 1.14.2 (or any version you want)
- Commit the change a push
_*Note:* That you can apply Git branch controls, where approvals(reviews) are required and not even admin's can merge without approval.
- The green nginx is updated without an outage, via a replica set


