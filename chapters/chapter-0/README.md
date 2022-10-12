# Chapter 0: Onboarding

Welcome to FooCo! We are excited to have you join our team. While we are all saddened by the departure of your predecessor,
the zookeepers have assured us that the walls of the ratite enclosure have been reinforced and that a similar incident at our
next company outing is highly unlikely. So you have nothing to worry about!

Here at FooCo, we deploy software. Right now we just have one app, which you will launch for us soon. In the future, we hope
to work with clients to help them run and manage their apps too. That's an ambitious goal, but with your expertise in
observability we're confident that it's manageable.

First, we'll need to get you started with everything you need to do your job. This is all standard onboarding stuff: install
some software, set up some of our infrastructure, and ensure you are up-to-date on all your inoculations against avian-borne disease.
The usual first-day activities for any job.

## Objective

By the end of this chapter you should have all of the necessary accounts set up and tools installed
to complete the rest of the chapters in this guide.

## Tasks

### Set up GCP infrastructure

Create a [GCP account](https://cloud.google.com/gcp).
* Create a [GCP project](https://cloud.google.com/resource-manager/docs/creating-managing-projects)
* Enable [billing for your project](https://cloud.google.com/billing/docs/how-to/modify-project)
* Enable the following APIs in your GCP project:
  * Kubernetes Engine (GKE)
  * Artifact Registry
  * Cloud Trace
* [Create a Kubernetes cluster](https://cloud.google.com/kubernetes-engine/docs/how-to/creating-an-autopilot-cluster) in your GCP project

### Install local software

Install the following software:
* [Docker](https://docs.docker.com/engine/install/)
* [NodeJS](https://nodejs.org/en/)
* [Helm](https://helm.sh/)
* [gcloud](https://cloud.google.com/sdk/docs/install)
* [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
  * Also [install the kubectl auth plugin for GCP](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl)

### Install cluster software

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

## Summary

You should now be all set to launch our first app. Move on to [Chapter 1](../chapter-1) to learn how.
