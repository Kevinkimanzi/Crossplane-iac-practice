# Crossplane-iac-practice
A simple demo on Using crossplane to create infrastructure

Crossplane is an open-source project that extends the kubernetes API to allow users to manage infrastructure resources alongside application workload

### why crossplane 
1.Crossplane easily integrates with GitOps workflows.

2.Crossplane will automatically correct drift.

3.Crossplane doesn’t need a state to be stored.

4.multi cloud and hybrid-cloud support

## Crossplane provider
Providers are Crossplane packages that bundle a set of Managed Resources and controllers to allow Crossplane to provision and manage the respective infrastructure resources

## CRD VS Controller vs Operators
CRD(Custom Resource Definitions) Allow you to define resources

controller manages the lifecycle of resources

Operator are specialized type of controller that automate the management of complex application by extending the kubernetes API.

## How crossplane works

A provider CRD maps to individual resources inside the provider. When crossplane creates and monitor resources its a managed resources

Using provider CRD creates a unique managed resource.

The crossplane controller provide a state enforcement for managed resources.
 

# Prerequisites

1.A Kubernetes cluster with at least 2 GB of RAM (Consider Minikube/Kind)

2.Permissions to create pods and secrets in the Kubernetes cluster
Helm version v3.2.0 or later

3.Aws Account with Permission to create the necessary resources (efs, s3 and any other)

4.GCP Account with Permission to create the necessary resources (Storage)

5.Authentication keys for both EKS and GCP

# Quick Set up
 ## Installing Crossplane Helm chart

 ##### Add the Crossplane repository with the helm repo add command.

$ helm repo add crossplane-stable https://charts.crossplane.io/stable

#### Update the local Helm chart cache with helm repo update.

$ helm repo update

### Install the Crossplane Helm chart 

helm install crossplane \
--namespace crossplane-system \
--create-namespace crossplane-stable/crossplane 


View the installed Crossplane pods with  

$ kubectl get pods -n crossplane-system.

### Install AWS provider(EFS)

kubectl apply -f .providers/aws-provider-config.yaml

kubectl apply -f ./providers/provider-aws-efs.yaml

Verify: kubectl get providers

## Create a Kubernetes secret for Aws
The provider requires credentials to create and manage AWS resources. Providers use a Kubernetes Secret to connect the credentials to the provider.

Generate a Kubernetes Secret from your AWS key-pair and then configure the Provider to use it.

Generate an AWS key-pair file
[default]
aws_access_key_id = <>

aws_secret_access_key = <>

save the above as credentials.txt

# Create a Kubernetes secret with the AWS credentials

kubectl create secret \
generic aws-secret \
-n crossplane-system \
--from-file=creds=./credentials.txt

Verify: kubectl describe secret aws-secret -n crossplane-system

# Create a managed resources (EFS)

Create filesystem

kubectl apply -f ./resources/aws-efs/filesystem.yaml

Create Access Point

kubectl apply -f ./resources/aws-efs/accesspoint.yaml

Create file system policy

kubectl apply -f ./resources/aws-efs/filesystem-policy.yaml

Create Mount Target

kubectl apply -f ./resources/aws-efs/mount-target.yaml

Create replication configuration

kubectl apply -f ./resources/aws-efs/replication-configuration.yaml






