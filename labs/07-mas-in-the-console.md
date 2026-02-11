# Lab 07 – Navigating MAS in the OpenShift Console

## Objective

Develop confidence locating and interpreting IBM Maximo Application Suite (MAS) components within an existing OpenShift environment.

This lab assumes MAS is already installed and operational.

By the end of this lab, you should be able to:

- Identify MAS-related projects
- Locate MAS application deployments
- Identify MAS routes
- Recognize supporting services and operators
- Safely gather structured information about MAS workloads

Estimated time: 30–45 minutes

---

## Important Context

This curriculum does not focus on installing MAS.

It assumes:

- The environment already exists
- Platform teams have deployed MAS
- Your responsibility is operational awareness

This lab teaches you how to understand and operate within the environment you have — not how to build one from scratch.

---

## Step 1 – Identify MAS Projects

1. In the OpenShift console, navigate to **Projects**.
2. Search for project names associated with MAS.

Common naming patterns may include:

- `mas-`
- `maximo-`
- Environment identifiers (dev, test, prod)

3. Select the primary MAS application project.

### Observe

MAS often spans multiple projects:

- Core platform components
- Application workloads
- Supporting services

### Validate

Confirm you can identify:

- The primary application project
- Any supporting projects

---

## Step 2 – Locate MAS Application Workloads

1. Switch to **Administrator** perspective.
2. Navigate to **Workloads → Deployments**.
3. Review deployment names.

### Observe

MAS applications typically:

- Run multiple deployments
- Include supporting services
- May include StatefulSets for stateful components

### Validate

Select one MAS-related deployment and record:

- Deployment name
- Replica count
- Pod status
- Resource requests and limits

Understanding workload structure reduces troubleshooting guesswork.

---

## Step 3 – Identify MAS Routes

1. Navigate to **Networking → Routes**.
2. Review exposed routes.

Look for:

- Workspace routes
- Application UI routes
- API endpoints (if exposed)

### Observe

Each route maps:

Route → Service → Pod

Click into a route and confirm:

- Target service
- TLS configuration
- Hostname

### Validate

Open a MAS route in a new browser tab (if permitted) and confirm it resolves correctly.

---

## Step 4 – Identify Persistent Storage

1. Navigate to **Storage → PersistentVolumeClaims**.
2. Review PVCs associated with MAS.

### Observe

- Storage class
- Access mode
- Capacity
- Bound status

Stateful components depend on stable storage.

### Validate

Confirm all MAS PVCs are in **Bound** status.

Unbound PVCs indicate a platform-level issue.

---

## Step 5 – Recognize Supporting Operators

1. Navigate to **Operators → Installed Operators**.
2. Identify operators associated with MAS and its dependencies.

Examples may include:

- Database operators
- Messaging operators
- Platform operators

Operators manage lifecycle and health for complex services.

### Important

Do not modify operator resources unless explicitly authorized.

---

## Step 6 – Build a Structured MAS Snapshot

Select one MAS application component and capture:

- Project name
- Deployment name
- Pod name
- Restart count
- Route (if applicable)
- CPU request
- Memory limit
- Associated PVCs

This structured snapshot forms the basis for safe troubleshooting and escalation.

---

## What You Learned

You should now understand:

- MAS is composed of multiple OpenShift workloads
- Routes expose MAS applications
- PVCs support persistence
- Operators manage platform dependencies
- Structured observation is essential in live environments

You do not need to build the platform to operate it effectively.

---

## Common Mistakes

- Attempting configuration changes without understanding workload structure
- Restarting pods without reviewing logs
- Confusing application-level errors with infrastructure failures
- Ignoring persistent storage health

In production environments, interpretation precedes intervention.

---

## Operational Discipline Reminder

When working in live MAS environments:

1. Confirm project
2. Confirm workload
3. Confirm scope
4. Gather structured evidence
5. Escalate when appropriate

Operational maturity is demonstrated through restraint and clarity.
