# OPA Gatekeeper with ACM
## Running in less the 30s
1. In ACM navigate to the applications page, and click: `Create application`
2. Enter name: `opa-gatekeeper`
3. Enter namespace: `gatekeeper-system`, it is important to use this exact value!!
4. Choose the Repository type `Git`
5. Enter or select the Git URL: `https://github.com/open-cluster-management/demo-subscription-gitops.git`
6. Enter or select branch: `gatekeeper`
7. Enter repository path: `opa/gatekeeper`
8. Choose a label key and value to match your target clusters
9. Click `Save` to deploy gatekeeper
10. Run:
```
oc apply -f ./opa/policy/policy-gatekeeper.yaml
```
That's it. There will now be a Policy in your GRC console.  The policy and subscription that deploys gatekeeper will share a placement rule, so both will always target the same clusters (gatekeeper will always be installed wherever the policy is being applied)
