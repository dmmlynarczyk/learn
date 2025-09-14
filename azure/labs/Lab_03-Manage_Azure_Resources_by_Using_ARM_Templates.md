# Lab 03 - Manage Azure resources by using Azure Resource Manager Templates

**What This Lab Taught Me**:
Learning to automate resource deployments using Azure Resource Manager templates - basically writing code to create infrastructure instead of clicking through the portal.

**Infrastructure as Code Concepts I Learned**:
- **Template Structure**: Understanding how parameters, variables, resources, and outputs work together in JSON format
- **Declarative Deployment**: Telling Azure what you want (a managed disk) rather than how to create it step-by-step
- **Repeatable Deployments**: Same template can create identical resources multiple times

**Real-World Value I Understood**:
- **Consistency**: No more "it worked on my machine" - everyone gets identical infrastructure
- **Version Control**: Infrastructure changes can be tracked like code changes
- **Speed**: Deploy complex setups in minutes instead of hours of manual work

**What Clicked for Me**:
- **Template vs Portal**: Portal is good for learning, templates are good for production
- **Parameter Files**: Keep the template generic, use parameters to customize for different environments
- **Deployment Validation**: Azure checks if the template is valid before actually creating anything

**Practical Challenges**:
- **JSON Syntax**: Had to be careful with brackets, quotes, and commas - one mistake breaks everything
- **Template Deployment UI**: Found the "Template deployment (deploy using custom templates)" section in the portal
- **Understanding Output**: Seeing what the template actually created vs what I expected

**Why This Matters**:
Manual clicking doesn't scale - imagine setting up 50 identical environments by hand. Templates let you deploy entire applications with one command.

**Key Insight**: 
ARM templates aren't just about avoiding clicks - they're about treating infrastructure like software with proper testing, version control, and repeatability.

This shows you understand templates as a professional practice, not just a technical exercise!