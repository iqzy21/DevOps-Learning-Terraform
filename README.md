# DevOps-Learning-Terraform
Terraform conetnt that i will go through and document 
<img width="550" height="306" alt="image" src="https://github.com/user-attachments/assets/dcac365f-750f-4c3f-914d-bd1182baac53" />

## Infrastructure as code
DevOps engineer writes code on terraform terraform code gets deployed to the cloud
terraform is cloud agnostic (works with any cloud deployes to any cloud)
teraform can be used to deploy kubernetes resources
terraform can deploy certainm things to vault 
Terraform uses its regestry to install certain plugins, different API calls to deploy to different providers
<img width="690" height="187" alt="image" src="https://github.com/user-attachments/assets/c8815260-2006-4d28-9cf7-58e7937619ef" />

## IaC with Version control
'you can use terraform with version control to save changes, roll back changed and vcollaberate with team mates 
when code is pushed its managed by the teraform state file and th eterafform lock file
<img width="688" height="372" alt="image" src="https://github.com/user-attachments/assets/d2c2c8ad-6dec-40b4-80b7-04dcd2763a94" />

## Infra Orchestration vs Config Management
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


## What is Terraform?
Starts with a practicioner / developer 
he creates the IAC and deploys it 
he then runs a plan the plan compares the codes state to the cloud and then tried to match what is on the code
then you apply once that plan is good to go 
then it deploys to the cloud  
<img width="675" height="364" alt="image" src="https://github.com/user-attachments/assets/6bd64d69-6e84-41fc-9179-43d96573f19a" />

##Tips for terraform
Get hands on with the documentation 
Get hands on with the Terraform Registiry 
you can find documentation for different providers 
Test and validate your terrafrom code
in a production environment you dont wanna break anything
Start with a small MVP minimum viable product then itterate
(configrure the resource you need by deploying into the cloud then itterate later on)
Impliment DRY dont repeat yoru self software engineering principles 

## Terraform State File
tarraform statefile is a blue print and record of your exisitng infrastructure 
its an up to date record for your current state 
in terms of terraform idempotency means no matter how may times your run you terraform config 
it will produce the szme resukts and not deploy multiple times
if you make a particular change to the config it will apply that perticular change 
it wont do a whole change 

desired vs current state
currunt state = up to date record of infrastructure e.g deployed 2 ec2 instance shout be in the current terraform state
desired state = my own configuration of potential changes or what i want to deploy 

The terraform state file compares the current state to the desired state 
to check wether there is any chngers 
e.g current state file has 2 ec2 instance and desired state has a 3rd ojne configured 
state file recognises this then deploys the chnage to the current state to match the desired state

desired state= what tyou want to achieve
current state = what exists 

## deploying infrastructure 
how is infrastructure deployed via terrasform?
how are connections established for your deployments 
How do i make sure i deploy things saftley and not break anything 

## Terraform Providers
Terrafrom provider is a plugin that allows you to interact with cloud platform services and other things 

## Terraform Provider Code break down
Terraform { … }
This block is used to configure global settings for Terraform itself.

required_providers { … }
Declares which providers your Terraform configuration depends on.

aws = { … }
This says: “I want to use the AWS provider.” The name aws is the local name you’ll use when writing resources.

Inside this block:

source = "hashicorp/aws"
Tells Terraform where to get the provider. Format:

<NAMESPACE>/<PROVIDER>


Here:

hashicorp → namespace (official registry namespace).

aws → provider.

version = "5.62.0"
Locks the provider to version 5.62.0. This ensures you get consistent behavior across environments.

2. Provider Block
provider "aws" {
  # Configuration options
}


provider "aws"
This defines and configures the AWS provider itself.

# Configuration options
Here’s where you’d specify details like:

provider "aws" {
  region  = "us-east-1"
  profile = "default"
}


This tells Terraform how to connect to AWS.

3. How It Works Together

The terraform block declares the dependency → “we’re using AWS provider from HashiCorp at version 5.62.0.”

The provider block configures it → “here’s how Terraform should authenticate and interact with AWS.”

After adding this to your .tf file, you run:

terraform init


This downloads the provider plugin and prepares your working directory.

👉 In short:

Terraform block = dependency declaration.

Provider block = configuration for that dependency.
<img width="316" height="317" alt="image" src="https://github.com/user-attachments/assets/85e513ed-6bb3-4aad-821d-ffae856dbe65" />

## Terraform imit (initialise)
this is a crucial command it is the command you run in any new or existing terraform project 
think of it like seting up a work place 

brrak down
initialising the backend - where terraform stores the stste of your infra could be store in local file or machine or remotley like in s3 bucket this is where the idempotancy comes in

initialising provider plug in - teraform init is used to download your provider terraform looks at yoour config and identify which provider you need and then downloadds these providers from the terraform registary or otehr soruces 
providers aree like plugings that let terraform communicate with the cloud 
<img width="595" height="305" alt="image" src="https://github.com/user-attachments/assets/e6823f04-332f-4120-afc6-3098b175f2ec" />

## terraform plan 
this command is to when terraform previews the changes terraform will make before it happens so you cna make sure everything is just right 

what is terraform plan?
its your way to see into the future by this i mena it allows you to see what your changes will do 
terraform analyses your con fig file compares to the state file then creates a plan on what it eill do next

desired state = config
current state = current state 

The output of running terraform plan represents our desired state

what key things should be looked out for ?
when should you run a terraform plan ?
what do you do with huge outputted plans ?
When workinging with large infra u can come across these issues 

plan break down 
resoyurces actions are indicated with the following symbols:
+ create: resources that re created
~ update-in-place: Resources that will be modified.
- destroy: RESOURCES THAT ARE DELETED

terraform will perform these actions:
AN ec2 instanced (aws_instance.example) will be created
A security group (aws_security_group.example) will have some properties updated.
An S3 bucket (aws_s3_bucket.example) will be destroyed.

always run a plan and look at the plan summary 
<img width="409" height="586" alt="image" src="https://github.com/user-attachments/assets/ab7c888b-ef15-4ebe-a99d-df50c349ebb8" />

## Terraform apply
Terraform apply takes the plan and applys it to your infrastructure 
it will create an execute plan theen load up a confermation before starting
after you say yess terraform will apply the chnages 

resource actions:
(aws_instance.example): creating
(aws_security_group.example) modifying
(aws_s3_bucket.example) destroying 
<img width="327" height="477" alt="image" src="https://github.com/user-attachments/assets/69fc4c4e-32cb-46d6-83d8-faa30c3d94c6" />

## Terraform destroy
Terraform destory command is a convinent way to destroy all remote objects managed by a particular Terraform configuration 
Say you just finished a project and you want to clean up your environment instead of deleting it 1 by 1 terraform destroy allows you to remove everything with saftey 
its the opposite if terraform apply
Terraform will read your current config and state file to understand what resources its managing
similar to a plan it creates a destruction plan telling you what will be deleted 
then terraform will have a confirmation after that the changes will be made to the state file and also the cloud 

## Resource block
In terraform a resource block defines a piece of infrastructure you want to manage such as ec2 instance, data base or s3 bucket
The resource block is where you specify what you want to create 
break down:
Resource "aws_instance" "Test" - defines resource type and the name of your resource 
ami - amazon machine images used to launch your instance determines your instance OS ect
instance_type - detirmines the configuration of your instance for exampple t2.micro
tags - a way to label or categorise your resources casn be named anything depening on the enivornment you are in such as dev or prod
<img width="379" height="218" alt="image" src="https://github.com/user-attachments/assets/3601ee61-62c2-4ba8-b6a7-e4d130fd864f" />

## terraform registary 
this is where you will find the neceessary code for your project 
<img width="929" height="683" alt="image" src="https://github.com/user-attachments/assets/108eb810-e37a-4ab9-9992-d811b98cadc3" />

## terraform import
this is a command that allows you to take excisting resources into your cloud environment and then bring them under terraform 
this is done when you wnat to intergrate terraform with an exisitng infrastructure set up without needing to recreate anything from scratch 
if you join a compan y that already has recouses that are delpyed to the cloud manually and you want to impliment best practices and iac 
it would be a pain to delete them and manually create them from scratch
terraform import allows you to bring those existing resources that were created manualy into you tf environmenr
first identify the resource on the cloud such as ec2 or s3
then create a resources block on the terrafrom config 

## terraform importing code block
import - in terraform v1.5.0+ use and import block to import instnces usingt he id
<img width="390" height="104" alt="image" src="https://github.com/user-attachments/assets/87b646f3-81df-4dca-aff1-750c3cca34dc" />

## Terraform Importing - Terraform Registry
heres the import example
one thing to remember is when importing is run a plan after to make sure the imported resource matches your current state 
keep running plans after imports to ensure the chnages have been made 
<img width="796" height="446" alt="image" src="https://github.com/user-attachments/assets/7309c5b3-61a2-4d90-8b5c-014db5665549" />

## terraform import ecample 
create new ec2 
<img width="779" height="42" alt="image" src="https://github.com/user-attachments/assets/f2b3546f-40b7-40fd-b884-2d3e4db30be1" />
get import code from tf registary 
<img width="765" height="396" alt="image" src="https://github.com/user-attachments/assets/c869a33f-9f05-476b-82d8-80f6fd96036b" />
create a resuurce 
<img width="494" height="88" alt="image" src="https://github.com/user-attachments/assets/93236387-e32f-4b96-8637-2a847614b43c" />
import with resoruce name and instance id
<img width="549" height="133" alt="image" src="https://github.com/user-attachments/assets/b45864b4-14ec-4b85-92fe-2c9223715013" />
import sucessful 
<img width="710" height="208" alt="image" src="https://github.com/user-attachments/assets/1a16615a-cd7e-4136-98f5-0b55003a091f" />






























































































