# Crossplane-iac-practice
A simple demo on Using crossplane to create infrastructure

Crossplane is an open-source project that extends the kubernetes API to allow users to manage infrastructure resources alongside application workload

### why crossplane 
1.Crossplane easily integrates with GitOps workflows.

2.Crossplane will automatically correct drift.

3.Crossplane doesn’t need a state to be stored.

4.multi cloud and hybrid-cloud support

# Prerequisites

1.A Kubernetes cluster with at least 2 GB of RAM (Consider Minikube/Kind)

2.Permissions to create pods and secrets in the Kubernetes cluster
Helm version v3.2.0 or later

3.Aws Account with Permission to create the necessary resources (efs, s3 and any other)

4.GCP Account with Permission to create the necessary resources (Storage)

5.Authentication keys for both EKS and GCP

# Quick Set up


