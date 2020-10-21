# Demonstrate placement algorithm
## Tool Requirements
- OpenShift CLI Version >= 4.3.0<br>_Needed for kustomize_
```bash
oc version
```

## This example, Deploys nginx with an internal service, that allows reading the Cloud provider and Region json. This is designed to work with the modified Pacman application.
1. Add the subscription to your Red Hat Advanced Cluster Management for Kubernetes HUB
```
clone https://github.com/open-cluster-management/demo-subscription-gitops.git
oc apply -k demo-subscription-gitops/cloud-provider/subscription/
```
### results
This will automatically provision the nginx with cloud provider and region identifier to:
### Amazon AWS
- us-east-1
- us-east-2
- us-east-3
- us-west-1
- eu-central-1
- eu-west-3

### Google GCP
- europe-west3

### Azure
- centralus

### Related
Pacman deployment with an Ansible job in: `ansible/`