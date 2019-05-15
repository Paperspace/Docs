---
description: >-
  Gradient Deployments enable a hassle-free, automatic “push to deploy” option
  for any trained model. These allow ML practitioners to quickly validate
  “end-to-end” services from R&D to production.
---

# About

![](../.gitbook/assets/image%20%2815%29.png)

{% hint style="info" %}
**Note:** Gradient Deployments are still in Beta. During the Beta period we do not recommend running mission-critical services. Additionally, API endpoints could be renamed/updated and there are certain restrictions placed on accounts. Learn more about restrictions below
{% endhint %}

## Overview

Deploy any model as a high-performance, low-latency micro-service with a RESTful API. Easily monitor, scale, and version deployments.  Deployments take a trained model and expose them as a persistent service at a known URI.

## Current Limitations

During the Beta period, Gradient Deployments have a number of restrictions.

* Teams are limited to a single running deployment. 
* Only K80 and CPU nodes are supported.
* The exposed endpoint URI is subject to change.
* Billing for deployments is not currently enabled. You will not see Gradient Deployments on your invoice.

## Deployment States

Deployments go through a series of states. They are enumerated here:

| ID | Name |
| :--- | :--- |
| 1 |  `Building`  |
| 2 | `Provisioning` |
| 3 | `Starting` |
| 4 | `Running` |
| 5 | `Stopping` |
| 6 | `Stopped` |
| 7 | `Error` |

