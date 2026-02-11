# Lab 06 – Observability and Diagnostics

## Objective

Develop a structured, console-based troubleshooting workflow for diagnosing application issues in OpenShift.

By the end of this lab, you should be able to:

- Locate and interpret container logs
- Review pod events for failure causes
- Identify restart patterns
- Review rollout history
- Use metrics to identify resource pressure
- Follow a disciplined incident response flow

Estimated time: 30–45 minutes

---

## Prerequisites

- Access to OpenShift web console
- Access to a project with at least one running deployment
- View or Edit permissions

No CLI access is required.

---

## Operational Philosophy

In regulated environments, troubleshooting must be:

1. Structured  
2. Observable  
3. Documented  
4. Reproducible  

Random restarts are not troubleshooting.

Observation precedes action.

This lab teaches a repeatable diagnostic workflow.

---

# Structured Troubleshooting Workflow

When something fails, follow this order:

1. Confirm Project
2. Confirm Deployment
3. Inspect Pod Status
4. Review Events
5. Review Logs
6. Review Metrics
7. Review Rollout History

Never skip steps.

---

## Step 1 – Confirm You Are in the Correct Project

1. In the console header, confirm the active project.
2. If necessary, switch to the correct project.

Operating in the wrong namespace is a common error.

---

## Step 2 – Inspect Deployment Status

1. Switch to **Administrator** perspective.
2. Navigate to **Workloads → Deployments**.
3. Select a deployment.

### Observe

- Replica count
- Available replicas
- Conditions (Available, Progressing, Degraded)

### Validate

Confirm whether the deployment reports a healthy condition.

---

## Step 3 – Inspect Pod Status

1. From the deployment page, click the **Pods** tab.
2. Select a pod.

### Observe

- Pod phase (Running, Pending, CrashLoopBackOff, etc.)
- Restart count
- Container status

### Validate

Record:

- Pod name
- Restart count
- Current state

Restart counts greater than zero require investigation.

---

## Step 4 – Review Events

1. While viewing the pod, click the **Events** tab.

Events often explain failures more clearly than logs.

Common examples:

- FailedScheduling
- OOMKilled
- ImagePullBackOff
- Liveness probe failures

### Validate

Identify:

- Most recent warning event
- Associated timestamp
- Reason code

Events often reveal root cause quickly.

---

## Step 5 – Review Container Logs

1. Click the **Logs** tab.
2. Observe recent output.
3. Scroll to identify:
   - Error messages
   - Stack traces
   - Warning indicators
   - Startup failures

### If the pod restarted

Look for:

- A “previous” log option
- Errors before termination

### Validate

Capture:

- Error snippet (if present)
- Timestamp
- Container name

Logs are evidence — not speculation.

---

## Step 6 – Review Metrics

1. Select the **Metrics** tab.
2. Observe:
   - CPU usage
   - Memory usage

### Look for:

- Memory usage reaching limit
- CPU throttling
- Sudden spikes before restart

### Validate

Determine whether resource pressure likely contributed to failure.

---

## Step 7 – Review Rollout History

1. Navigate back to the deployment.
2. Click **Actions → Rollout History** (if available).

### Observe

- Recent configuration changes
- Image updates
- Restart rollouts

Failures often correlate with recent changes.

### Validate

Identify whether:

- A recent rollout preceded the issue
- The failure began after configuration updates

---

# Practical Exercise – Build an Incident Snapshot

Select a deployment and capture:

- Project name
- Deployment name
- Pod name
- Restart count
- Last warning event
- Recent error log line
- CPU request
- Memory limit

This structured snapshot supports escalation and audit.

---

# Common Failure Patterns

### CrashLoopBackOff
- Application startup failure
- Misconfiguration
- Missing dependency

### OOMKilled
- Memory limit too low
- Reporting workload spike
- Large in-memory object creation

### ImagePullBackOff
- Registry access issue
- Incorrect image reference
- Authentication failure

### FailedScheduling
- Insufficient cluster resources
- Request too large for available nodes

Pattern recognition reduces resolution time.

---

# What You Learned

You should now be able to:

- Follow a disciplined troubleshooting flow
- Distinguish logs from events
- Recognize resource-related failures
- Identify restart patterns
- Correlate rollouts with incidents

Observation is more powerful than reaction.

---

# Common Mistakes

- Restarting pods before reviewing logs
- Ignoring events
- Failing to document findings
- Escalating without evidence
- Changing production configurations without root cause analysis

In regulated systems, discipline is non-negotiable.

---

# Operational Discipline Reminder

Before making changes during an incident:

1. Capture state
2. Confirm scope
3. Review evidence
4. Communicate findings
5. Proceed deliberately

Stability is preserved through structure.
