# Lab 02 – Console Navigation

## Objective

Develop practical confidence navigating the OpenShift web console.

By the end of this lab, you should be able to:

- Switch between Developer and Administrator perspectives  
- Locate workloads quickly  
- View pod logs  
- View events  
- Identify resource usage metrics  
- Understand where to look when something fails  

This lab builds operational fluency without requiring CLI access.

Estimated time: 20–30 minutes

---

## Prerequisites

- Access to an OpenShift cluster running MAS  
- Access to at least one MAS project (namespace)  
- View-level permissions are sufficient  

No CLI access is required.

---

## Step 1 – Understand Perspectives

OpenShift has two primary perspectives:

- **Administrator**
- **Developer**

### Switch Perspectives

1. In the upper-left corner of the console, locate the **Perspective switcher**.
2. Select **Developer**.
3. Observe the navigation menu.
4. Switch back to **Administrator**.
5. Compare the navigation menu again.

### Observe

- Developer view emphasizes Topology and application flows.
- Administrator view exposes infrastructure-level details.

### Validate

You should be comfortable switching between perspectives and understanding when each is appropriate.

---

## Step 2 – Navigate to Your MAS Project

1. In the left navigation, click **Projects**.
2. Select your MAS project.
3. Confirm you are operating within the correct namespace (displayed at the top of the console).

Operating in the wrong project is a common operational mistake.

---

## Step 3 – Locate Workloads Quickly

### Using Topology (Developer View)

1. Switch to **Developer** perspective.
2. Click **Topology**.
3. Identify a MAS component.
4. Click it to view details.

### Using Workloads (Administrator View)

1. Switch to **Administrator** perspective.
2. Navigate to **Workloads → Deployments**.
3. Select a deployment.
4. Review:
   - Replica count  
   - Pod status  
   - Conditions  

### Validate

You should be able to locate the same workload using both perspectives.

---

## Step 4 – View Pod Logs

1. From a deployment, click the **Pods** tab.
2. Select a running pod.
3. Click **Logs**.

### Observe

- Log stream updates in real time.
- You can scroll backward in time.
- Previous logs may be available if the pod restarted.

### Validate

Identify:
- The container name
- The timestamp format
- Any recent informational or warning messages

Logs are your first diagnostic tool.

---

## Step 5 – View Events

1. While viewing the pod, click the **Events** tab.
2. Review recent events.

### Observe

Events often reveal:

- Scheduling failures  
- Image pull issues  
- Resource pressure  
- Restart triggers  

### Validate

Confirm you can distinguish between normal and warning events.

---

## Step 6 – Review Resource Usage Metrics

1. While viewing a pod, select the **Metrics** tab (if monitoring is enabled).
2. Review CPU and memory graphs.

### Observe

- CPU spikes during activity  
- Memory trends over time  
- Potential resource pressure  

### Validate

Confirm you can identify whether the pod appears resource constrained.

---

## Step 7 – Practice Structured Observation

Select one MAS deployment and record the following:

- Project name  
- Deployment name  
- Replica count  
- Pod name  
- Route (if applicable)  
- CPU request  
- Memory limit  

This is not busywork.

This is building operational discipline.

---

## What You Learned

You should now be able to:

- Confidently move between perspectives  
- Locate workloads quickly  
- Inspect logs and events  
- Review resource usage  
- Gather structured information before escalating issues  

Console fluency reduces reaction time during incidents.

---

## Common Mistakes

- Operating in the wrong project  
- Restarting pods without checking logs  
- Ignoring events  
- Confusing deployments with pods  
- Misinterpreting CPU spikes as failures  

Careful observation precedes action.

---

## Operational Discipline Reminder

In regulated environments, every change should be deliberate.

Before making changes:

1. Observe  
2. Capture details  
3. Confirm scope  
4. Communicate if necessary  

Precision prevents unnecessary disruption.
