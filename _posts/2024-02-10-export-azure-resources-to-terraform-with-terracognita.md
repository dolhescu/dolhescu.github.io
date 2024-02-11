---
title: Export Your Azure Resources to Terraform with Terracognita
date: 2024-02-11 18:00
categories: [Tech, DevOps]
tags: [terraform, tooling, IaC]
---

## Context
Hosting your web application system on the cloud is fantastic. It provides a great deal of flexibility, and depending on the payment model, you only pay for the resources you actually use. Are you aware that a period with lower usage is approaching? You can scale down all components to minimize costs during this time.

> Without a central source of truth, unintended changes to the infrastructure may occur.
{: .prompt-warning }

We're all familiar with the narrative. You commence with a modest application, revel in your accomplishments, and before you know it, the entire ecosystem becomes overly intricate. A diverse team, spanning from DevOps and developers to project managers, accesses the Azure Portal (or any cloud provider you've selected), altering databases, virtual machines, Kubernetes clusters, and more according to their requirements. It's easy to overlook changes, and with no centralized source of truth, everyone has the autonomy to modify the infrastructure. This can lead to unintended consequences, such as incurring unnecessary costs simply because someone forgot about certain resources still running in the cloud.

> Infrastructure as Code encourages collaboration and teamwork.
{: .prompt-tip }

Why not set up a system where any changes to the infrastructure go through a review process, just like we do with new features using repositories and branches? The answer lies in a powerful tool called Infrastructure as Code (IaC), with Terraform doing an excellent job in this area. Terraform is great because it easily works with different cloud providers, making your infrastructure more flexible. If there's a need for a major change in the provider later on, the whole process can be smoother. However, the most important benefit of IaC is that it encourages collaboration and teamwork.

## Scenario: Azure infrastructure without IaC

In this article, we'll explore a specific scenario where your infrastructure is already on Azure, but lacks Infrastructure as Code (IaC). Updates are currently handled manually through the Azure Portal, Azure CLI, or perhaps Azure Templates (Microsoft's IaC). Now, you aim to harness the benefits of Terraform and its versatile IaC capabilities. How do you transition all your infrastructure into Terraform? While you could do this manually, dealing with a complex production infrastructure would be quite a challenge. The good news is, there are tools to make this job easier. I'll mention a few: Terracognita, Terraformer, and the one in the title, Aztfexport. This post will focus on exploring what Terracognita can do.

## Solution: Utilizing Terracognita to export Azure resources into Terraform
Terracognita is open-source software designed to efficiently and automatically generate Terraform scripts from your manually-provisioned resources. Currently, Terracognita supports importing from various cloud providers, including AWS, GCP, AzureRM, and VMware vSphere, translating them into Terraform.
### Prerequisites
To proceed, ensure the following prerequisites are met:
* A Microsoft Azure account with existing infrastructure
* Azure CLI installed and configured on your machine (In this case, using Mac)
* Terraform installed and configured on your machine (In this case, using Mac)

### Step by step guide
#### Install TerraCognita
To install Terracognita, use the following commands in your terminal:
``` terminal
brew install terracognita
```
To verify the installation and explore available commands, run:

``` terminal
terracognita --help
```

#### Create Azure Service Principal
Terracognita requires a service principal to access Azure resources. Use the following Azure CLI command to create a service principal:
``` terminal
az ad sp create-for-rbac --name myServicePrincipalName
                         --role contributor
                         --scopes /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG1
```
Replace myServicePrincipalName with a suitable name and ensure that the subscription ID and resource group match your specific Azure environment.

Output:

``` terminal
{
  "appId": "myAppId",
  "displayName": "myServicePrincipalName",
  "password": "myServicePrincipalPassword",
  "tenant": "myTentantId"
}
```
Save the output. You'll need the appId, tenant, and password values for configuring Terracognita to securely interact with your Azure resources.

#### Running TerraCognita
Execute the following command in your terminal to run Terracognita:
``` terminal
terracognita azurerm --tenant-id '<myTentantId>'
                     --subscription-id '<00000000-0000-0000-0000-000000000000>' 
                     --tfstate 'terraform.tfstate' 
                     --client-id '<myAppId>' 
                     --client-secret '<myServicePrincipalPassword>' 
                     --resource-group-name '<myRG1>' 
                     --hcl <output path, eg ./terracognita/> 
```
Adjust the placeholder values with your actual Azure information. This command runs Terracognita and generates Terraform scripts representing your Azure resources. The output is stored in the provided HCL format in the specified directory.

Once you run the Terracognita command, it will take some time to process. Afterward, you'll find a folder called "terracognita", and inside, there are files with a ".tf" extension.

#### Validation
To confirm the accuracy of the infrastructure snapshot, navigate to the "terracognita" directory and execute `terraform init` followed by `terraform plan`. If the auto-generated code accurately represent your existing Azure resources, Terraform should not detect any changes. Depending on your specific setup and requirements, some manual code adjustments may still be necessary.

### Limitations
* The tool lacks comprehensive documentation, making it challenging for users to understand its functionalities thoroughly
* The exporting process can be time-consuming, especially when dealing with policies
* The auto-generated Terraform code may lack accuracy, requiring additional manual adjustments

## Conclusion
Using Infrastructure as Code (IaC) is now a widely recognized best practice. It's a great idea to translate your infrastructure into Terraform, and there are tools to help with that. But remember, these tools have limitations. No tool is perfect; they all have constraints and challenges. While these tools can be useful, it's up to the software engineers to make sure the move to Infrastructure as Code is successful and accurate.