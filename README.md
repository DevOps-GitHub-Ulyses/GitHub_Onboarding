# GitHub_Onboarding
This repository is meant to facilitate onboarding to GitHub DevOps Practices


	• Setup GitHub Organization to support Terraform deployments
		○ GitHub.com: select profile bubble, Settings, Organizations, and then New Organization. *Do not select, "Turn <PROFILE> into an organization."
	• Setup VS Code to connect to GitHub:
	    ○ Install VS Code
	    ○ Install Git (Next through the defaults)
	    ○ Sign into GitHub via VS Code:
	      • Select the Account Icon
	      • Select Turn on edit sessions
	      • Sign in with GitHub
	      • Allow each dialog box that requests permissions
	• Configure Azure subscription
		○ Ensure you have access to an Azure subscription with either Owner or Contributor + User Access Administrator
	• Homework
		○ Create a branch from main in VS Code from the forked repository
		○ Install LATEST AZ PowerShell Modules
			§ Reminder: Set-ExecutionPolicy Bypass
			§ Install-Module Az.Accounts, Az.Resources, Az.Storage -Force
	
	• Implement Terraform Prerequisites (Day 1 Continued)
		• Create GH PAT (Classic) for authenticating Environment & Secrets generation
			○ https://github.com/settings/tokens
			○ Repo rights
			○ Copy the generated token for using in the bootstrap script later
				§ Don't commit the script with the token in it!
		• Learn how to implement Terraform Remote Backend
			○ https://developer.hashicorp.com/terraform/language/settings/backends/azurerm
			○ az-tf-gh-bootcamp/dev-azure-bootcamp at main · jrybergDemo/az-tf-gh-bootcamp (github.com)
		• Run the bootstrap script
			○ Install PSSodium: Install-Module PSSodium
				§ Might need to download the Sodium.Core package
					□ Register-PackageSource -Location 'https://www.nuget.org/api/v2' -name 'nuget.org' -Trusted -ProviderName NuGet
					□ Install-Package Sodium.Core
			○ Authenticate to Azure: Connect-AzAccount
			○ Update the script variables with
				§ Azure resource location
				§ Terraform backend Storage Account name
				§ AAD Service Principal name
				§ GitHub username
				§ GitHub PAT
				§ GitHub Organization Name
			○ https://github.com/jrybergDemo/az-tf-gh/blob/main/bootstrap-remote-backend.ps1
		• Homework
			○ Confirm Terraform backend resources are in place
			○ Confirm the GitHub Environment and Secrets are in place
			○ Review the Learning Matrix OneNote
	• Deploy Azure resources using Terraform (Day 2)
		• Working session to add Bastion, a Virtual Machine, Storage Account w/Private Endpoint, and supporting resources to the TF config
			○ https://learn.microsoft.com/en-us/azure/private-link/tutorial-private-endpoint-storage-portal
			○ Review the workflow execution
			○ Establish the tfstate file with the single resource group first, then begin adding resources
			○ Some resources are separate in terraform vs deployed together in the portal (e.g. private endpoint)
		• Homework
			○ Complete the config, solution to be revealed next session
	• Solution Reveal & Advanced Topics (Day 3)
		• Data structures
		• Looping
		• Avoiding pitfalls while using Terraform (Rantings)
			○ Different configurations for different environments is a future disaster
			○ Minimize data silos & keep it together
				§ Be careful of naming/concatenation and rolling changes e.g. vm nic name based on vm name
			○ DON'T TOUCH PROD
				§ If for no other reason than to reduce personal culpability when disaster strikes
				§ Inevitably leads to issues with TF state - will need to either import or destroy and recreate
			○ Always make changes to the configs in the lowest environment and promote
				§ Constant temptation to tweak the PROD configs, which will result in future disaster
				§ Pulling changes from release into lower environments is MESSSSSY!
				§ This is why you need to make your pipelines easy to run and consistent

## Git Source Control

Source control management is an integral part of infrastructure as code. A working knowledge of git branching, merging, committing, etc is required to maintain code integrity and change auditing, especially on larger projects. Proper release management is fundamental to keeping production systems online without unscheduled interruptions. 

Learning Resources:
Name	Link	Description	Level
Git Book	https://git-scm.com/book/en/v2/	The source of truth for source control - everything you need to learn about git, but also a bunch of low level knowledge that isn't necessary to simple source control management	300
Everyday Git	https://git-scm.com/docs/giteveryday	A cheat sheet of the most frequently used commands	200
GitHub Flow	https://docs.github.com/en/get-started/quickstart/github-flow	GitHub's advice on how to use their product.	200
GitHub and VS Code	https://learn.microsoft.com/en-us/training/modules/introduction-to-github-visual-studio-code/	Learning module (22 Minutes) to integrate GitHub with VS Code to streamline source control operations from your IDE.	100
GitHub Branch Protection Rules	https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule	An overview of all the settings available for protecting branches (like main/root) from directly merging commits, requiring a pull request instead.	200
GitHub Git Cheat Sheet	https://training.github.com/downloads/github-git-cheat-sheet/	GitHub's version of a git cheat sheet	200
GitHub Administration	https://learn.microsoft.com/en-us/users/githubtraining/collections/mom7u1gzjdxw03	A learning module to dive deeply into GitHub administration, including secrets management and enterprise/organizational support.	400

# Agile

Most modern development teams follow an agile approach to developing infrastructure as code, which includes iterative work over a defined period of time. A working knowledge of the concepts of agile methodologies is necessary to be successful on a development team.

Learning Resources:
Name	Link	Description	Level
Agile 101	https://www.agilealliance.org/agile101/	A general overview of the Agile methodology. Ensure to read the manifesto and principles pages as well	100
What is Agile?	https://www.pmi.org/disciplined-agile/agile/whatisagile	Includes a video overview of what Agile means practically.	100
Plan Efficient Workloads	https://learn.microsoft.com/en-us/devops/plan/planning-efficient-workloads-with-devops	Microsoft's perspective on Agile. After reading the Introduction page, follow the related links in the navigation pane	200

# Orchestration

Orchestration is the 'glue' that connects your code in source control with cloud resources through automated deployments. There are several tools available when it comes to orchestrating cloud deployments, but most modern Azure IaC solutions use Bicep or Terraform.

Learning Resources:
Name	Link	Description	Level
IaC Tools Comparison	https://techcommunity.microsoft.com/t5/itops-talk-blog/infrastructure-as-code-iac-comparing-the-tools/ba-p/3205045	A comparison of many of the orchestration tools available, with pros/cons and further links	200
What is Terraform?	https://learn.microsoft.com/en-us/azure/developer/terraform/overview	An overview of Terraform and the Azure-related providers.	100
Terraform Intro	https://www.terraform.io/intro	Hashicorp's overview of Terraform, with many supporting links in the navigation pane. Ignore the Terraform Cloud materials.	200
Terraform 'What the Hack'	https://microsoft.github.io/WhatTheHack/012-InfraAsCode-Terraform	Challenge yourself to learn Terraform based on a list of requirements.	300
Terraform Azure Remote Backend	https://developer.hashicorp.com/terraform/language/settings/backends/azurerm	How to configure Terraform Azure provider to store its state remotely in an Azure Storage Account	300
Source code for Terraform Azurerm provider	https://github.com/hashicorp/terraform-provider-azurerm	Source code for the AzureRM provider	400
Connect to multiple Azure subscriptions with Terraform	https://developer.hashicorp.com/terraform/language/providers/configuration#alias-multiple-provider-configurations	A brief description of how to implement Terraform configurations across Azure subscriptions.	300
What is Bicep?	https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep	An overview of the Bicep DSL, including many links and examples.	100
Fundamentals of Bicep	Fundamentals of Bicep - Training | Microsoft Learn	Fundamental training path to learning bicep  	100
Intermediate	Intermediate Bicep - Training | Microsoft Learn	Intermediate training path to learning bicep  	200
Bicep		
Advanced Bicep	Advanced Bicep - Training | Microsoft Learn	Advanced training path to learning bicep  	300
		
Deploy Azure resources by using Bicep and GitHub Actions	Deploy Azure resources by using Bicep and GitHub Actions - Training | Microsoft Learn	Learn how to deploy azure resources using Bicep and Github Actions	200

# CLI and PowerShell

Even with an orchestration tool, some tasks require an additional set of tools. The AZ cli and the AZ PowerShell Modules provide (nearly) the same functionality and both (mostly) provide cross-platform support. Be careful not to use these tools to deploy resources, but use them to pull resource info, start VMs, and other administrative tasks during your pipeline runs as needed (or when troubleshooting deployment or resource failures). Ultimately, in making a decision between the tools, if you prefer json output, use AZ cli, otherwise, if you prefer working with PowerShell objects use the PowerShell modules. If you still don't know which tool is right, choose the AZ cli as it has fewer prerequisites (can be run without installing PowerShell on *nix platforms).

Learning Resources:
Name	Link	Description	Level
Choose your tool	https://learn.microsoft.com/en-us/cli/azure/choose-the-right-azure-command-line-tool	Provides a comparison of AZ cli and the PowerShell modules and links to each tool's overview pages	100
AZ CLI Reference	https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest	Contains references to all the AZ cli plugins and resource references	300
AZ PS Module Reference	https://learn.microsoft.com/en-us/powershell/module/?view=azps-9.0.0	Reference for all AZ PS cmdlets. Can search for individual cmdlets, or click a specific module for its cmdlets	300

# Pipelines

Pipelines are the automated activities that take place after defined triggers are activated. These triggers can be a variety of events, but are most commonly commits to pull requests, merges to the main branch, or commits to feature branches. These automated activities can be nearly limitless, and include staging files for Terraform execution, running automated tests, and triggering other pipelines. Continuous Integration & Continuous Deployment (CI/CD) pipelines are meant to keep updates to infrastructure small in scope and constant in delivery.

Learning Resources:
Name	Link	Description	Level
About continuous integration	https://docs.github.com/en/actions/automating-builds-and-tests/about-continuous-integration	Quick overview of Continuous Integration (CI) with a closer, brief look at CI with GitHub Actions	100
Understand GitHub Actions	https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions	Detailed overview of the working pieces that make up GitHub Actions	100
Deploy Azure resources by using Bicep and GitHub Actions	Deploy Azure resources by using Bicep and GitHub Actions - Training | Microsoft Learn	Deploy resources into Azure using Bicep, YAML pipelines, and Github Actions	300

Deploy Azure resources by using Bicep and Azure Pipelines	Deploy Azure resources by using Bicep and Azure Pipelines - Training | Microsoft Learn	Deploy resources into Azure using Bicep and Azure pipelines	300

# Azure Resources

Working with cloud infrastructure is a constant effort of learning a constant stream of new services, APIs, and attributes. It's impossible to remember them all, so it is important to have the references handy when deploying a new type of resource.

Learning Resources:
Name	Link	Description	Level
Terraform Azure Provider	https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs	Reference documentation for Terraform Azure provider (AzureRM).	300
Azure resource API reference	https://learn.microsoft.com/en-us/azure/templates/	Reference list for all Azure resources with Bicep and Terraform examples. Note that the Terraform examples all use the AzAPI provider instead of the AzureRM provider.	400
Azure resource Documenatation	https://learn.microsoft.com/en-us/azure/?product=all	Documentation for all Azure resources.	400

# Identity

Although a comprehensive working knowledge of Azure Active Directory (AAD) is unnecessary to understand IaC authentication methods, it is good to have a general working knowledge of how AAD objects are created and managed for a more holistic picture of the solution.

Learning Resources:
Name	Link	Description	Level
Authenticating Terraform to Azure	https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/service_principal_oidc	Detailed description of how to create the Azure AD Service Principal and OIDC federated credentials.	300
Azure Login GitHub Action	https://github.com/marketplace/actions/azure-login	Overview of how to use this GitHub Action in a workflow to authenticate to Azure. Includes how to create the service principal and a variety of credentials.	300
App & Service Principals in AAD	https://learn.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals	Detailed overview of the AAD objects used to authenticate connections to Azure resources	400
Connect GitHub Actions to Azure	https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure	Learn how to create a Service Principal with OIDC federated credentials to authenticate a GitHub repository without secrets.	400
Configure GitHub to connect to Azure with OIDC	https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure	A more truncated overview of the Azure published guidance, focuses on how to configure the GitHub Actions workflow to use OIDC federated credentials to connect to Azure.	300

# Data Structures

Data structures are an integral part of any development work. Proper IaC configurations begin with proper data structures to increase efficiencies, reduce code, and reduce stress.

Learning Resources:
Name	Link	Description	Level
Terraform Data Types	https://developer.hashicorp.com/terraform/language/expressions/types	The data types available in Terraform	300
Terraform For Each	https://developer.hashicorp.com/terraform/language/meta-arguments/for_each	How to use a single Terraform resource block to manage multiple similar resources	300
Terraform Expressions	https://developer.hashicorp.com/terraform/language/expressions	A list of the variety of expressions and syntax available in Terraform	300
Flatten nested objects	https://developer.hashicorp.com/terraform/language/functions/flatten	An approach to how Terraform can loop through nested objects	400
Bicep Data Types	https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/data-types	The data types available in Bicep	300

