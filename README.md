# DevOps-Learning-Terraform
Terraform conetnt that i will go through and document 
<img width="550" height="306" alt="image" src="https://github.com/user-attachments/assets/dcac365f-750f-4c3f-914d-bd1182baac53" />

Infrastructure as code
DevOps engineer writes code on terraform terraform code gets deployed to the cloud
terraform is cloud agnostic (works with any cloud deployes to any cloud)
teraform can be used to deploy kubernetes resources
terraform can deploy certainm things to vault 
Terraform uses its regestry to install certain plugins, different API calls to deploy to different providers
<img width="690" height="187" alt="image" src="https://github.com/user-attachments/assets/c8815260-2006-4d28-9cf7-58e7937619ef" />

IaC with Version control
'you can use terraform with version control to save changes, roll back changed and vcollaberate with team mates 
when code is pushed its managed by the teraform state file and th eterafform lock file
<img width="688" height="372" alt="image" src="https://github.com/user-attachments/assets/d2c2c8ad-6dec-40b4-80b7-04dcd2763a94" />

Infra Orchestration vs Config Management
1. Configuration Management (CM)

Think of this as making sure machines stay in the right state.

Tools: Ansible, Puppet, Chef, SaltStack

Purpose: Install software, manage files, set system settings, apply patches.

Analogy: Like a housekeeper who ensures every room has the right furniture, lights, and temperature, no matter what.

Example:

Ensure every server in your web cluster has Nginx installed, port 80 open, and the right config file.

2. Infrastructure Orchestration (IO)

This is coordinating and provisioning entire environments.

Tools: Terraform, CloudFormation, Pulumi

Purpose: Create and manage infrastructure resources (VMs, networks, load balancers, storage).

Analogy: Like an architect + construction crew who can build the whole building from scratch (servers, networks, firewalls) before the housekeeper steps in.

Example:

Provision a VPC, load balancer, and 3 EC2 instances in AWS.

Key Difference

CM = What’s inside the machine (software, settings).

IO = The machines themselves and how they connect.
<img width="673" height="353" alt="image" src="https://github.com/user-attachments/assets/0b61cd10-3987-411d-934f-a80b53ac9ae5" />


What is Terraform?
Starts with a practicioner / developer 
he creates the IAC and deploys it 
he then runs a plan the plan compares the codes state to the cloud and then tried to match what is on the code
then you apply once that plan is good to go 
then it deploys to the cloud  
<img width="675" height="364" alt="image" src="https://github.com/user-attachments/assets/6bd64d69-6e84-41fc-9179-43d96573f19a" />

Tips for terraform
Get hands on with the documentation 
Get hands on with the Terraform Registiry 
you can find documentation for different providers 
Test and validate your terrafrom code
in a production environment you dont wanna break anything
Start with a small MVP minimum viable product then itterate
(configrure the resource you need by deploying into the cloud then itterate later on)
Impliment DRY dont repeat yoru self software engineering principles 





























































































































