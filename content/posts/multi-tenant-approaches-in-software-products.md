---
author: arul
category:
  - software-development
cover:
  alt: image
  image: /wp-content/uploads/2023/12/image.png
date: "2024-09-20T07:02:00+00:00"
guid: https://arulselvan.net/?p=724
title: Multi-Tenant Approaches In Software Products
url: /multi-tenant-approaches-in-software-products/

---
**What is multi-tenancy?**

Multitenancy is a software architecture where a single software instance can serve multiple, distinct user groups. or common infrastructure shared across multiple, distinct user groups. Software-as-a-service (SaaS) offerings are an example of multi-tenant architecture

![](/wp-content/uploads/2023/11/multi-tenancy.png)

**Approaches to Implement Multi-Tenancy** **Capability**

There are below two types of approaches or a combination of both, used in the Multi-Tenancy

- **Application Level**
- **Infrastructure Level**

##### Application Level:

In this model, a single instance of the application serves requests from multiple tenants. The application code is responsible for keeping each tenant's data separate and making sure other tenants can't see any data or activity that does not belong to them

![](/wp-content/uploads/2023/12/image.png)

Simple Example Nodejs Code Snip:

```
// app.js
const express = require('express');
const mongoose = require('mongoose');
const tenantMiddleware = require('./middleware/multitenancy');

const app = express();

// Use the multitenancy middleware
app.use(tenantMiddleware);

// Your routes and other middleware go here

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

```

In the above simple nodejs example, express tenantMiddleware extracts the tenant identifier from the request (e.g., from a subdomain or a header) and sets the database connection based on the extracted tenant identifier. a database, each tenant can have its own database or schema within a shared database.

##### Infrastructure Level:

The infrastructure level involves creating an environment that efficiently supports the requirements of multiple tenants. This typically involves considerations at various levels of your infrastructure stack (through Virtualization, Container Orchestration, etc..) Below, we are going to see only the Infra Level on the Kubernetes platform:

_**What is Kubernetes?**_  
Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services that facilitates both declarative configuration and automation

**K8s Namespace Level Tenancy:**

In Kubernetes, _namespaces_ provide a mechanism for isolating groups of resources within a single cluster. Using this approach, each tenant will have its dedicated namespace to isolate all of their resources. only common resources will be shared across all the tenants.

![](/wp-content/uploads/2023/12/image-1.png)

**K8s Cluster-level tenancy:**

Each tenant will have a dedicated K8s cluster and will not share resources because it creates strong isolation between tenants.

![](/wp-content/uploads/2023/12/image-2.png)

**Conclusion:**

**Application Level:** application to be written for multi-tenancy to isolate tenants; complete infrastructure can be shared, with low infrastructure costs and high tenant density possible.

**Infra Level:** without writing any code changes, existing single-tenant applications can also be deployed for multi-tenancy capability.  
 \- Namespace Level: Medium tenant density and medium infrastructure cost per tenant  
 \- Cluster Level: Low tenant density and high infrastructure costs per tenant.

These approaches are not mutually exclusive and can be combined to provide the best fit for your application or to address the requirements of specific tenants. For example, an application that implements multi-tenancy could be deployed as multiple instances with either namespace-level or cluster-level tenancy to provide enhanced security protections and to contain the potential impact of vulnerabilities on a limited number of tenants.

Many SaaS providers operate on a subscription model, offering various tiers, for example: free, professional, and enterprise.

In the free tier, a code-level multi-tenant application can be deployed on a single namespace (Free), allowing for high-density usage.

For the Professional tier, each tenant can utilize their dedicated namespace, ensuring better control over hardware and network resources.

In enterprise subscriptions, providers may offer a dedicated cluster with dedicated hardware tailored to meet the specific requirements of the client.
