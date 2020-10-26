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
9. Click `Add another repository`
10. Choose Gi
11. Click `Save` to deploy gatekeeper
12. Choose the Repository type `Git`
13. Select the Git URL: `https://github.com/open-cluster-management/demo-subscription-gitops.git`
14. Enter or select branch: `gatekeeper`
15. Enter repository path: `opa/gatekeeper-emptysecret`
16. Check teh `Merge udpates` box
17. Choose a label key and value to match your target clusters (The same one used above)
18. Click `Add another repository`
19. Choose the Repository type `Git`
20. Enter or select the Git URL: `https://github.com/open-cluster-management/demo-subscription-gitops.git`
21. Enter or select branch: `gatekeeper`
22. Enter repository path: `opa/policy`
23. Select the `Deploy on local cluster` box
24. Click `Save` to complete

That's it. There will now be a Policy in your GRC console.  The policy and subscription that deploys gatekeeper will share a placement rule, so both will always target the same clusters (gatekeeper will always be installed wherever the policy is being applied)
