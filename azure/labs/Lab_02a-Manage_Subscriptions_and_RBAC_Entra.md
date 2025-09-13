# Lab 02a - Manage Subscriptions and RBAC Entra

**Real-World Context**: 
- *Utilizing RBAC to control what action identities can perform and ease the burden of subscription management.*
- Created a help desk scenario where support staff can create tickets and view resources but can't modify anything - this mirrors actual enterprise setups.

**What I Learned**: Learning how Azure organizes permissions through management groups and how custom roles actually work in practice.

**What I Did**: Create management groups, assign pre-configured and custom roles to groups, and monitored activity log for specific creation activity.

## Key Concepts

> [!NOTE]
> As a best practice always assign roles to groups and not individuals
create a custom RBAC role

- **Management Group Hierarchy**: How management groups organize subscriptions and allow RBAC inheritance - like folders for permissions
- **Custom RBAC Roles**: The difference between built-in roles and creating specific permissions for business needs
- **Permission Testing**: How to verify what a user can actually do vs what they're supposed to do

## Lessons Learned

- **Permission Delays**: Changes didn't show up immediately - had to wait a few minutes
- **Scope Complexity**: Understanding where to assign the role (management group vs subscription) was trickier than expected
- **Testing Process**: Had to actually sign in as the test user to see what they could access - not just assume it worked

## Navigation Learning

- Found the Management Groups section (wasn't obvious where it lived)
- Custom role creation was buried deeper in IAM than I expected
- Activity logs were useful for confirming the role assignments actually worked

## Why This Matters

This isn't just about following steps - it's about understanding how real companies control who can do what in Azure. The help desk scenario is something I'd actually encounter in a job.

## Key Takeaways

RBAC is about giving people exactly the permissions they need for their job, nothing more. The custom role approach prevents the "too many permissions" problem.
