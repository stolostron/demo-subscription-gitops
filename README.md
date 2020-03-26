# Demonstrate BareMetalAssets via Git Ops

## This repo is setup to manage your Bare Metal Assets as code
### Setup (ONLY ONCE)
### Activate a subscription
1. Create a branch in the repository or fork the repository.
  - If you branched, update `./subscription/subscription.yaml` and set `spec.branch: master` to your branch name.
  - If you forked the repo, update `./subscription/channel.yaml` and set `spec.pathname` to your forked git repository url
2. Edit the `./subscriptions/secret.yaml` file
  - Base64 encode your git username, and put the result in `data.user: `
  - Base64 encode your git access token, and put the result in `data.accessToken: `
3. Add the subscription to your Red Hat Advanced Cluster Management for Kubernetes HUB
```
oc apply -k subscription/
```
### Using
- After you have completed the ONE time setup, you will start to see the BMA Objects from the `./BareMetalAssets` folder start appearing in the Bare Metal Asset UI.
- If you commit a change to your branch or forked repo, those changes will appear in the Bare Metal Asset UI in <60s
- The namespace used for the Bare Metal Asset Objects is `default`

### Help
Reach out to `jpacker@redhat.com` or Slack `@jpacker` in coreos.slack.com for help
