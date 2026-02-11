# MAS on OpenShift – Console Labs

Console-based training labs for IBM Maximo Application Suite (MAS) operators running on Red Hat OpenShift.

This repository is designed for platform operators, application administrators, and public sector teams who run MAS on OpenShift and want practical, console-first operational fluency — without requiring `kubectl` or deep Kubernetes engineering experience.

---

## Why This Exists

IBM Maximo Application Suite runs on Red Hat OpenShift.

Many MAS users are experts in:
- Asset management  
- Work management  
- Reporting (BIRT)  
- Operational workflows  

But they are not always Kubernetes engineers — and they shouldn’t need to be.

These labs bridge that gap.

This repository focuses on:

- How to navigate the OpenShift web console with confidence  
- How to understand projects (namespaces) and access controls  
- How services and routes expose applications  
- How resource requests and limits affect stability  
- How to troubleshoot using logs and events  
- How to gather useful artifacts when reports or workloads fail  

All labs are written to be completed entirely in the OpenShift web console.

---

## Curriculum Philosophy

This repository is intentionally different from traditional “lab build” training.

It does not require:

- Building a new cluster
- Running infrastructure automation
- Debugging installation failures
- Constructing a synthetic training environment

It assumes the platform already exists.

Many teams do not need to learn how to install OpenShift or MAS.
They need to understand how to operate what they already have.

This curriculum focuses on:

- Interpreting real workloads
- Navigating live environments safely
- Understanding resource behavior
- Gathering structured evidence
- Practicing disciplined change management

It is designed for operational fluency — not infrastructure assembly.

In regulated environments, confidence comes from clarity, not complexity.

These exercises help operators understand, interpret, and optimize their existing environment without introducing unnecessary risk or frustration.

---

## Intended Audience

- IBM MAS application administrators  
- Reporting (BIRT) developers  
- Public sector platform operators  
- Regulated environment teams (federal, state, or enterprise)  
- Anyone who operates MAS but does not want to rely on CLI access  

---

## What This Is (and Is Not)

### This is:
- A console-first operational lab series  
- A reusable enablement artifact for regulated environments  
- Practical day-2 operational fluency  

### This is not:
- A full MAS installation guide  
- A Kubernetes deep-dive course  
- A replacement for vendor documentation  

---

## Lab Structure

Each lab follows a consistent format:

1. Objective  
2. Prerequisites  
3. Step-by-step console workflow  
4. Validation checks  
5. Troubleshooting guidance  
6. What you learned  

Estimated time per lab: 15–45 minutes.

---

## Labs

### 01 – Orientation: MAS on OpenShift
How MAS components map to OpenShift constructs (projects, deployments, routes, PVCs, operators).

### 02 – Console Navigation
Switching perspectives, finding workloads, viewing logs and events.

### 03 – Projects and Access
Creating and understanding projects (namespaces), roles, and isolation boundaries.

### 04 – Deployments, Services, and Routes
How applications become reachable. Understanding Service → Route → Pod relationships.

### 05 – Resources and Quotas
CPU/memory requests and limits, quotas, and how resource constraints impact stability.

### 06 – Observability
Using logs, events, rollout history, and metrics to diagnose failures.

### 07 – MAS in the Console
Locating MAS workloads, operators, and application routes safely.

### 08 – BIRT and Report Troubleshooting
Console-based workflow for collecting logs, identifying reporting pods, checking storage mounts, and preparing incident packets for escalation.

### 09 – Day 2 Operational Readiness
Develop a structured approach to managing MAS workloads in steady-state operations (Day 2).

---

## Operational Philosophy

In regulated environments, operational clarity reduces risk.

When something fails, the most valuable response is not guesswork — it is structured evidence:

- Namespace  
- Deployment name  
- Pod name  
- Route  
- Logs  
- Events  
- Resource allocations  
- Storage claims  

These labs emphasize disciplined troubleshooting that supports auditability and rapid escalation.

---

## Reuse and Adaptation

This work is intentionally public and reusable.

Organizations may fork, adapt, and extend these labs to support internal training, platform enablement, and operational standardization.

Licensed under Apache License 2.0.

---

## About Turtini

Turtini is a specialized partner focused on reducing operational friction in regulated Red Hat environments.

We emphasize precision, transparency, and reusable public artifacts that strengthen platform maturity.
