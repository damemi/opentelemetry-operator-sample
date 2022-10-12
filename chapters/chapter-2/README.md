# Chapter 2: Your first trace

Some of our users are complaining about high latency in our product. But, we're not sure whether this latency is coming from the
client or the server. Our logs aren't much help, and besides we don't want to fill up our log storage with debug messages.
We need a way to diagnose which of our microservices is having trouble.

When they pulled your predecessor from the ratite enclosure, she was muttering something about "tracing." No one else here at
FooCo knows what that means, but we found this guide among her effects that looks to be helpful. Follow it to set up tracing
and see if that helps pinpoint the issue.

## Objective

Learn how to manually instrument tracing.

## Tasks

Open a new terminal window to complete the tasks in this chapter.

### Installing Jaeger to visualize traces

Install [Jaeger](https://www.jaegertracing.io/) in your GKE cluster by following
the [installation steps on the Jaeger docs](https://www.jaegertracing.io/docs/1.24/operator/):

```
kubectl create namespace observability
kubectl create -f https://github.com/jaegertracing/jaeger-operator/releases/download/v1.38.0/jaeger-operator.yaml -n observability
```

[Create a Jaeger instance](https://www.jaegertracing.io/docs/1.24/operator/#quick-start---deploying-the-allinone-image)
with [`jaeger-inst.yaml`](jaeger-inst.yaml):

```
kubectl apply -f jaeger-inst.yaml -n observability
```

### Modifying the sample app

Navigate to the [NodeJS sample app](../../sample-apps/nodejs):

```
cd ../../sample-apps/nodejs
```

### Adding auto-instrumentation libraries

Install the `npm` modules for OpenTelemetry:

```
npm install @opentelemetry/sdk-node @opentelemetry/api @opentelemetry/auto-instrumentations-node @opentelemetry/exporter-jaeger
```

These modules contain the following:
* [`@opentelemetry/api`](https://www.npmjs.com/package/@opentelemetry/api): OpenTelemetry basic library for JavaScript
* [`@opentelemetry/sdk-node`](https://www.npmjs.com/package/@opentelemetry/sdk-node): OpenTelemetry SDK for NodeJS
* [`@opentelemetry/auto-instrumentations-node`](https://www.npmjs.com/package/@opentelemetry/auto-instrumentations-node): Automatic instrumentation
  module for common NodeJS libraries such as `http` and `express`.
* [`@opentelemetry/exporter-jaeger`](https://www.npmjs.com/package/@opentelemetry/exporter-jaeger): Jaeger exporter library.

Modify [`app.js`](app.js) to initialize the OpenTelemetry SDK and a Jaeger exporter to write traces to the Jaeger
instance you created earlier:

```
cp ../../chapters/chapter-2/app.js .
```

### Building the new application code

Modify the [`Dockerfile`](Dockerfile) to include the new Node modules in the app's container image:

```
cp ../../chapters/chapter-2/Dockerfile .
```

Build and push the new app and server code:

```
make build
make push
```

### Deploying the changes

Roll out a new deployment of the NodeJS app (created in [Chapter 1](chapter-1)) with the following commands:

```
kubectl rollout restart deployment.apps/nodeshowcase-app -n $NODEJS_NS
kubectl rollout restart deployment.apps/nodeshowcase-service -n $NODEJS_NS
```

### Viewing the traces

Expose the Jaeger service port on your local machine with the following command:

```
kubectl port-forward service/jaeger-query -n observability 16686
```

Then open your browser and navigate to `localhost:16686`.

## Summary

You have saved the day. Now that we know where the issue is, we can adjust our SLOs to match. Now our users will be happy!

But, it is kind of a pain now that we have to manage this Jaeger instance ourselves. Our team is considering switching
to [Cloud Trace](https://cloud.google.com/trace) as our backend, and we're hoping you can make that switch without
any downtime. You should be able to do that in [Chapter 3](../chapter-3).
