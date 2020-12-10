# GitOps driven policy demonstration
- Log into the hub cluster.
- Activate the gitops subscription.
```bash
oc apply -k subscripton/
```
- Navigate to the Governance, Risk, and Policy section in the console. You will see a policy.
- Adjust the `placementRule` for the policy to target the correct clusters.
- Adjust the policy itself to target different namespaces. This can all be done in Git and will be reflected in the hub cluster.
