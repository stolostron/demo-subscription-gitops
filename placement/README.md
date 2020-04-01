# Demonstrate placement algorithm

## This example, allows you to demonstrate moving an application from one cluster to another
### Activate a subscription (ONLY RUN ONCE)
1. Create the file `subscriptions/secret.yaml`
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
- Navigate to the Application Management UI
- Edit the placement rule, and change `cloud: Amazon` to `cloud: Google`
