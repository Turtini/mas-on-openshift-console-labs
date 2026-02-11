# Lab 05 – Resources and Quotas

## Objective

Understand how CPU and memory resources are allocated in OpenShift and how resource constraints affect application stability.

By the end of this lab, you should be able to:

- Explain the difference between resource **requests** and **limits**
- Locate resource settings for a deployment
- Identify resource quotas and limit ranges in a project
- Recognize symptoms of memory or CPU pressure
- Understand why resource configuration impacts MAS workloads and reporting (including BIRT)

Estimated time: 30–40 minutes

---

## Prerequisites

- Access to OpenShift web console
- Edit access to a non-production project (lab project recommended)
- A running deployment from Lab 04

No CLI access is required.

---

## Conceptual Overview

Every container in OpenShift can define:

- **CPU Request** – The amount of CPU guaranteed to the container
- **CPU Limit** – The maximum CPU the container can use
- **Memory Request** – The amount of memory reserved for scheduling
- **Memory Limit** – The maximum memory the container can consume

Think of it this way:

- Request = reservation
- Limit = ceiling

If a container exceeds its memory limit, it is terminated by the system.

This often appears as:

`OOMKilled`

In reporting-heavy environments (such as BIRT workloads), insufficient memory limits are a common failure cause.

---

## Step 1 – Review Resource Settings on a Deployment

1. Switch to **Administrator** perspective.
2. Navigate to **Workloads → Deployments**.
3. Select the deployment created in Lab 04.
4. Scroll to the **Pod Template** section.
5. Locate **Resource Requests and Limits**.

### Observe

- CPU request (example: 10m, 100m, 500m)
- Memory request (example: 64Mi, 256Mi, 512Mi)
- CPU limit
- Memory limit

### Validate

Record:

- CPU request
- CPU limit
- Memory request
- Memory limit

Understanding current configuration is required before making changes.

---

## Step 2 – Edit Resource Limits

In your lab project (non-production only):

1. Select the deployment.
2. Click **Actions → Edit Resource Limits** (or Edit YAML if required).
3. Modify memory limit to a lower value (example: reduce by 50%).
4. Save changes.

### Observe

- A new rollout begins.
- Pods restart with new limits.

### Validate

Confirm:

- Updated limits are visible in deployment details.
- New pod is running successfully.

---

## Step 3 – Monitor Metrics

1. Click the running Pod.
2. Navigate to the **Metrics** tab (if enabled).
3. Observe memory and CPU graphs.

### Observe

- Memory usage relative to limit
- CPU consumption spikes

### Validate

Determine whether memory usage approaches the limit.

If memory consumption reaches the limit, the pod may restart.

---

## Step 4 – Recognize Resource Failures

Navigate to:

- **Pods**
- Select a pod
- Click **Events**

Common resource-related events include:

- OOMKilled
- Container terminated due to memory limit
- Failed scheduling due to insufficient resources

### Validate

Confirm you can identify:

- Restart count
- Termination reason
- Relevant event messages

---

## Step 5 – Review Project Resource Controls

Navigate to:

**Administrator → Administration → ResourceQuotas**

If present, review:

- Total CPU quota
- Total memory quota
- Object limits (pods, services, etc.)

Then navigate to:

**Administrator → Administration → LimitRanges**

### Observe

LimitRanges may:

- Set default requests
- Set default limits
- Enforce minimum/maximum thresholds

### Validate

Confirm whether your project:

- Has no quotas
- Has defined quotas
- Has defined limit ranges

Resource controls protect cluster-wide stability.

---

## Real-World Context: MAS and Reporting

Reporting workloads (including BIRT-based reports) often:

- Consume high memory during execution
- Generate large temporary objects
- Spike CPU during rendering

If memory limits are too low:

- Reports fail
- Pods restart
- Users experience errors

Resource configuration must reflect workload behavior.

---

## What You Learned

You should now understand:

- The difference between requests and limits
- How to view and edit resource settings
- How resource limits affect application behavior
- Where to check for OOMKilled events
- How quotas protect shared infrastructure

Resource configuration is not arbitrary — it directly impacts system stability.

---

## Common Mistakes

- Setting limits too low for memory-intensive workloads
- Ignoring restart counts
- Confusing CPU throttling with failure
- Modifying production limits without change control
- Failing to monitor after resource changes

Always observe before and after any change.

---

## Operational Discipline Reminder

Before changing resource allocations:

1. Capture current configuration
2. Confirm environment (dev/test/prod)
3. Understand workload behavior
4. Monitor after deployment
5. Document the change

In regulated environments, resource adjustments should be deliberate and traceable.

---

## Optional Cleanup

If you reduced resource limits for testing:

- Restore previous resource values
- Confirm rollout completes successfully
- Verify pod stability

Never leave lab configurations in production environments.
