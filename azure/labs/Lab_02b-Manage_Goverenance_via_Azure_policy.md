## Lab 02b - Manage Governance via Azure Policy

**What This Lab Taught Me**:
Learning how to implement Azure Policy to enforce governance, apply resource tagging, and configure resource locks for better resource management and compliance

## Core Governance Concepts I Learned
- **Policy vs Manual Work**: Instead of asking people to tag resources, policies can enforce it automatically
- **Remediation Tasks**: Azure Policy remediation feature brings existing resources into compliance automatically
- **Resource Locks**: How to prevent accidental deletion of critical resources

## Real-World Business Context

Practiced tagging resources for cost tracking and applying policies to ensure compliance - this solves the problem of "shadow IT" where people create resources without proper organization.

## What Clicked for Me
- **Proactive vs Reactive**: Policies prevent problems instead of fixing them after they happen  
- **Scale**: One policy can govern thousands of resources automatically
- **Audit vs Enforce**: Understanding when to block actions vs just report violations

## Practical Challenges I Hit
- **Policy Timing**: Policies don't apply instantly - had to wait to see effects on new resources
- **Scope Selection**: Figuring out whether to apply the policy to subscription, resource group, or individual resources
- **Existing Resources**: Understanding the difference between preventing new violations vs fixing old ones

## Navigation Discovery
- Found Azure Policy has its own dedicated section (not buried in other services)
- Compliance dashboard shows policy violations clearly
- Resource locks are in a different place than I expected (under each resource's settings)

## Why This Matters for Real Jobs
Companies need automatic governance because manual processes don't scale. If you have 100 developers creating resources, you can't rely on them all remembering to tag everything correctly.

## Key Insight
Governance isn't about being controlling - it's about making compliance automatic so teams can focus on building instead of remembering rules.
