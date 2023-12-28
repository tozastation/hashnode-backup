---
title: "K8sGPT: Overview"
datePublished: Thu Dec 28 2023 05:55:08 GMT+0000 (Coordinated Universal Time)
cuid: clqosjdh2000i08l987f77qod
slug: k8sgpt-overview
tags: kubernetes, openai, gpt-4, k8sgpt

---

## What is [K8sGPT](https://github.com/k8sgpt-ai/k8sgpt)

> It has SRE experience codified into its analyzers and helps to pull out the most relevant information to enrich it with AI.  
> README.md, k8sgpt, [https://github.com/k8sgpt-ai/k8sgpt](https://github.com/k8sgpt-ai/k8sgpt)

## SRE Experience & Analyzers

A class called Analyzer is defined for each resource in Kubernetes. Analyzer has Core (Pod, PVC, ReplicaSet, etc...) and Optional (HPA, PDB, NetworkPolicy, etc ...). You can choose your own or leave it to the default. See [here](https://github.com/k8sgpt-ai/k8sgpt?tab=readme-ov-file#analyzers) for a complete list. Analyzer has validations defined for each resource. The content of this validation is connected to 'SRE experience'. Verification content is manually defined.

### Example: SRE Experience

* Deployment Analyzer
    
    * Regarding Replicas, Desire and Actual do not match. ([here](https://github.com/k8sgpt-ai/k8sgpt/blob/main/pkg/analyzer/deployment.go) impl.)
        
* PVC Analyzer
    
    * If the PVC status is Pending and EventReason is Provisioning Failed.
        
* Node Analyzer
    
    * If the node status corresponds to Node Not Ready or DiskPressure, MemoryPressure, PIDPressure, NetworkUnavailable
        

## Where is GPT used?

K8sGPT will send the following prompts along with the findings from the Analyzer. In the prompt below, you can see that we are asking GPT to provide a solution based on the error.

> Simplify the following Kubernetes error message delimited by triple dashes written in --- %s --- language; --- %s ---.  
> Provide the most possible solution in a step by step style in no more than 280 characters.  
> Write the output in the following format: Error: {Explain error here} Solution: {Step by step solution here}
> 
> [https://github.com/k8sgpt-ai/k8sgpt/blob/main/pkg/ai/prompts.go](https://github.com/k8sgpt-ai/k8sgpt/blob/main/pkg/ai/prompts.go)

## Contributing

If you would like to implement this kind of functionality in Analyzer based on your knowledge of Kubernetes operations, please read this document! ([here](https://github.com/k8sgpt-ai/k8sgpt/blob/main/CONTRIBUTING.md))