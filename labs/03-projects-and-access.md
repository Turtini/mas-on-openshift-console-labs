# Lab 03 – Projects and Access

## Objective

Understand how OpenShift projects (namespaces) provide isolation, access control, and operational boundaries.

By the end of this lab, you should be able to:

- Explain what a project (namespace) is
- Create a new project (if permitted)
- Identify your access level
- Understand basic role-based access control (RBAC)
- Recognize why project boundaries protect stability

Estimated time: 25–35 minutes

---

## Prerequisites

- Access to the OpenShift web console
- Permission to view projects
- Permission to create projects (optional; if not permitted, observe an existing project)

No CLI access is required.

---

## Why Projects Matter

In OpenShift, a **Project** is a Kubernetes namespace with additional access controls.

Projects provide:

- Isolation between environments (dev, test, prod)
- Separation between applications
- Controlled access through roles
- Resource boundaries (quotas and limits)

In regulated environments, project discipline prevents accidental cross-environment impact.

---

## Step 1 – Review Existing Projects

1. In the left navigation, select **Projects**.
2. Review the list of available projects.
3. Identify your MAS project.
4. Observe naming conventions (for example: `mas-prod`, `mas-dev`, etc.).

### Observe

- Projects often reflect environment boundaries.
- Access varies by project.
- You may not see all projects in the cluster.

### Validate

Confirm you understand which project supports:
- Production
- Development
- Testing (if applicable)

Operating in the wrong project is one of the most common operational mistakes.

---

## Step 2 – Create a New Project (If Permitted)

If you have permission:

1. Click **Create Project**.
2. Name the project (example):  
   `mas-lab-<yourname>`
3. Optionally add:
   - Display Name
   - Description
4. Click **Create**.

If you do not have permission:
- Observe an existing non-production project instead.

### Validate

Confirm the project appears in your project list and is selected in the console header.

---

## Step 3 – Understand Your Access Level

1. With your project selected, navigate to:
   **Administrator → User Management → RoleBindings**

2. Review role bindings in the project.

Common roles include:

- **View** – Read-only access
- **Edit** – Modify most application resources
- **Admin** – Full project-level control

### Observe

You may see:
- Individual user accounts
- Groups
- Service accounts

### Validate

Identify:
- Your username
- Your assigned role
- Whether your role allows resource modification

If unsure, confirm with your platform administrator before making changes.

---

## Step 4 – Understand Isolation Boundaries

Switch to a different project and observe:

- Workloads do not cross project boundaries.
- Routes are scoped to a project.
- Secrets and ConfigMaps are project-specific.

Projects are security and stability boundaries.

Actions taken in one project do not affect another — unless cluster-level permissions are involved.

---

## Step 5 – Review Resource Controls (If Present)

Within your lab project:

1. Navigate to:
   **Administrator → Administration → ResourceQuotas**
2. Review any defined quotas.

Then navigate to:

**Administrator → Administration → LimitRanges**

### Observe

- CPU and memory caps
- Default limits applied to new pods
- Maximum resource thresholds

### Validate

Confirm whether your project has:
- No quotas
- Defined CPU/memory quotas
- Defined limit ranges

Resource controls protect cluster stability.

---

## Practical Exercise – Safe Verification

In your lab project:

1. Navigate to **Workloads → Deployments**.
2. Confirm whether deployments exist.
3. If the project is new and empty, observe that no workloads are present.

Projects start empty.

Everything deployed must be intentional.

---

## What You Learned

You should now understand:

- Projects isolate applications and environments.
- RBAC determines who can do what.
- Resource controls protect shared infrastructure.
- Access level determines operational authority.
- Precision in project selection prevents disruption.

Projects are not folders — they are boundaries.

---

## Common Mistakes

- Deploying changes in the wrong project
- Assuming access equals authorization
- Ignoring resource quotas
- Editing production projects without change control

In regulated environments, clarity and verification are required before action.

---

## Operational Discipline Reminder

Before making changes in any project:

1. Confirm the project name
2. Confirm your role
3. Confirm environment (dev/test/prod)
4. Capture current state
5. Communicate if required

Structured behavior protects mission systems.
