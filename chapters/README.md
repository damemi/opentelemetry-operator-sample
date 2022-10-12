# OpenTelemetry the Easy Way

This folder contains the chapters that make up an interactive tutorial for getting started
with the OpenTelemetry Operator. Each chapter uses the [sample apps](../sample-apps) and
[recipes](../recipes) from this repo to build a realistic scenario in which those samples
could be applied.

In this story you assume the role of the new technical lead at a fledgling startup, FooCo. The
company is excited to launch and grow, and it's your job to help that go smoothly using
OpenTelemetry.

The chapters are roughly organized into the following sections:

## Section 1 - Background

Chapters in this section are designed to set the stage for any reader choosing to follow this guide
from the beginning. This includes setting up prerequisite accounts and tools, deploying a sample app,
and getting started with OpenTelemetry SDKs and the [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/).

* [Chapter 0: Onboarding](chapter-0)
  
  Set up the prerequisites for this tutorial.
  
* [Chapter 1: Your first app](chapter-1)
  
  Deploy a sample application which you'll use for the next chapters.
  
* [Chapter 2: Your first trace](chapter-2)
  
  Learn how to manually instrument traces in your app.
  
* [Chapter 3: Switching backends](chapter-3)
  
  Use the OpenTelemetry Collector to route observability data to different tools.
  
## Section 2 - Getting to know the Operator

This section is all about getting started with the [OpenTelemetry Operator](https://github.com/open-telemetry/opentelemetry-operator).
It builds on the lessons from the first section about writing manual instrumentation
and deploying the Collector to show how the Operator makes these tasks easier.

* [Chapter 4: Auto-instrumentation](chapter-4)
  
  Deploy the OpenTelemetry Operator to instrument apps without code changes.
  
* [Chapter 5: Configuring the Collector](chapter-5)
  
  Use the OpenTelemetry Operator to deploy and manage a Collector.
  
* [Chapter 6: Advanced instrumentation configuration](chapter-6)
  
  Learn about the range of options offered by the Operator's auto-instrumentation config object.

* [Chapter 7: Advanced Collector configuration](chapter-7)
  
  Learn about the range of options offered by the Operator's Collector config object.

  
## Section 3 - Recipes

These chapters show more complex and interesting use cases for the Operator. They can
be completed in any order.
  
* Chapter N: Resource detection
  
  Inject environment and provider attributes into telemetry.
  
* Chapter N: Redacting sensistive data
  
  Obscure data from telemetry data.
  
* Chapter N: Auto-instrumentation II
  
  Learn other ways to auto-instrument applications, such as with Cloud Build and code generation.
