# Lab 04 – Deployments, Services, and Routes

## Objective

Deploy a simple application in a project and expose it using a Route.

By the end of this lab, you should be able to:

- Deploy a container using the OpenShift console
- Understand the difference between a Deployment and a Pod
- Identify the Service created for your application
- Create and validate a Route
- Explain the relationship: Route → Service → Pod

Estimated time: 30–40 minutes

---

## Prerequisites

- Access to OpenShift web console
- Access to a non-production project (lab project recommended)
- Edit or Admin permissions in the project

No CLI access is required.

---

## Conceptual Overview

In OpenShift:

- A **Deployment** manages Pods.
- A **Pod** runs containers.
- A **Service** provides stable internal networking.
- A **Route** exposes a Service externally.

The traffic flow is:

Route → Service → Pod

Understanding this chain prevents common troubleshooting errors.

---

## Step 1 – Deploy a Simple Application

1. Switch to **Developer** perspective.
2. Ensure your lab project is selected.
3. Click **+Add**.
4. Choose **Container Image**.
5. In the image field, enter:

