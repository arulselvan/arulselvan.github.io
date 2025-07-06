---
author: arul
category:
  - software-development
date: "2023-10-30T23:35:53+00:00"
draft: "true"
guid: https://arulselvan.net/?p=706
title: K8s Service Mesh
url: /

---
What is Service Mesh?

A service mesh is a dedicated infrastructure layer that controls service-to-service communication over a network, It can make service-to-service communication fast, reliable, and secure. basically, it removes the burden from the application code for all the infrastructure-related decisions.

Capabilities/Features of Service Mesh:

- service discovery
- load balancing
- encryption
- observability
- traceability
- authentication and authorization
- support for the circuit breaker

How Does Service Mesh Work in k8s?

A service mesh works by using a proxy instance called a sidecar, which runs alongside each service. The sidecar proxy handles all communication between the service and other services. This includes routing requests, load balancing, and encryption.

Available K8s Service Mesh

Istio Vs Linkerd

Linkerd Example
