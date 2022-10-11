# Chapter 0: Onboarding

## Objective

By the end of this chapter you should have all of the necessary accounts set up and tools installed
to complete the rest of the chapters in this guide.

## Tasks

Install the following software:
* [Docker](https://docs.docker.com/engine/install/)

Install [`cert-manager`](https://cert-manager.io) in your cluster. On GKE Autopilot, do this
with [Helm](https://helm.sh) using the following commands:

```
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install \
  --create-namespace \
  --namespace cert-manager \
  --set installCRDs=true \
  --set global.leaderElection.namespace=cert-manager \
  --set extraArgs={--issuer-ambient-credentials=true} \
  cert-manager jetstack/cert-manager
```
