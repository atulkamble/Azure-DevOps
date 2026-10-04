# AZ-400 — Sessions 1–3: Codes, Steps & Points to Remember

## Session 1 — DevOps Foundations

### 1. DevOps Principles & Culture

**DevOps = Development + Operations + Security + Automation + Collaboration**

Core principles:
- Collaboration between Dev, Ops, QA, Security.
- Automate repetitive processes.
- Deliver small changes frequently.
- Get feedback quickly.
- Infrastructure as Code (IaC).
- Continuous testing and monitoring.
- Shift security left.
- Continuous improvement.

Simple flow:

```text
Plan
  ↓
Code
  ↓
Build
  ↓
Test
  ↓
Release
  ↓
Deploy
  ↓
Operate
  ↓
Monitor
  ↓
Feedback
  └────────────→ Plan
```

**Remember:** DevOps is primarily a **culture and set of practices**, not simply a collection of tools.

---

### 2. DevOps Lifecycle + Value Stream

Typical lifecycle:

```text
Plan → Develop → Build → Test → Release → Deploy → Operate → Monitor
```

Azure DevOps mapping:

```text
Plan      → Azure Boards
Code      → Azure Repos
Build     → Azure Pipelines
Test      → Azure Test Plans
Package   → Azure Artifacts
Deploy    → Azure Pipelines
Monitor   → Azure Monitor / Application Insights
```

A **value stream** represents the complete flow from:

```text
Customer Requirement
        ↓
Planning
        ↓
Development
        ↓
Testing
        ↓
Deployment
        ↓
Production
        ↓
Customer Feedback
```

Points to remember:
- Identify delays and bottlenecks.
- Reduce manual handoffs.
- Automate repetitive activities.
- Reduce deployment lead time.
- Increase feedback speed.

---

### 3. CI/CD Concepts

**CI — Continuous Integration**

Developers frequently merge code and automatically run:

```text
Developer
    ↓
Git Push
    ↓
Build
    ↓
Unit Test
    ↓
Code Analysis
    ↓
Artifact
```

**CD — Continuous Delivery/Deployment**

```text
Artifact
   ↓
Dev
   ↓
Test
   ↓
Staging
   ↓
Approval
   ↓
Production
```

Example Azure Pipeline:

```yaml
trigger:
  - main

pool:
  vmImage: ubuntu-latest

steps:
  - script: echo "Starting CI Pipeline"
    displayName: Start Pipeline

  - script: |
      echo "Building application..."
    displayName: Build

  - script: |
      echo "Running tests..."
    displayName: Test

  - script: |
      echo "Pipeline completed"
    displayName: Complete
```

Remember:

```text
CI = Build + Test
CD = Release + Deploy
```

---

### 4. DORA Metrics

Four important metrics:

| Metric | Meaning |
|---|---|
| Deployment Frequency | How frequently production deployments happen |
| Lead Time for Changes | Time from code change to production |
| Change Failure Rate | Percentage of deployments causing failures |
| Time to Restore Service | How quickly service is restored |

Example:

```text
Code Commit:      10:00 AM
Production:       12:00 PM

Lead Time = 2 hours
```

Failure example:

```text
Total deployments = 100
Failed deployments = 5

Change Failure Rate = 5 / 100 × 100
                    = 5%
```

Remember:

```text
Higher Deployment Frequency → Good
Lower Lead Time             → Good
Lower Change Failure Rate   → Good
Lower Restore Time          → Good
```

---

### 5. DevOps Maturity Levels

Simple maturity model:

```text
Level 1
Manual
   ↓
Level 2
Basic Automation
   ↓
Level 3
CI/CD
   ↓
Level 4
Infrastructure as Code
   ↓
Level 5
Platform Engineering / Full Automation
```

**Level 1 — Manual**
- Manual deployment
- Manual infrastructure
- Limited monitoring

**Level 2 — Basic automation**
- Git introduced
- Build scripts
- Some automated testing

**Level 3 — CI/CD**
- Automated pipelines
- Automated testing
- Deployment automation

**Level 4 — Advanced DevOps**
- Terraform/Bicep
- Containers/Kubernetes
- Automated security
- Observability

**Level 5 — Platform Engineering**
- Internal developer platform
- Self-service environments
- Golden paths/templates
- Policy automation

---

### 6. Platform Engineering Overview

Platform engineering builds reusable internal platforms for developers.

```text
Developers
     ↓
Developer Portal
     ↓
Internal Developer Platform
     ↓
--------------------------------
CI/CD | Kubernetes | IaC | Security
--------------------------------
     ↓
Azure / AWS / GCP
```

Examples:
- Predefined pipeline templates
- Terraform modules
- Kubernetes templates
- Self-service environments
- Centralized monitoring
- Secret management

Remember:

```text
DevOps → Culture + Practices

Platform Engineering
→ Provides reusable platforms supporting DevOps
```

---

### 7. DevOps Toolchain

```text
Planning        → Azure Boards / Jira

Source Control  → Git / GitHub / Azure Repos

Build           → Maven / Gradle / npm

CI/CD           → Azure Pipelines / GitHub Actions / Jenkins

Containers      → Docker

Orchestration   → Kubernetes / AKS

IaC             → Terraform / Bicep

Configuration   → Ansible

Security        → Defender / SonarQube / Trivy

Monitoring      → Azure Monitor / Prometheus / Grafana
```

Typical toolchain:

```text
Developer
   ↓
Git
   ↓
GitHub / Azure Repos
   ↓
Azure Pipeline
   ↓
SonarQube
   ↓
Docker
   ↓
ACR
   ↓
AKS
   ↓
Azure Monitor
```

---

### 8. AZ-400 Exam Overview

Focus your preparation on:
- Source control
- Git strategy
- CI/CD
- Azure Pipelines
- GitHub Actions
- Security
- Package management
- Infrastructure as Code
- Monitoring
- Feedback
- Azure DevOps
- GitHub

Important exam idea:

```text
Plan
↓
Source Control
↓
CI
↓
Artifact
↓
CD
↓
Infrastructure
↓
Security
↓
Monitoring
↓
Feedback
```

---

# Session 2 — Azure DevOps Platform

## 1. Azure DevOps Services Overview

Main Azure DevOps services:

```text
Azure DevOps
│
├── Boards
├── Repos
├── Pipelines
├── Test Plans
└── Artifacts
```

| Service | Purpose |
|---|---|
| Boards | Work/project tracking |
| Repos | Git repositories |
| Pipelines | CI/CD |
| Test Plans | Testing |
| Artifacts | Package management |

---

## 2. Organization & Project Setup

Structure:

```text
Azure DevOps Organization
        ↓
      Project
        ↓
--------------------------------
Boards | Repos | Pipelines | Artifacts
--------------------------------
```

Portal steps:

```text
1. Open Azure DevOps
2. Create Organization
3. Create Project
4. Select Visibility
5. Open Repos
6. Initialize Repository
7. Create Pipeline
```

Azure DevOps CLI extension:

```bash
az extension add --name azure-devops
```

Update:

```bash
az extension update --name azure-devops
```

Login:

```bash
az devops login
```

Configure defaults:

```bash
az devops configure --defaults \
organization=https://dev.azure.com/cloudnautic \
project=project
```

Verify:

```bash
az devops project list --output table
```

Create project example:

```bash
az devops project create \
  --name demo-project \
  --visibility private
```

---

## 3. Azure DevOps vs GitHub

| Feature | Azure DevOps | GitHub |
|---|---|---|
| Git | Azure Repos | GitHub Repositories |
| CI/CD | Azure Pipelines | GitHub Actions |
| Planning | Azure Boards | GitHub Issues/Projects |
| Packages | Azure Artifacts | GitHub Packages |
| Enterprise DevOps | Strong | Strong |
| Open-source ecosystem | Supported | Very strong |

Concept mapping:

```text
Azure Repos      ↔ GitHub Repositories
Azure Pipelines  ↔ GitHub Actions
Azure Boards     ↔ GitHub Issues/Projects
Azure Artifacts  ↔ GitHub Packages
```

---

## 4. Service Connections

Purpose:

```text
Azure DevOps Pipeline
        ↓
Service Connection
        ↓
External Resource
```

Examples:

```text
Azure DevOps → Azure
Azure DevOps → Docker Registry
Azure DevOps → Kubernetes
Azure DevOps → GitHub
```

Portal:

```text
Project Settings
      ↓
Service Connections
      ↓
New Service Connection
      ↓
Choose Resource Type
      ↓
Configure Authentication
      ↓
Save
```

Pipeline example:

```yaml
steps:

- task: AzureCLI@2
  inputs:
    azureSubscription: 'azure-service-connection'
    scriptType: bash
    scriptLocation: inlineScript
    inlineScript: |
      az account show
      az group list --output table
```

Points to remember:
- Don't put passwords directly in YAML.
- Prefer workload identity federation or managed identities where supported.
- Restrict permissions.
- Avoid granting access to all pipelines unless required.

---

## 5. DevOps Navigation

Important locations:

```text
Organization Settings
│
├── Users
├── Billing
├── Permissions
└── Agent Pools

Project Settings
│
├── Teams
├── Repositories
├── Pipelines
├── Service Connections
└── Permissions
```

Main project menu:

```text
Overview
Boards
Repos
Pipelines
Test Plans
Artifacts
Project Settings
```

---

## 6. Access Levels & Licensing

Common access concepts:

```text
Organization
   ↓
Users
   ↓
Access Level
   ↓
Security Group
   ↓
Permissions
```

Typical groups:
- Project Administrators
- Contributors
- Readers
- Build Administrators
- Release Administrators

Remember:

```text
Access Level ≠ Permission
```

Access level controls available product features, while permissions determine what the identity can actually do.

---

## 7. Integration Overview

Typical integration:

```text
Developer
   ↓
GitHub / Azure Repos
   ↓
Azure Pipelines
   ↓
SonarQube
   ↓
Docker
   ↓
Azure Container Registry
   ↓
AKS
   ↓
Azure Monitor
```

Other integrations:
- Terraform
- Kubernetes
- Docker Hub
- Azure Key Vault
- Microsoft Teams
- Slack
- Jenkins
- GitHub

---

## 8. DevOps Best Practices

Remember these:

```text
✓ Everything in Git
✓ Use Pull Requests
✓ Protect main branch
✓ Automate builds
✓ Automate testing
✓ Use IaC
✓ Store secrets securely
✓ Use service connections
✓ Scan dependencies
✓ Scan container images
✓ Monitor production
✓ Use least privilege
✓ Implement approvals where necessary
```

Recommended branching:

```text
main
 ↑
Pull Request
 ↑
feature/login
```

Avoid:

```text
Developer → Direct Push → main
```

Prefer:

```text
Developer
   ↓
Feature Branch
   ↓
Pull Request
   ↓
Review
   ↓
Automated Tests
   ↓
Merge
```

---

# Session 3 — Identity & Access

## 1. Microsoft Entra ID

Microsoft Entra ID provides cloud identity and access management.

```text
User / Application
        ↓
Microsoft Entra ID
        ↓
Authentication
        ↓
Authorization
        ↓
Azure Resource
```

Important concepts:
- Users
- Groups
- Applications
- Service principals
- Managed identities
- MFA
- Conditional Access
- RBAC

Remember:

```text
Authentication = Who are you?

Authorization = What can you do?
```

---

## 2. RBAC — Azure + DevOps

Azure RBAC structure:

```text
Security Principal
       +
Role
       +
Scope
       =
Role Assignment
```

Scope hierarchy:

```text
Management Group
      ↓
Subscription
      ↓
Resource Group
      ↓
Resource
```

Common roles:

```text
Owner
Contributor
Reader
User Access Administrator
```

View role assignments:

```bash
az role assignment list --output table
```

View roles:

```bash
az role definition list \
  --query "[].roleName" \
  --output table
```

Example assignment:

```bash
az role assignment create \
  --assignee USER_OR_OBJECT_ID \
  --role Reader \
  --scope /subscriptions/SUBSCRIPTION_ID/resourceGroups/myRG
```

Remember:

```text
Assign permissions at the smallest practical scope.
```

---

## 3. Managed Identity

Managed identity eliminates the need to manually manage application credentials.

```text
Azure VM / App Service
        ↓
Managed Identity
        ↓
Microsoft Entra ID
        ↓
Access Token
        ↓
Key Vault / Storage / SQL
```

Types:

```text
System Assigned
User Assigned
```

Enable VM system-assigned identity:

```bash
az vm identity assign \
  --resource-group myRG \
  --name myVM
```

Check:

```bash
az vm identity show \
  --resource-group myRG \
  --name myVM
```

Remember:

```text
Managed Identity
→ No password stored in application
→ Azure manages underlying credentials
```

---

## 4. Service Principals

A service principal is an identity used by an application or automation.

Concept:

```text
Pipeline
   ↓
Service Principal
   ↓
Microsoft Entra ID
   ↓
Azure RBAC
   ↓
Azure Resources
```

Create example:

```bash
az ad sp create-for-rbac \
  --name demo-devops-sp \
  --role Contributor \
  --scopes /subscriptions/SUBSCRIPTION_ID/resourceGroups/myRG
```

For training/labs, understand that the returned credential is sensitive and should **not** be committed to Git.

Prefer, where possible:

```text
Workload Identity Federation
instead of
Long-lived Client Secret
```

---

## 5. Secure Service Connections

Preferred architecture:

```text
Azure Pipeline
      ↓
Service Connection
      ↓
Workload Identity Federation
      ↓
Microsoft Entra ID
      ↓
Azure Resource
```

Advantages:
- No long-lived secret.
- Reduced credential-management burden.
- Better security posture.
- Easier credential rotation concerns.

---

## 6. Conditional Access

Conditional Access evaluates signals before allowing access.

```text
User
 ↓
Sign-in
 ↓
Conditional Access
 ↓
Evaluate Conditions
 ↓
Allow / Block / Require MFA
```

Possible signals:
- User/group
- Application
- Location
- Device
- Risk
- Authentication context

Example:

```text
IF

User accesses Azure
from an untrusted condition

THEN

Require MFA
```

Remember:

```text
Conditional Access = IF conditions → THEN access controls
```

---

## 7. Least Privilege Model

Principle:

```text
Give only the permissions required
for only the resources required
for only as long as required.
```

Bad:

```text
Everyone → Owner → Subscription
```

Better:

```text
Pipeline
   ↓
Contributor/Specific Role
   ↓
Specific Resource Group
```

Best practices:
- Avoid unnecessary Owner assignments.
- Use groups instead of assigning users individually where practical.
- Use managed identities.
- Use workload identity federation.
- Review access regularly.
- Remove unused identities.
- Use narrowly scoped custom roles only when built-in roles don't fit.

---

## 8. Access Governance

Access governance manages the lifecycle of permissions.

```text
Request
   ↓
Approval
   ↓
Access Granted
   ↓
Periodic Review
   ↓
Renew / Remove
```

Important technologies/concepts:
- Access Reviews
- Privileged Identity Management (PIM)
- Entitlement Management
- Groups
- RBAC
- Conditional Access

Remember:

```text
Permanent Admin Access
        ↓
Higher Risk

Just-in-Time Privileged Access
        ↓
Lower Risk
```

---

# Sessions 1–3 Final Practice

A useful practical flow is:

```text
1. Create Azure DevOps organization
2. Create project
3. Create Git repository
4. Clone repository
5. Create application
6. Push code
7. Create azure-pipelines.yml
8. Run CI pipeline
9. Create Azure Resource Group
10. Create Service Connection
11. Use secure authentication
12. Assign minimum required RBAC
13. Execute Azure CLI from pipeline
14. Protect main branch
15. Create feature branch
16. Raise Pull Request
17. Review and merge
18. Monitor pipeline results
```

Basic Git practice:

```bash
git clone <repo-url>

cd <repo>

git checkout -b feature/demo

echo "AZ-400 DevOps Practice" > README.md

git add .

git commit -m "Add AZ-400 practice"

git push -u origin feature/demo
```

Then:

```text
feature/demo
      ↓
Pull Request
      ↓
Code Review
      ↓
CI Pipeline
      ↓
Approval
      ↓
main
      ↓
CD Pipeline
      ↓
Azure
```

### Key points to remember

```text
DevOps      = Culture + Automation + Feedback

CI          = Integrate + Build + Test

CD          = Release + Deploy

Git         = Source Control

Azure Repos = Git Hosting

Pipeline    = Automation

RBAC        = Authorization

Entra ID    = Identity

Managed Identity
            = Azure-managed workload identity

Service Principal
            = Application/workload identity in Entra ID

Service Connection
            = Azure DevOps connection to an external system

Key Vault   = Secrets/keys/certificates management

IaC         = Infrastructure defined as code

DORA        = Delivery and operational performance metrics

Least Privilege
            = Minimum required permissions
```
