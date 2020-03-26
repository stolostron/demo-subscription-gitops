# Demonstrate BareMetalAssets via Git Ops

## This repo is setup to manage your Bare Metal Assets as code
### Getting started
1. Create a subscription once to this repo, then all changes will be `Continously Delivered` to your cluster
  - `oc apply -f ./subscription`
2. Make changes in the `./BareMetalAssets`, any changes when committed to `master` will be automatically applied to your cluster (namespace `default`)

