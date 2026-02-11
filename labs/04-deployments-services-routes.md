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

```yaml
quay.io/openshift/hello-openshift
```

6. Click **Search**.
7. Leave defaults unless your cluster requires adjustments.
8. Click **Create**.

### Observe

- A Deployment is created.
- A Pod starts.
- A Service is automatically generated.

### Validate

Go to **Topology** and confirm:

- The application appears
- The pod status becomes **Running**

---

## Step 2 – Inspect the Deployment

Switch to **Administrator** perspective.

1. Navigate to **Workloads → Deployments**.
2. Select your deployment.
3. Review:
- Replica count
- Strategy
- Resource requests and limits
- Pod template details

### Observe

The Deployment manages Pods.  
If a Pod fails, the Deployment replaces it.

### Validate

Click the **Pods** tab and confirm:

- At least one pod is running
- The pod name matches the deployment prefix

---

## Step 3 – Inspect the Service

1. Navigate to **Networking → Services**.
2. Locate the service associated with your deployment.
3. Click into it.

### Observe

- Selector labels
- Target port
- Cluster IP

Services provide stable internal connectivity even if Pods restart.

### Validate

Confirm the Service selector matches the labels on your Pod.

---

## Step 4 – Create a Route

If a Route was not automatically created:

1. Navigate to **Networking → Routes**.
2. Click **Create Route**.
3. Select your Service.
4. Leave hostname blank (auto-generated).
5. Choose TLS settings if required by cluster policy.
6. Click **Create**.

### Observe

The Route now points to your Service.

### Validate

1. Click the Route URL.
2. Open it in a new browser tab.
3. Confirm you see the Hello OpenShift page.

If access fails:
- Confirm the pod is running.
- Confirm the Service selector is correct.
- Check Events for errors.

---

## Step 5 – Scale the Application

1. Navigate back to **Workloads → Deployments**.
2. Edit the replica count from 1 to 2.
3. Save changes.

### Observe

A second pod is created.

### Validate

- Confirm two pods are running.
- Refresh the Route URL.
- The application remains accessible.

The Service distributes traffic across pods automatically.

---

## Step 6 – Simulate a Safe Restart

1. In the Deployment view, select **Restart Rollout**.
2. Observe pods terminating and being recreated.

### Observe

- New pod names are generated.
- The Service continues routing traffic.
- The Route remains stable.

This demonstrates resilience.

---

## What You Learned

You should now understand:

- Deployments manage Pods.
- Services provide internal stability.
- Routes expose applications externally.
- Scaling increases pod replicas.
- Restarting a deployment does not change the Route.

Application stability depends on understanding these relationships.

---

## Common Troubleshooting Scenarios

If the Route does not work:

- Pod not running
- Service selector mismatch
- Incorrect target port
- TLS misconfiguration
- Resource constraints preventing pod startup

Always check:

1. Pod status
2. Events
3. Logs
4. Service configuration
5. Route configuration

---

## Operational Discipline Reminder

Before modifying production workloads:

- Confirm project
- Confirm environment
- Confirm replica count
- Capture current configuration
- Understand blast radius

In regulated environments, controlled change prevents outages.

---

## Optional Cleanup

If this was a lab project:

1. Delete the Deployment.
2. Confirm the Service and Route are removed (or delete manually).
3. Verify no orphaned resources remain.

Intentional cleanup reinforces operational maturity.

