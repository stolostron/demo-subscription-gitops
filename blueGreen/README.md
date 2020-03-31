# Demonstrate Blue-Green deployment of NGINX via Git Ops

## This repo is setup to manage the Blue / Green deployment of nginx
### Activate a subscription (ONLY RUN ONCE)
1. Create a fork the repository and create two branches.
  a. One branch is Blue and one branch is green
  b. Modify `subscription/subscription-nginx-blue.yaml`, changing the value for `apps.open-cluster-management.io/github-branch` to your Blue branch
  c. Modify `subscription/subscription-nginx-green.yaml`, changing the value for `apps.open-cluster-management.io/github-branch` to your Green branch
  d. Modify `subscription/channel.yaml`, changing the value of `spec.pathname` to that of your fork of this repository
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
- Two namespaces are created `demo-gitops` for the channel and `nginx` for the subscriptions
- Three subscriptions are created in project `nginx`
  1. The ingress resource from `master` branch
  2. The blue deployment and service resource from `blue-nginx` branch
  3. The green deployment and service resource from `green-nginx` branch
### How to upgrade green to v1.14.2
- The default configuration:
  - `green` as nginx `v1.12.2`
  - `blue` is nginx `v1.14.2`
- 


