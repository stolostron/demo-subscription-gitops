# Demonstrate Blue-Green deployment of NGINX via Git Ops

## This repo is setup to manage the Blue / Green deployment of nginx
### Activate a subscription (ONLY RUN ONCE)
1. Create a fork the repository and create two branches.
  a. One branch is Blue and one branch is green
  b. Modify `blueGreen/subscription/subscription-nginx-blue.yaml`, changing the value for `apps.open-cluster-management.io/github-branch` to your Blue branch
  c. Modify `blueGreen/subscription/subscription-nginx-green.yaml`, changing the value for `apps.open-cluster-management.io/github-branch` to your Green branch
  d. Modify `blueGreen/subscription/channel.yaml`, changing the value of `spec.pathname` to that of your fork of this repository
2. Create the file `blueGreen/subscriptions/secret.yaml`
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
- After you have completed the ONE time setup, you will start to see the BMA Objects from the `./bma/BareMetalAssets` folder start appearing in the Bare Metal Asset UI.
- If you commit a change to your branch or forked repo, those changes will appear in the Bare Metal Asset UI in <60s
- The namespace used for the Bare Metal Asset Objects is `default`

### Help
Reach out to `jpacker@redhat.com` or Slack `@jpacker` in coreos.slack.com for help
