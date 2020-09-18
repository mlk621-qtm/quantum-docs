---
title: Azure Quantum Release Notes
description: Learn about the latest updates of the Azure Quantum service. 
author: geduardo
ms.author: v-edsanc@microsoft.com
ms.date: 07/27/2020
ms.topic: article
uid: microsoft.azure.quantum.relnotes
---

# Azure Quantum Release Notes

## 2020-08-31: Bug Fixes & Job Scheduling Perf Improvements
- Fixed a bug where the `all_betas` parameter returned from parameter-free solvers was named `betas`

## 2020-08-25: Job Shop Optimization Sample now Available
[The sample for job shop optimization is now available in the Samples folder](https://github.com/MicrosoftDocs/quantum-docs-private/blob/feature/onboarding-azure-quantum/azure-quantum/samples/job-shop-sample/). This complete sample teaches:
- What the job shop scheduling problem is and why it is important
- How to represent problem terms mathematically
- How to build penalty functions to represent problem constraints
- How to transform these mathematical functions into code using the Azure Quantum Optimization Python SDK
- How to submit problem terms to Azure Quantum
- How to interpret the results

## 2020-08-24: Parameter-free solvers now return parameters
A highly requested feature – the ability to see the parameters chosen by parameter-free solvers – is now available. When running a problem against a parameter-free solver you will now see a “parameters” object returned in the job result. These parameters were used to generate the returned configuration.

```json
{
    "configuration": {
        "0": 1,
        "1": -1,
        "2": 1
    },
    "cost": 0.4,
    "parameters": {
        "all_betas": [
            0.1,
            0.2,
            0.3
        ],
        "replicas": 3,
        "sweeps": 100
    }
}
```

No SDK updates are needed to take advantage of this update.