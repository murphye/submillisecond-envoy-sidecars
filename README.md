# Submillisecond Envoy Sidecars

## Summary

This repository demonstrates how to achieve high throughput and low latencies with an Envoy sidecar when using Istio service mesh. With this demo, you can deploy 3 Java (Spring Boot WebFlux) microservices and a PostgreSQL database in Kubernetes (GKE). You can then run a series of load tests against the demo application both with and without Istio sidecars enabled.

At scale, you will see the delta of latency for Envoy sidecar ingress/egress measure to be less than 1 millisecond. This enables the demo application to have an end-to-end p95 latency of only 10 ms, at 10,000 RPS, while passing through 7 Envoy sidecar ingresses or egresses across 3 microservices and a database.

Optionally, you may scale this demo up to 28,000 RPS with an end-to-end p95 latency of 28 ms. This demonstrates a more constrained cluster that is consuming a higher level of CPU and memory resources, but is still able to maintain acceptable performance.

Ultimately, this demo shows that with best practices for deploying applications at scale on Kubernetes, Envoy sidecars are up to the task for low latency and high throughput applications.

## [Setup Guide](SETUP.md)

## Demo Performance Requirements

When conducting performance testing, it's important to have specific performance requirements to target. Running naive performance tests with no goals in mind will create results that do not translate to the real world. For example, it's good practice to throttle a load test client at a threshold that meets performance requirements to show true latency metrics. This compares to ramming as much traffic into the application as possible which kills the latency metrics.

Here are the performance requirements used for the demos:

### Performance Requirements #1 (Low Latency for Demo #2)

1. At least 10,000 requests per second (RPS)
1. At most 10 milliseconds (ms) end-to-end latency using a client within the same datacenter/zone as the cluster
1. No HTTP errors for 1,000,000 requests (after proper warm up run)

### Performance Reqirements #2 (High Throughput for Demo #3)

1. At least 28,000 requests per second (RPS)
1. At most 28 milliseconds (ms) end-to-end latency using a client within the same datacenter/zone as the cluster
1. No HTTP errors for 1,000,000 requests (after proper warm up run)

Note: 30K RPS was not obtainable during testing due to a probable database bottleneck.

## Demo #1 with Deployment Replication of 1 (Poor Sidecar Performance with Naive Load Testing)

## Demo #2 with Deployment Replication of 3 (Achieving Low Latency at 10K RPS)

## Demo #3 with Deployment Replication of 8 (Achieving 28K RPS in a Constrained Cluster)

## Recommendations and Best Practices
