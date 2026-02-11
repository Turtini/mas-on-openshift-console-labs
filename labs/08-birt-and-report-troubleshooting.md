# Lab 08 – BIRT and Report Troubleshooting in the Console

## Objective

Develop a structured, console-based workflow for diagnosing IBM MAS reporting issues (including BIRT-based reports) in an existing OpenShift environment.

This lab assumes:

- MAS is already installed
- Reporting is already configured
- You are troubleshooting a report execution issue

By the end of this lab, you should be able to:

- Identify reporting-related workloads
- Locate the correct pod for investigation
- Review logs for report execution errors
- Identify resource-related failures
- Verify storage attachments
- Build a structured incident packet for escalation

Estimated time: 40–60 minutes

---

## Important Context

This lab does not cover:

- Installing BIRT
- Configuring reporting engines
- Modifying report templates

This lab focuses on:

Understanding how to interpret reporting behavior in OpenShift when something fails.

In regulated environments, structured observation is more valuable than guesswork.

---

# Structured Report Troubleshooting Workflow

When a report fails:

1. Confirm the namespace
2. Identify the reporting workload
3. Inspect pod status
4. Review events
5. Review logs
6. Review resource usage
7. Confirm storage attachments
8. Build a structured incident summary

Follow this order.

---

## Step 1 – Confirm the Correct MAS Project

1. Navigate to **Projects**.
2. Select the MAS project where reporting runs.
3. Confirm you are in the correct environment (dev/test/prod).

Misidentifying the namespace leads to incorrect conclusions.

---

## Step 2 – Identify Reporting-Related Workloads

1. Switch to **Administrator** perspective.
2. Navigate to **Workloads → Deployments**.
3. Look for deployment names associated with reporting.

Common patterns may include keywords such as:

- `report`
- `birt`
- `rpt`
- `reporting`

If unsure:

- Use the console search bar
- Review deployment descriptions
- Coordinate with your platform administrator

### Validate

Select the most likely reporting deployment.

Confirm:

- Replica count
- Pod status

---

## Step 3 – Inspect Pod Status

1. Click the **Pods** tab within the deployment.
2. Select the most recently running pod.

### Observe

- Restart count
- Current state
- Pod phase

If restart count is greater than zero, further investigation is required.

---

## Step 4 – Review Events

1. Within the pod view, select the **Events** tab.

Look for:

- OOMKilled
- Failed scheduling
- Liveness probe failures
- Permission errors
- Volume mount failures

### Validate

Record:

- Most recent warning event
- Timestamp
- Reason code

Events often reveal infrastructure-level issues.

---

## Step 5 – Review Logs

1. Select the **Logs** tab.
2. Observe recent entries.

Look for:

- Stack traces
- OutOfMemory errors
- Database connectivity errors
- File system permission errors
- Timeout messages
- Rendering exceptions

If the pod recently restarted:

- Check for "previous" logs (if available)
- Scroll upward to identify pre-termination errors

### Validate

Capture:

- Relevant log snippet
- Timestamp
- Container name

Logs provide direct evidence of application behavior.

---

## Step 6 – Review Resource Usage

1. Navigate to the **Metrics** tab.
2. Observe memory and CPU usage.

Reporting workloads often:

- Spike memory during rendering
- Consume high CPU during large dataset processing

If memory usage approaches the limit:

- The container may be terminated
- The report may fail silently from the user perspective

### Validate

Compare:

- Memory usage
- Memory limit

Resource exhaustion is a common report failure cause.

---

## Step 7 – Verify Persistent Storage Attachments

1. From the pod view, locate the **Volumes** section.
2. Identify attached PersistentVolumeClaims.
3. Navigate to **Storage → PersistentVolumeClaims**.
4. Confirm the PVC status is **Bound**.

### Observe

If PVCs are not bound:

- Report output may fail
- Temporary files may not persist
- Application behavior may degrade

Storage integrity is critical for reporting systems.

---

# Build a Structured Incident Packet

When escalating or documenting a report issue, capture:

- Project name
- Deployment name
- Pod name
- Restart count
- Most recent warning event
- Relevant log snippet
- CPU request
- Memory limit
- Observed memory usage
- Associated PVC names
- Timestamp of report execution

This structured packet reduces resolution time and supports audit traceability.

---

# Common Reporting Failure Patterns

### Memory Limit Too Low
- OOMKilled events
- Pod restarts
- Partial rendering

### Database Connectivity Issues
- Authentication errors
- Timeout exceptions
- Connection pool exhaustion

### File System or Volume Issues
- Permission denied errors
- Volume mount failures
- Write errors

### Long-Running Queries
- CPU spikes
- Report timeouts
- Backend service overload

Pattern recognition accelerates resolution.

---

# What You Learned

You should now be able to:

- Identify reporting workloads safely
- Distinguish infrastructure failures from application failures
- Recognize resource-related report failures
- Verify storage health
- Produce structured evidence for escalation

Effective troubleshooting does not require cluster-level access.

It requires disciplined observation.

---

# Operational Discipline Reminder

When working in production reporting environments:

1. Do not restart workloads without reviewing logs.
2. Do not change resource limits without authorization.
3. Capture evidence before escalation.
4. Preserve timestamps and error messages.
5. Document findings clearly.

Operational maturity is demonstrated through clarity, not speed.
