# Lab 09 – Day 2 Operational Readiness

## Objective

Develop a structured approach to managing MAS workloads in steady-state operations (Day 2).

This lab focuses on:

- Change awareness
- Safe rollout observation
- Post-change validation
- Ongoing operational hygiene
- Audit-ready documentation practices

This lab assumes:

- MAS is already deployed
- You are operating within an established environment
- Changes are controlled and authorized

Estimated time: 30–45 minutes

---

## What is Day 2?

Day 1 is installation.

Day 2 is everything that follows:

- Monitoring
- Scaling
- Updating
- Troubleshooting
- Validating stability
- Preparing for audits
- Supporting users

Most operational risk occurs during Day 2.

Discipline reduces that risk.

---

# Structured Day 2 Change Workflow

Before making any change:

1. Confirm project and environment
2. Capture current state
3. Understand blast radius
4. Communicate if required
5. Proceed deliberately
6. Validate after change
7. Document outcome

---

## Step 1 – Capture Baseline State

Select a MAS deployment.

Record:

- Project name
- Deployment name
- Replica count
- Pod names
- Restart counts
- CPU request
- Memory limit
- Active Route
- Timestamp

This baseline allows you to detect unintended changes.

---

## Step 2 – Observe Before Change

Before modifying:

1. Review **Events**
2. Review **Logs**
3. Review **Metrics**
4. Confirm no active degradation

Never layer a new change onto an unstable system.

---

## Step 3 – Perform a Controlled Change (Non-Production Recommended)

In a non-production project:

- Scale replicas up or down
- Perform a rollout restart
- Adjust resource limits (if authorized)

Observe:

- Rollout progress
- Pod recreation
- Route stability

Do not perform changes in production without change control approval.

---

## Step 4 – Validate After Change

After change:

1. Confirm all replicas are available
2. Confirm restart counts are stable
3. Confirm Route accessibility
4. Confirm logs show clean startup
5. Confirm no new warning events

Validation is not optional.

---

## Step 5 – Confirm Storage and Dependencies

For stateful workloads:

- Confirm PVCs remain Bound
- Confirm no volume errors
- Confirm dependent services are reachable

Day 2 failures often occur in dependencies, not the primary workload.

---

# Ongoing Operational Hygiene

On a regular cadence:

- Review restart counts
- Review resource usage trends
- Review warning events
- Confirm Route TLS validity (if applicable)
- Review quota consumption

Small anomalies often precede larger failures.

---

# Audit-Ready Documentation

In regulated environments, be prepared to answer:

- What changed?
- When did it change?
- Who approved it?
- What was the impact?
- How was validation performed?

Maintaining structured records simplifies compliance reviews.

---

# What You Learned

You should now understand:

- How to prepare for controlled changes
- How to validate rollout behavior
- How to monitor stability post-change
- How to document operational decisions
- How to operate MAS workloads responsibly

Day 2 discipline preserves mission stability.

---

# Common Mistakes

- Making changes without baseline capture
- Restarting workloads to “see if it fixes it”
- Ignoring dependency health
- Failing to validate after change
- Treating non-production and production identically

Maturity is demonstrated through restraint and structure.

---

# Operational Discipline Reminder

In live environments:

- Observe first
- Change deliberately
- Validate thoroughly
- Document clearly

Operational confidence comes from repeatable structure.
