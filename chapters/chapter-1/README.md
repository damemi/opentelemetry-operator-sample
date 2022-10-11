# Chapter 1: Your first app

## Objective

By the end of this chapter you will have a basic sample app deployed in your cluster.

## Tasks

Open a new terminal window to do the tasks in this chapter.

### Building and deploying a basic app

First, make sure you [have `kubectl` installed and can connect to your GKE cluster](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl).

Build the [NodeJS sample app](../../sample-apps/nodejs) with the following commands:

```
cd ../../sample-apps/nodejs
make build
make push
```

Create a new namespace for this app and deploy it in the cluster:

```
export NODEJS_NS=nodejs-sample
kubectl create namespace $NODEJS_NS
kubectl apply -f k8s/. -n $NODEJS_NS
```

After a few moments, the app will be running. You can confirm this by running:

```
kubectl get all -n $NODEJS_NS
```

This command should print output similar to the following:

```
NAME                                        READY   STATUS    RESTARTS   AGE
pod/nodeshowcase-app-77dd58cf56-rt9vz       1/1     Running   0          32s
pod/nodeshowcase-service-6474f5bdd8-4j6gb   1/1     Running   0          31s

NAME                           TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
service/nodeshowcase-service   ClusterIP   10.8.129.172   <none>        80/TCP    32s

NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nodeshowcase-app       1/1     1            1           33s
deployment.apps/nodeshowcase-service   1/1     1            1           32s

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/nodeshowcase-app-77dd58cf56       1         1         1       33s
replicaset.apps/nodeshowcase-service-6474f5bdd8   1         1         1       32s
```

You can verify that the app and server are running with the `kubectl logs` command:

```
$ kubectl logs pod/nodeshowcase-service-6474f5bdd8-4j6gb -n $NODEJS_NS
serving on port 8080...

$ kubectl logs pod/nodeshowcase-app-77dd58cf56-rt9vz -n $NODEJS_NS
starting app for service at http://nodeshowcase-service/
{ data: 'Hello world' }
{ data: 'Hello world' }
...
```

> Note: the app may log "connection refused" errors for the first few seconds as the service starts up.

## Summary

Congratulations! Our first app is launched and working flawlessly. Hopefully, nothing will ever
go wrong. But just in case it does, let's learn how to manually instrument traces with
OpenTelemetry in [Chapter 2](../chapter-2).
