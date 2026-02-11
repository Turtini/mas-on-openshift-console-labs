# Lab 01 – Orientation: MAS on OpenShift

## Objective

Understand how IBM Maximo Application Suite (MAS) components map to Red Hat OpenShift constructs.

By the end of this lab, you should be able to:

- Identify the OpenShift project (namespace) where MAS runs  
- Locate MAS workloads in the console  
- Recognize how routes expose MAS applications  
- Understand where persistent storage is attached  
- Describe how MAS relies on Kubernetes primitives  

This lab builds the mental model that supports all future labs.

Estimated time: 20–30 minutes

---

## Prerequisites

- Access to an OpenShift cluster running IBM MAS  
- Permission to view projects and workloads  
- Access to the OpenShift web console  

No CLI access is required.

---

## Conceptual Overview

MAS is not a single application.

It is a collection of workloads running inside one or more OpenShift projects (namespaces).

At a high level:

| MAS Concept | OpenShift Construct |
|-------------|--------------------|
| MAS Suite / App | Deployment / StatefulSet |
| MAS Workspace URL | Route |
| MAS Application Pods | Pods |
| MAS Configuration | ConfigMaps / Secrets |
| MAS Persistent Data | PersistentVolumeClaims (PVCs) |
| MAS Platform Services | Operators + Custom Resources |

Understanding this mapping is critical for safe operations.

---

## Step 1 – Locate the MAS Project (Namespace)

1. Log into the OpenShift web console.
2. In the left navigation, select **Projects**.
3. Search for project names associated with MAS (common patterns may include `mas-`, `maximo-`, or environment-specific naming conventions).
4. Select the primary MAS application project.

### Validate

You should now see:

- Workloads
- Pods
- Routes
- Storage
- ConfigMaps
- Secrets

If you cannot see these resources, verify your access level with your platform administrator.

---

## Step 2 – View MAS Workloads

1. In the selected project, click **Topology** (Developer perspective).
2. Observe the running application components.
3. Switch to **Administrator perspective**.
4. Navigate to **Workloads → Deployments**.
5. Review the list of deployments.

### Observe

- Multiple deployments support MAS.
- Some components may be stateless (Deployments).
- Others may be stateful (StatefulSets).

### Validate

Click into one deployment and confirm:

- Replica count  
- Pod status  
- Resource requests and limits  
- Environment variables  

You should understand which deployment supports which function at a high level.

---

## Step 3 – Identify MAS Application Routes

1. Navigate to **Networking → Routes**.
2. Review available routes.
3. Identify routes that correspond to:
   - MAS Workspace
   - Application UI
   - Supporting services (if exposed)

### Observe

Each Route connects:

Route → Service → Pod

Click into a route and confirm:

- Hostname  
- Target service  
- TLS configuration  

### Validate

Open the route URL in a new browser tab (if permitted).  
Confirm it resolves to a MAS application page.

---

## Step 4 – Locate Persistent Storage

1. Navigate to **Storage → PersistentVolumeClaims (PVCs)**.
2. Review the list of claims associated with MAS.
3. Click into one PVC.

### Observe

- Storage class  
- Access mode  
- Capacity  
- Bound status  

Persistent storage ensures MAS data survives pod restarts.

### Validate

Confirm the PVC status is **Bound**.

If a PVC is not bound, that is a platform-level issue requiring escalation.

---

## Step 5 – Understand Operators (High-Level)

1. Navigate to **Operators → Installed Operators**.
2. Locate operators relevant to MAS (if visible in your access scope).

MAS often relies on operators to manage complex services such as:

- Databases  
- Messaging  
- Platform components  

Operators manage lifecycle, scaling, and health.

No changes should be made in this section unless explicitly authorized.

---

## What You Learned

You should now understand:

- MAS runs inside OpenShift projects (namespaces).
- MAS applications are composed of deployments and pods.
- Routes expose MAS applications externally.
- PVCs provide persistent storage.
- Operators manage supporting platform services.

This mental model is the foundation for safe troubleshooting and operational confidence.

---

## Troubleshooting Tips

If you cannot see MAS projects:
- Verify your role (View, Edit, Admin).
- Confirm you are logged into the correct cluster.

If workloads appear degraded:
- Check **Pods → Status**
- Review **Events**
- Review **Logs**

Do not restart or modify workloads unless authorized.

---

## Operational Discipline Reminder

In regulated environments, clarity reduces risk.

Before making changes, always capture:

- Project name  
- Deployment name  
- Pod name  
- Route  
- Timestamp  

Structured observation prevents unnecessary disruption.
