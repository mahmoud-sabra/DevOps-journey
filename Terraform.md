## **Infrastructure As Code (IaC)**
**what is Infrastructure as Code (IaC) ?**
It is the management of infrastructure (networks, virtualmachines, load balancers, and connection topology) in a descriptive model, Infrastructure as code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.
- [What is Infrastructure as Code with Terraform? | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/infrastructure-as-code)
![[Pasted image 20250107164153.png]]


**Idempotence** is a principle of Infrastructure as Code. Idempotence is the property that a deployment command always sets the target environment into the same configuration, regardless of the environment’s starting state

## **Benefits of IaC**
While there are many benefits of Infrastructure as Code, a few key benefits include simplifying cloud adoption, allowing us to adopt cloud-based services and offerings to improve our capabilities quickly. Infrastructure as Code allows us to remove many of the manual steps required today for infrastructure requests, giving us the ability to automate approved requests without worrying about tickets sitting in a queue. We can also use Infrastructure as Code to provide capacity-on-demand by offering a library of services for our developers. We can publish a self-service capability where developers and application owners can be empowered to request and provision infrastructure that better matches their requirements. Again, all of this is possible while driving standardization and consistency throughout the organization, which can drive efficiencies and reduce errors or deviations from established norms.

## **Example of IaC** 
IaC Tools The list below represents some of the most popular Infrastructure as Code tools used by many organizations worldwide. These tools focus on deploying infrastructure on a private or public cloud platform. The list does NOT include tools such as Puppet, Chef, Saltstack, or Ansible since those are commonly placed in the configuration management category and don’t really deploy infrastructure resources.
There are likely other tools available, but they are not as popular as the ones listed below. • 

- HashiCorp Terraform - terraform.io 
-  AWS CloudFormation - aws.amazon.com/cloudformation 
-  Azure Resource Manager (ARM) - azure.microsoft.com 
-  Google Cloud Deployment Manager - cloud.google.com/deployment-manager/docs 
## ***What is Terraform**
**Terraform** is HashiCorp's infrastructure as code tool.
It lets you define resources and infrastructure in human-readable, declarative configuration files,
and manages your infrastructure's lifecycle.
Using Terraform has several advantages over manually managing your infrastructure:
## **Why Terraform?**
- Terraform can manage infrastructure on multiple cloud platforms.
- The human-readable configuration language helps you write infrastructure code quickly.
- Terraform's state allows you to track resource changes throughout your deployments.
- You can commit your configurations to version control to safely collaborate on infrastructure. an IaC model generates the same environment every time it is applied.

>One cool thing about Terraform is, it’s plan command lets you see what changes you’re about to apply before you apply them.

![[Pasted image 20250322175520.png]]

### Installation
[Install Terraform | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


## **How Terraform works?**
Terraform is logically split into two main parts: Terraform Core and Terraform Plugins.
Terraform Core uses remote procedure calls (RPC) to communicate with Terraform Plugins,
and offers multiple ways to discover and load plugins to use.
[How Terraform works with plugins | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/plugin/how-terraform-works)

### **Terraform core**
**Terraform Core** is a statically-compiled binary written in the Go programming language. The
compiled binary is the command line tool (CLI) terraform, the entrypoint for anyone using
Terraform.

The primary responsibilities of Terraform Core are:
1. Infrastructure as code: reading and interpolating configuration files and modules
2. Resource state management
3. Construction of the Resource Graph
4. Plan execution
5. Communication with plugins over RPC

### **Terraform plugins**
**Terraform Plugins** are written in Go and are executable binaries invoked by Terraform Core
over RPC. Each plugin exposes an implementation for a specific service, such as AWS, or
provisioner, such as bash. All Providers and Provisioners used in Terraform configurations are
plugins. They are executed as a separate process and communicate with the main Terraform
binary over an RPC interface.

The primary responsibilities of Provider Plugins are:
1. Initialization of any included libraries used to make API calls
2. Authentication with the Infrastructure Provider
3. Define Resources that map to specific Services

The primary responsibilities of Provisioner Plugins are:
Executing commands or scripts on the designated Resource after creation, or on
destruction.


## **Terraform Workflow**
![[Pasted image 20250322202001.png]]

**Terraform init**
The terraform init command is used to initialize a working directory containing
Terraform configuration files.

> This is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control. It is safe to run this command multiple times.


**Terraform plan**
The terraform plan command is used to create an execution plan. Terraform
performs a refresh, unless explicitly disabled, and then determines what actions are
necessary to achieve the desired state specified in the configuration files.
 
 >This command is a convenient way to check whether the execution plan for a set of changes matches your expectations without making any changes to real resources or to the state. 
 
**Terraform apply**
The terraform apply command is used to apply the changes required to reach the
desired state of the configuration, or the pre-determined set of actions generated by
a terraform plan execution plan.

**Terraform destroy**
The terraform destroy command is used to destroy the Terraform-managed
infrastructure.

----
## Terraform providers
**Providers**
Terraform is used to create, manage, and update infrastructure resources such as
physical machines, VMs, network switches, containers, and more. Almost any
infrastructure type can be represented as a resource in Terraform.
A provider is responsible for understanding API interactions and exposing
resources. Providers generally are an IaaS (e.g. Alibaba Cloud, AWS, GCP,
Microsoft Azure, OpenStack), PaaS (e.g. Heroku), or SaaS services (e.g. Terraform
Cloud, DNSimple, Cloudflare).

----
-----

# 1. Lab: Terraform Basics


All interactions with Terraform occur via the CLI. Terraform is a local tool (runs on the current machine). The terraform ecosystem also includes providers for many cloud services, and a module repository. Hashicorp also has products to help teams manage Terraform: Terraform Cloud and Terraform Enterprise.

There are a handful of basic terraform commands, including:

- `terraform init`
- `terraform validate`
- `terraform plan`
- `terraform apply`
- `terraform destroy`

These commands make up the terraform workflow that we will cover in objective 6 of this course. It will be beneficial for us to explore some basic commands now so that work alongside and deploy our configurations.

- Task 1: Verify Terraform installation and version
- Task 2: Initialize Terraform Working Directory: `terraform init`
- Task 3: Validating a Configuration: `terraform validate`
- Task 4: Genenerating a Terraform Plan: `terraform plan`
- Task 5: Applying a Terraform Plan: `terraform apply`
- Task 6: Terraform Destroy: `terraform destroy`

## Task 1: Verify Terraform installation and version


You can get the version of Terraform running on your machine with the following command:

```shell
terraform -version
```

If you need to recall a specific subcommand, you can get a list of available commands and arguments with the help argument.

```shell
terraform -help
```

## Task 2: Terraform Init


Initializing your workspace is used to initialize a working directory containing Terraform configuration files.

Copy the code snippet below into the file called `main.tf` This snippet leverages the random provider, maintained by HashiCorp, to generate a random string.

`main.tf`

```hcl
resource "random_string" "random" {
  length = 16
}
```

Once saved, you can return to your shell and run the init command shown below. This tells Terraform to scan your code and download anything it needs locally.

```shell
terraform init
```

Once your Terraform workspace has been initialized you are ready to begin planning and provisioning your resources.

> Note: You can validate that your workspace is initialized by looking for the presence of a `.terraform` directory. This is a hidden directory, which Terraform uses to manage cached provider plugins and modules, record which workspace is currently active, and record the last known backend configuration in case it needs to migrate state. This directory is automatically managed by Terraform, and is created during initialization.

## Task 3: Validating a Configuration
[Syntax - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/syntax/configuration) 

The terraform validate command validates the configuration files in your working directory.

To validate there are no syntax problems with our terraform configuration file run a

```shell
terraform validate
```

```shell
Success! The configuration is valid.
```

## Task 4: Genenerating a Terraform Plan


Terraform has a dry run mode where you can preview what Terraform will change without making any actual changes to your infrastructure. This dry run is performed by running a `terraform plan`.

In your terminal, you can run a plan as shown below to see the changes required for Terraform to reach your desired state you defined in your code. This is equivalent to running Terraform in a "dry" mode.

```shell
terraform plan
```

If you review the output, you will see 1 change will be made which is to generate a single random string.

```shell
Terraform will perform the following actions:

  # random_string.random will be created
  + resource "random_string" "random" {
      + id          = (known after apply)
      + length      = 16
      + lower       = true
      + min_lower   = 0
      + min_numeric = 0
      + min_special = 0
      + min_upper   = 0
      + number      = true
      + result      = (known after apply)
      + special     = true
      + upper       = true
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```

> Note: Terraform also has the concept of planning out changes to a file. This is useful to ensure you only apply what has been planned previously. Try running a plan again but this time passing an -out flag as shown below.

```shell
terraform plan -out myplan
```

This will create a plan file that Terraform can use during an `apply`.

## Task 5: Applying a Terraform Plan

Run the command below to build the resources within your plan file.

```shell
terraform apply myplan
```

Once completed, you will see Terraform has successfully built your random string resource based on what was in your plan file.

Terraform can also run an `apply` without a plan file. To try it out, modify your `main.tf` file to create a random string with a length of 10 instead of 16 as shown below:

```hcl
resource "random_string" "random" {
  length = 10
}
```

and run a `terraform apply`

```shell
terraform apply
```

Notice you will now see a similar output to when you ran a `terraform plan` but you will now be asked if you would like to proceed with those changes. To proceed enter `yes`.

```shell
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # random_string.random must be replaced
-/+ resource "random_string" "random" {
      ~ id          = "XW>5m{w8Ig96d1A&" -> (known after apply)
      ~ length      = 16 -> 10 # forces replacement
      ~ result      = "XW>5m{w8Ig96d1A&" -> (known after apply)
        # (8 unchanged attributes hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```

Once complete the random string resource will be created with the attributes specified in the `main.tf` configuration file.

## Task 6: Terraform Destroy



The `terraform destroy` command is a convenient way to destroy all remote objects managed by a particular Terraform configuration. It does not delete your configuration file(s), `main.tf`, etc. It destroys the resources built from your Terraform code.

Run the command as shown below to run a planned destroy:

```shell
terraform plan -destroy
```

```shell
Terraform will perform the following actions:

  # random_string.random will be destroyed
  - resource "random_string" "random" {
      - id          = "1HIQs)moC0" -> null
      - length      = 10 -> null
      - lower       = true -> null
      - min_lower   = 0 -> null
      - min_numeric = 0 -> null
      - min_special = 0 -> null
      - min_upper   = 0 -> null
      - number      = true -> null
      - result      = "1HIQs)moC0" -> null
      - special     = true -> null
      - upper       = true -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.
```

You will notice that it is planning to destroy your previously created resource. To actually destroy the random string you created, you can run a destroy command as shown below.

```shell
terraform destroy
```

```shell
Terraform will perform the following actions:

  # random_string.random will be destroyed
  - resource "random_string" "random" {
      - id          = "1HIQs)moC0" -> null
      - length      = 10 -> null
      - lower       = true -> null
      - min_lower   = 0 -> null
      - min_numeric = 0 -> null
      - min_special = 0 -> null
      - min_upper   = 0 -> null
      - number      = true -> null
      - result      = "1HIQs)moC0" -> null
      - special     = true -> null
      - upper       = true -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value:
```

> Note: As similar to when you ran an apply, you will be prompted to proceed with the destroy by entering "yes".

# 2. Lab: Terraform Plug-in Based Architecture


Terraform relies on plugins called "providers" to interact with remote systems and expand functionality. Terraform configurations must declare which providers they require so that Terraform can install and use them. This is performed within a Terraform configuration block.

- Task 1: View available Terraform Providers
- Task 2: Install the Terraform AWS Provider
- Task 3: View installed and required providers

## Task 1: View available Terraform Providers


Terraform Providers are plugins that implement resource types for particular clouds, platforms and generally speaking any remote system with an API. Terraform configurations must declare which providers they require, so that Terraform can install and use them. Popular Terraform Providers include: AWS, Azure, Google Cloud, VMware, Kubernetes and Oracle.

[![Terraform Plug-in Architecture](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2004%20-%20Understand%20Terraform%20Basics/img/terraform-plugin-ins.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2004%20-%20Understand%20Terraform%20Basics/img/terraform-plugin-ins.png)

For a full list of available Terraform providers, reference the [Terraform Provider Registry](https://registry.terraform.io/)

[![Terraform Provider Registry](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2004%20-%20Understand%20Terraform%20Basics/img/terraform_provider_registry.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2004%20-%20Understand%20Terraform%20Basics/img/terraform_provider_registry.png)

## Task 2: Install the Terraform AWS Provider


To install the [Terraform AWS provider](https://registry.terraform.io/providers/hashicorp/aws/latest), and set the provider version in a way that is very similar to how you did for Terraform. To begin you need to let Terraform know to use the provider through a `required_providers` block in the `terraform.tf` file as seen below.

`terraform.tf`

```hcl
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "3.1.0"
  }
}
```

> Note: You can always find the latest version of a provider on its > registry page at [https://registry.terraform.io](https://registry.terraform.io/).

Run a `terraform init` to install the providers specified in the configuration

```shell
terraform init
```

## Task 3: View installed and required providers

If you ever would like to know which providers are installed in your working directory and those required by the configuration, you can issue a `terraform version` and `terraform providers` command.

```shell
terraform version
```

![[Pasted image 20250326133352.png]]


```shell
terraform providers
```
![[Pasted image 20250326133321.png]]

[Build infrastructure | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build)

## Configure Terraform AWS Provider

Edit the `provider` block within the `main.tf` to configure the Terraform AWS provider.

provider.tf`

```hcl
# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}
```

This informs Terraform that it will deploy services into the `us-east-1` region within AWS.
[Providers - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/providers)

# 3. Lab: Terraform Resource Blocks


Terraform uses resource blocks to manage infrastructure, such as virtual networks, compute instances, or higher-level components such as DNS records. Resource blocks represent one or more infrastructure objects in your Terraform configuration. Most Terraform providers have a number of different resources that map to the appropriate APIs to manage that particular infrastructure type.

```hcl
# Template
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
 # Block body
<IDENTIFIER> = <EXPRESSION> # Argument
}

# AWS EC2 Example
resource "aws_instance" "web_server" { # BLOCK
  ami = "ami-04d29b6f966df1537" # Argument
  instance_type = t3.micro 
```

|Resource|AWS Provider|AWS Infrastructure|
|---|---|---|
|Resource 1|aws_instance|EC2 Instance|
|Resource 2|aws_security_group|Security Group|
|Resource 3|aws_s3_bucket|Amazon S3 bucket|
|Resource 4|aws_key_pair|EC2 Key Pair|

When working with a specific provider, like AWS, Azure, or GCP, the resources are defined in the provider documentation. Each resource is fully documented in regards to the valid and required arguments required for each individual resource. For example, the `aws_key_pair` resource has a "Required" argument of `public_key` but optional arguments like `key_name` and `tags`. You'll need to look at the provider documentation to understand what the supported resources are and how to define them in your Terraform configuration.

**Important** - Without `resource` blocks, Terraform is not going to create resources. All of the other block types, such as `variable`, `provider`, `terraform`, `output`, etc. are essentially supporting block types for the `resource` block.

- Task 1: View and understand an existing resource block in Terraform
- Task 2: Add a new resource to deploy an Amazon S3 bucket
- Task 3: Create a new AWS security group
- Task 4: Configure a resource from the random provider
- Task 5: Update the Amazon S3 bucket to use the random ID

## Task 1: View and understand an existing resource block in Terraform

Using the main.tf created in previous labs, look for a resource block that deploys a route table. The code should look something like this:

```hcl
resource "aws_route_table" "public_route_table" {
  vpc_id = aws_vpc.vpc.id

  route {
    cidr_block     = "0.0.0.0/0"
    gateway_id     = aws_internet_gateway.internet_gateway.id
  }
  tags = {
    Name      = "demo_public_rtb"
    Terraform = "true"
  }
}
```

```hcl
resource "aws_internet_gateway" "internet_gateway" {

  vpc_id = aws_vpc.my_vpc.id

  tags = {

    Name = "demo_igw"

  }

}
```

Let's look at the details in this resource block. First, all resource blocks will be declared using the resouce block type. Next, you'll find the type of resource that is going to be deployed. In this case, it's `aws_route_table` which is part of the AWS provider. Finally, we gave this resource a local name of `public_route_table`.

> Note: Your resource blocks must have a unique resource id (combination of resource type along with resource name). In our example, our resource id is `aws_route_table.public_route_table`, which is the combination of our resource type `aws_route_table` and resource name `public_route_table`. This naming and interpolation nomenclature is powerful part of HCL that allows us to reference arguments from other resource blocks.

Within our resouce block, we have arguments that are specific to the type of resource we are deploying. In our case, when we deploy a new AWS route table, there are certain arguments that are either `required` or `optional` that will apply to this resource. In our example, an AWS route table must be tied to a VPC, so we are providing the `vpc_id` argument and providing a value of our VPC using interpolation. Check out the `aws_route_table` documentation and see all the additional arguments that are available.

## Task 2: Add a new resource to deploy an Amazon S3 bucket


Ok, so now that we understand more about a resource block, let's create a new resource that will create an Amazon S3 bucket. In your main.tf file, add the following resource block:

```hcl
resource "aws_s3_bucket" "my-new-S3-bucket" {   
  bucket = "my-new-tf-test-bucket-sabra"

  tags = {     
    Name = "My S3 Bucket"     
    Purpose = "Intro to Resource Blocks Lab"   
  } 
}

resource "aws_s3_bucket_ownership_controls" "my_new_bucket_acl" {   
  bucket = aws_s3_bucket.my-new-S3-bucket.id  
  rule {     
    object_ownership = "BucketOwnerPreferred"   
  }
}
```

### Task 2.1.1



Run a `terraform plan` to see that this new Amazon S3 bucket will be added to our account. Don't worry, S3 buckets don't incur any fees unless you upload data to the bucket.

```shell
terraform plan
```

```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_s3_bucket.my-new-S3-bucket will be created
  + resource "aws_s3_bucket" "my-new-S3-bucket" {
      + acceleration_status         = (known after apply)
      + acl                         = "private"
      + arn                         = (known after apply)
      + bucket                      = "my-new-tf-test-bucket-sabra"
      + bucket_domain_name          = (known after apply)
      + bucket_regional_domain_name = (known after apply)
      + force_destroy               = false
      + hosted_zone_id              = (known after apply)
      + id                          = (known after apply)
      + region                      = (known after apply)
      + request_payer               = (known after apply)
      + tags                        = {
          + "Name"    = "My S3 Bucket"
          + "Purpose" = "Intro to Resource Blocks Lab"
        }
      + tags_all                    = {
          + "Name"    = "My S3 Bucket"
          + "Purpose" = "Intro to Resource Blocks Lab"
        }
      + website_domain              = (known after apply)
      + website_endpoint            = (known after apply)

      + versioning {
          + enabled    = (known after apply)
          + mfa_delete = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```

Once the plan looks good, let's apply our configuration to the account by issuing a `terraform apply`

```shell
terraform apply

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes
```

You will be prompted to confirm the changes before they're applied. Respond with `yes`.

### Task 2.2.1


Log into your AWS account and validate that the new Amazon S3 bucket exists.

## Task 3: Configure an AWS security group


Let's add one more resource block just to make sure you've got the hang of it. In this example, we're going to create a new Security Group that could be used for a web server to allow secure inbound connectivity over 443. If you are deploying EC2 instances or other resources in AWS, you'll probably need to define a custom security group.

In your main.tf file, add the following resource block:

```hcl
resource "aws_security_group" "my-new-security-group" {
  name        = "web_server_inbound"
  description = "Allow inbound traffic on tcp/443"
  vpc_id      = aws_vpc.vpc.id

  ingress {
    description = "Allow 443 from the Internet"
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name    = "web_server_inbound"
    Purpose = "Intro to Resource Blocks Lab"
  }
}
```

Notice that this resource, the `aws_security_group` requires completely different arguments. We're providing a name, a description, a VPC, and most importantly, the rules that we want to permit or restrict traffic. We also providing tags that will be added to the resource.



Log into AWS, browse to the EC2 or VPC console and verify the newly created Security Group.

## Task 4: Configure a resource from the random provider



Ok, one more resource. But this time, it's not an AWS resource. Terraform supports many resources that don't interact with any other services. In fact, there is a provider that you can use just to create random data to be used in your Terraform.

Let's add a new resource block to Terraform using the `random` provider. In your main.tf file, add the following resource block:

```hcl
resource "random_id" "randomness" {
  byte_length = 10
}
```



Whoops....what happened? Well, we added a new resource that requires a provider that we haven't downloaded yet. Up until now, we've just been using the AWS provider, so adding AWS resources has worked fine. But now we need the hashicorp/random provider to use the `random_id` resource.

```

Notice that Terraform is going to create a new resource for us now:

```



Apply complete! Resources: 1 added, 0 changed, 0 destroyed.


## Task 5: Update the Amazon S3 bucket to use the random ID



Now that we have a `random_id` being created by Terraform, let's see how we can use that for other resources. If you're not aware, Amazon S3 bucket names have to be globally unique, meaning nobody in the world can create a bucket with the same name as an existing bucket. That means if I create a bucket named "my-cool-s3-bucket", nobody else can create a bucket with the same name. This is where the random_id might come in handy, so let's update the name of our bucket to use a random ID.

In your main.tf file, find the resource block where you created a new Amazon S3 bucket. It's the code we added in Task 2 above. Modify the `bucket` argument to include the following:

```hcl
resource "aws_s3_bucket" "my-new-S3-bucket" {
  bucket = "my-new-tf-test-bucket-${random_id.randomness.hex}"

  tags = {
    Name    = "My S3 Bucket"
    Purpose = "Intro to Resource Blocks Lab"
  }
}
```

### Task 5.1.1

Run a `terraform plan` again to see that Terraform is going to replace our Amazon S3 bucket in our account because the name is changing. The name will now end with our random id that we created using the `random_id` resource.

```shell
terraform plan
```

```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # aws_s3_bucket.my-new-S3-bucket must be replaced
-/+ resource "aws_s3_bucket" "my-new-S3-bucket" {
      + acceleration_status         = (known after apply)
      ~ arn                         = "arn:aws:s3:::my-new-tf-test-bucket-bryan" -> (known after apply)
      ~ bucket                      = "my-new-tf-test-bucket-bryan" -> "my-new-tf-test-bucket-Htd2k6vC5PrbOxGeCBxAcQ" # forces replacement
      ~ bucket_domain_name          = "my-new-tf-test-bucket-bryan.s3.amazonaws.com" -> (known after apply)
      ~ bucket_regional_domain_name = "my-new-tf-test-bucket-bryan.s3.amazonaws.com" -> (known after apply)
      ~ hosted_zone_id              = "Z3AQBSTGFYJSTF" -> (known after apply)
      ~ id                          = "my-new-tf-test-bucket-bryan" -> (known after apply)
      ~ region                      = "us-east-1" -> (known after apply)
      ~ request_payer               = "BucketOwner" -> (known after apply)
      ~ tags                        = {
          + "Random"  = "Htd2k6vC5PrbOxGeCBxAcQ"
            # (2 unchanged elements hidden)
        }
      ~ tags_all                    = {
          + "Random"  = "Htd2k6vC5PrbOxGeCBxAcQ"
            # (2 unchanged elements hidden)
        }
      + website_domain              = (known after apply)
      + website_endpoint            = (known after apply)
        # (2 unchanged attributes hidden)

      ~ versioning {
          ~ enabled    = false -> (known after apply)
          ~ mfa_delete = false -> (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 1 to destroy.
```

### Task 5.1.2


Now that we're done with going over the Resource block, feel free to delete the resources that we created in this lab. These resources include:

- Amazon S3 bucket
- Security Group
- Random ID

Once you deleted them from your Terraform configuration file, go ahead and run a `terraform plan` and `terraform apply` to delete the resources from your account.

# 4. Lab: Introduction to the Terraform Variables Block


As you begin to write Terraform templates with a focus on reusability and DRY development (don't repeat yourself), you'll quickly begin to realize that variables are going to simplify and increase usability for your Terraform configuration. Input variables allow aspects of a module or configuration to be customized without altering the module's own source code. This allows modules to be shared between different configurations.

Input variables (commonly referenced as just 'variables') are often declared in a separate file called `variables.tf`, although this is not required. Most people will consolidate variable declaration in this file for organization and simplification of management. Each variable used in a Terraform configuration must be declared before it can be used. Variables are declared in a variable block - one block for each variable. The variable block contains the variable name, most importantly, and then often includes additional information such as the type, a description, a default value, and other options.

The variable block follows the following pattern:
```
variable “<VARIABLE_NAME>” {
  # Block body
  type = <VARIABLE_TYPE>
  description = <DESCRIPTION>
  default = <EXPRESSION>
  sensitive = <BOOLEAN>
  validation = <RULES>
}

```
# Example



```hcl
variable "aws_region" {
  type        = string
  description = "region used to deploy workloads"
  default     = "us-east-1"
}
```

- Task 1: Add a new VPC resource block with static values
- Task 2: Define new variable blocks to declare new variables
- Task 3: Modify the value of the variable by adding defaults
## Task 1: Add a new VPC resource block with static values

Before we can add any meaningful new variables, we should add a new resource to use as a demo. Let's add a new VPC resource that we'll use in this lab. In the `main.tf` file, add the following code at the bottom. **_Do not remove the existing VPC resource_**
```
resource "aws_subnet" "variables-subnet" {
  vpc_id                  = aws_vpc.my_vpc.id
  cidr_block              = "10.0.10.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true

  tags = {
    Name      = "sub-variables-us-east-1a"
    Terraform = "true"
  }
}
```
## Task 2: Define new variable blocks to declare new variables


Now that we have a new resources to use, let's change some of those static values to use variables instead. In your `variables.tf` file, add the following variable blocks anywhere in the file:
### Task 2.1


In your `main.tf` file, let's remove our static values and replace them with our new variables to make our configuration a bit more flexible. Update the configuration file so the new VPC resource reflects the changes shown below:

```hcl
resource "aws_subnet" "variables-subnet" {
  vpc_id                  = aws_vpc.vpc.id
  cidr_block              = var.variables_sub_cidr
  availability_zone       = var.variables_sub_az
  map_public_ip_on_launch = var.variables_sub_auto_ip

  tags = {
    Name      = "sub-variables-${var.variables_sub_az}"
    Terraform = "true"
  }
}
```

## Task 3: Modify the value of the variable by adding defaults



Another common method of providing values for variables is by setting default values in the variable block. If no other values are provided during a `terraform plan` or `terraform apply`, then Terraform will use the default values. This is especially handy when you have variables where the value doesn't often change.

In the `variables.tf` file, modify the new variables we added earlier to now include a default argument and value.
```
variable "variables_sub_cidr" {
  description = "CIDR Block for the Variables Subnet"
  type        = string
  default     = "10.0.10.0/24"
}

variable "variables_sub_az" {
  description = "Availability Zone used for Variables Subnet"
  type        = string
  default     = "us-east-1a"
}

variable "variables_sub_auto_ip" {
  description = "Set Automatic IP Assigment for Variables Subnet"
  type        = bool
  default     = true
}
```


-----
# 5.  Lab: Introduction to the Terraform Locals Block

Locals blocks (often referred to as locals) are defined values in Terraform that are used to reduce repetitive references to expressions or values. Locals are very similar to traditional input variables and can be referred to throughout your Terraform configuration. Locals are often used to give a name to the result of an expression to simplify your code and make it easier to read.

Locals are not set directly by the user/machine executing the Terraform configuration, and the values don't change between or during the Terraform workflow (`init`, `plan`, `apply`).

Locals are defined in a `locals` block (plural) and include named local variables with their defined values. Each locals block can contain one or more local variables. Locals are then referenced in your configuration using interpolation using `local.<name>` (note `local` and not `locals`). The syntax of a locals block is as follows:
[Local Values - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/values/locals)
# Template


```hcl
locals {
  # Block body
  local_variable_name = <EXPRESSION OR VALUE>
  local_variable_name = <EXPRESSION OR VALUE>
}
```

# Example


```hcl
locals {
  time = timestamp()
  application = "api_server"
  server_name = "${var.account}-${local.application}"
```

- Task 1: Define the Name of an EC2 Instance using a Local Variable

## Task 1: Define the Name of an EC2 Instance using a Local Variable



Before we can use a locals variable, it needs to be defined in our configuration file. Locals are often defined right in the configuration file where they will be used. In the `main.tf` file, add the following locals block to the configuration file:

```hcl
locals {
  team = "depi-dev"
  application = "learning"
  server_name = "ec2-${var.environment}-api-${var.variables_sub_az}"
}
```

Next, let's update the configuration of our web server resource to use the locals variable to define the name. Modify the web_server resource in `main.tf` so it matches the following:

```hcl
resource "aws_instance" "web_server" {
  ami           = "ami-084568db4383264d4"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.variables-subnet.id
  tags = {
    Name = local.server_name
    Owner = local.team
    App = local.application
  }
}
```

### Task 1.1


Run a `terraform plan` to see the changes to our web server. You should see that the EC2 instance will not be destroyed, but the name of the server (tag) will be updated to reflect the value of our local variables.

```shell
terraform plan
```



### Task 1.2


Let's go ahead and commit our code to validate Terraform makes the desired changes to the AWS infrastructure. Run a `terraform apply` to apply the changes. Log into AWS and validate the changes were applied.

Once validated, feel free to remove the `locals` block and tags on the EC2 instance and then apply the configuration to revert back to the original values. However, you can leave everything in your Terraform configuration if you'd like.

----
# 6. Lab: Introduction to the Terraform Data Block


Data sources are used in Terraform to load or query data from APIs or other Terraform workspaces. You can use this data to make your project's configuration more flexible, and to connect workspaces that manage different parts of your infrastructure. You can also use data sources to connect and share data between workspaces in Terraform Cloud and Terraform Enterprise.

To use a data source, you declare it using a `data` block in your Terraform configuration. Terraform will perform the query and store the returned data. You can then use that data throughout your Terraform configuration file where it makes sense.

Data Blocks within Terraform HCL are comprised of the following components:

- Data Block - "resource" is a top-level keyword like "for" and "while" in other programming languages.
- Data Type - The next value is the type of the resource. Resources types are always prefixed with their provider (aws in this case). There can be multiple resources of the same type in a Terraform configuration.
- Data Local Name - The next value is the name of the resource. The resource type and name together form the resource identifier, or ID. In this lab, one of the resource IDs is `aws_instance.web`. The resource ID must be unique for a given configuration, even if multiple files are used.
- Data Arguments - Most of the arguments within the body of a resource block are specific to the selected resource type. The resource type's documentation lists which arguments are available and how their values should be formatted.

Example: A data block requests that Terraform read from a given data source ("aws_ami") and export the result under the given local name ("example"). The name is used to refer to this resource from elsewhere in the same Terraform module.

# Template


```hcl
data “<DATA TYPE>” “<DATA LOCAL NAME>”   {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}
```

- Task 1: Add a new data source to query the current AWS region being used
- Task 2: Update the Terraform configuration file to use the new data source
- Task 3: View the data source used to retrieve the availability zones within the region
- Task 4: Validate the data source is being used in the Terraform configuration file
- Task 5: Create a new data source for querying a different Ubuntu image
- Task 6: Make the aws_instance web_server use the Ubuntu image returned by the data source

## Task 1: Add a new data source to query the current AWS region being used



Modify the main.tf file to include a new data source block. This simple data source will use the AWS credentials and determine the AWS region that you are using.

```hcl
#Retrieve the AWS region
data "aws_region" "current" { }
```

## Task 2: Update the Terraform configuration file to use the new data source

Now that we know Terraform will query AWS for the current region, we can now use that information within our configuration file. In our main.tf file, you'll find the resource block where we are creating the VPC. Within that block, you'll see that we are adding tags to the VPC for easily identification. Let's add a "Region" tag and use the results of our data source we just added.

Modify the VPC resource block to add another tag and get the value from our data source. Terraform will query AWS, grab the current region, and add the value to our new tag.

```
#Define the VPC
resource "aws_vpc" "vpc" {
  cidr_block = var.vpc_cidr

  tags = {
    Name        = var.vpc_name
    Environment = "demo_environment"
    Terraform   = "true"
    Region      = data.aws_region.current.name

  }
}
```

Notice the formatting of our reference to the data block. We'll go into more detail when we learn about Variables, but the syntax to refer to a data block is as follows:

`data.<type>.<name>.<attribute>`

In our example, `data` is used since we're referring to a data block. The "**type**" is `aws_region`, the "**name**" is `current`, and the "**attribute**" is `name`. You can simply look at the data block and see how this is all put together. Finally, `name` is one of the attributes that is exported by the `aws_region` data source. Make sure to check out the official documentation for a data source to learn about the different attributes available for the one you're using.

## Task 3: View the data source used retrieve the availability zones within the region

If you didn't notice already, we were already using a data source to retrieve the availability zones in the region we are using. Towards the top of the main.tf file, look for the following code:

```hcl
#Retrieve the list of AZs in the current AWS region
data "aws_availability_zones" "available" {}
```

It looks very similar to our first task, but this is retrieving different data for us. Obtaining this data might be helpful if you are building a fleet of web servers and you want to ensure each one is deployed in a different AZ. The benefit of using a data source, as opposed to manually typing in the availability zones, is that you can run the exact same Terraform in multiple regions and it would work without modifications, since the AZs are dynamically obtained by the data source.

## Task 4: Validate the data source is being used in the Terraform configuration file


Let's take a look at how we're already using this data source in our deployment. Look in the main.tf and find the resource block that is creating our private subnets. When you create a subnet, one of the required parameters is choosing an availability zone where the subnet will be created. Rather than hard code this, we can use our data source to dynamically choose an availability zone.

```hcl
#Deploy the private subnets
resource "aws_subnet" "private_subnets" {
  for_each          = var.private_subnets
  vpc_id            = aws_vpc.vpc.id
  cidr_block        = cidrsubnet(var.vpc_cidr, 8, each.value)
  availability_zone = tolist(data.aws_availability_zones.available.names)[each.value]

  tags = {
    Name      = each.key
    Terraform = "true"
  }
}
```

## Task 5: Create a new data source for querying a different Ubuntu image

### Step 5.1.1



Add an aws_ami data source called "ubuntu_22_04" in `main.tf`. It will find the most recent instance of a Ubuntu 22.04 AMI from Canonical (owner ID 099720109477).

```hcl
# Terraform Data Block - Lookup Ubuntu 22.04
data "aws_ami" "ubuntu_22_04" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }

  owners = ["099720109477"]
}
```

## Task 6: Modify the aws_instance so it uses the returned AMI


Edit the aws_instance in `main.tf` so that its ami argument uses the AMI returned by the data source.

```hcl
resource "aws_instance" "web_server" {
  ami                         = data.aws_ami.ubuntu_22_04.id
  instance_type               = "t3.micro"
  subnet_id                   = aws_subnet.public_subnets["public_subnet_1"].id
  security_groups             = [aws_security_group.vpc-ping.id]
  associate_public_ip_address = true
  tags = {
    Name = "Web EC2 Server"
  }
}
```

### Step 6.1.1

Run `terraform apply` one last time to apply the changes you made.

```shell
terraform apply
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes
  ```

---- 
# 7 Lab: Introduction to the Terraform Output Block
[Output Values - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/values/outputs)

Terraform output values allow you to export structured data about your resources. You can use this data to configure other parts of your infrastructure with automation tools, or as a data source for another Terraform workspace. Outputs are also necessary to share data from a child module to your root module.

As with all other blocks in HashiCorp Configuration Language (HCL), the output block has a particular syntax that needs to be followed when creating output blocks. Each output name should be unique. The syntax looks like this:

# Template



```hcl
output “<NAME>” {
  # Block body
  value= <EXPRESSION> # Argument
}
```

# Example

```hcl
output "web_server_ip" {
  description = "Public IP Address of Web Server on EC2"
  value       = aws_instance.web_server.public_ip
  sensitive   = true
}
```

- Task 1: Add Output Block to Export Attributes of Resources
- Task 2: Output Meaningful Data using Static and Dynamic Values
- Task 3: Generate Machine-Readable Outputs in JSON

## Task 1: Add Output Block to Export Attributes of Resources


In the same working directory that contains our `main.tf` and `variables.tf` files, create a new file called `outputs.tf`. This file is commonly used to store all output blocks within your working directory. In the new file, add the following code:

```hcl
output "hello-world" {
  description = "Print a Hello World text output"
  value = "Hello World"
}

output "vpc_id" {
  description = "Output the ID for the primary VPC"
  value = aws_vpc.vpc.id
}
```

### Task 1.1


After saving the new `outputs.tf`file, run a `terraform apply -auto-approve`to see our new outputs for our infrastructure.

```
No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no
differences, so no changes are needed.

Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

hello-world = "Hello World"
vpc_id = "vpc-058d23c9d5d2f70b5"
```

# Task 2: Output Meaningful Data using Static and Dynamic Values



Resource attribute data can also be included within a string to include additional information or create a particular output, such as a website URL or database connection string. Modify the `outputs.tf` file to include the additional output blocks as shown below:

```hcl
output "public_url" {
  description = "Public URL for our Web Server"
  value = "https://${aws_instance.web_server.public_ip}:8080/index.html"
}

output "vpc_information" {
  description = "VPC Information about Environment"
  value = "Your ${aws_vpc.vpc.tags.Environment} VPC has an ID of ${aws_vpc.vpc.id}"
}
```

# Task 2.1



After saving the new `outputs.tf`file, run a `terraform apply -auto-approve`to see our new output. The output now provides a full URL that contains the IP address of our public web server. We also have an additional string that provides information about our VPC as well.

```
No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no differences, so no changes
are needed.

Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

hello-world = "Hello World"
public_url = "https://10.0.101.10:8080/index.html"
vpc_id = "vpc-058d23c9d5d2f70b5"
vpc_information = "Your demo_environment VPC has an ID of vpc-058d23c9d5d2f70b5"
```

## Task 2.2

If you ever need to read the values of your Terraform outputs but might be nervous about running a `terraform apply`, you can use the `terraform output`command to view them.

Run a `terraform output`and view the list of outputs from your configuration:

```
$ terraform output
hello-world = "Hello World"
public_url = "https://10.0.101.10:8080/index.html"
vpc_id = "vpc-058d23c9d5d2f70b5"
vpc_information = "Your demo_environment VPC has an ID of vpc-058d23c9d5d2f70b5"
```

## Task 3: Generate Machine-Readable Outputs in JSON



When working with Terraform in your organization, it is common practice to use an automation tool to automate your terraform deployments. But don't fret! We can still use outputs and make them "machine-readable" so other automation tools can parse the information, if needed.

Run a `terraform output -json`and view the list of outputs in JSON format from your configuration:

---- 
# 8 Lab: Commenting Terraform Code



To make our code easier to understand for others who might want to contribute we may want to add a comment to explain what a resource or a particular code block is doing. The Terraform language supports three different syntaxes for comments:

```hcl
# begins a single-line comment, ending at the end of the line.
```

```hcl
// also begins a single-line comment, as an alternative to #.
```

```hcl
/* and */ are start and end delimiters for a comment that might span over multiple lines.
```

- Task 1: Add Single Line Comment to Terraform Configuration
- Task 2: Add Multi-Line Comment to Terraform Configuration

## Task 1: Add Single Line Comment to Terraform Configuration


Update your `main.tf` to include a single line comment at the top of your file.

```hcl
# IaC Buildout for Terraform Associate Exam

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}
```

Run a `terraform plan` to validate that adding a single line comment has no effect on the configuration and thus will return a `No Change` plan.

```shell
terraform plan
```

```shell
No changes. Infrastructure is up-to-date.
```

> Note: There is no harm in running a `terraform plan` after adding any items into a Terraform configuration file. In fact it can be quite useful to run to validate that your configuration changes will not have any impact on your deployments.

## Task 2: Add Multi-Line Comment to Terraform Configuration

Update your `main.tf` to include a single line comment at the top of your file.

```hcl
/*
Name: IaC Buildout for Terraform 
Description: AWS Infrastructure Buildout
Contributors: DEPI Sessions
*/

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

```

Run a `terraform plan` to validate that adding a single line comment has no effect on the configuration and thus will return a `No Change` plan.

```shell
terraform plan
```

```shell
No changes. Infrastructure is up-to-date.
```

The `#` single-line comment style is the default comment style and should be used in most cases. Automatic configuration formatting tools may automatically transform `//` comments into `#` comments, since the double-slash style is not idiomatic.

## Reference


[Terraform HCL Comments](https://www.terraform.io/docs/language/syntax/configuration.html#comments)


-----



  Use Terraform to create:

- Use data source to fetch **availability zones**, **Region** dynamically
    
- Create a **public VPC** setup (subnet + route table + IGW)
    
- Launch an **EC2 instance in a specific AZ**
    
- Create an **S3 bucket**
    
- Use **variables**, **outputs**, and **locals** properly ( outputs: instance_public_ip, s3_bucket_name, availability_zone_used )

# 9 Lab: Generate SSH Key with Terraform TLS Provider

The Terraform TLS provider provides utilities for working with Transport Layer Security keys and certificates. It provides resources that allow private keys, certificates and certificate requests to be created as part of a Terraform deployment.

- Task 1: Check Terraform
- Task 2: Install Terraform TLS Provider
- Task 3: Creates a self-signed certificate with TLS Provider
## Task 1: Check Terraform version


Run the following command to check the Terraform version:

```shell
terraform -version
```


## Task 2: Install Terraform TLS Provider


Edit the file titled `terraform.tf` to add the Terraform TLS provider.

`terraform.tf`

```hcl
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
    tls = {
      source  = "hashicorp/tls"
      version = "3.1.0"
    }
  }
}
```

Install the provider by performing a `terraform init`

```shell
terraform init
```

This informs Terraform that it will install the TLS provider for working with Transport Layer Security keys and certificates.

Validate the installation by running a `terraform version`

```shell
terraform version
```

```
Terraform v1.3.9
on windows_386
+ provider registry.terraform.io/hashicorp/aws v5.94.1
+ provider registry.terraform.io/hashicorp/tls v3.1.0
```

## Task 3: Creates a self-signed certificate with TLS Provider


Update the `main.tf` file with the followig configuration blocks for generating a TLS self signed certificate and saving the private key locally.

```hcl
resource "tls_private_key" "generated" {
  algorithm = "RSA"
}

resource "local_file" "private_key_pem" {
  content  = tls_private_key.generated.private_key_pem
  filename = "MyAWSKey.pem"
}
```

> Note: This example creates a self-signed certificate for a development environment. THIS IS NOT RECOMMENDED FOR PRODUCTION SERVICES.

Create the Keypair via Terraform

```shell
terraform apply
```


Validate you now have a self-signed private key inside your current working directory name `MyAWSKey.pem`

# 10 Lab: Terraform Taint and Replace

The terraform `taint` command allows for you to manually mark a resource for recreation. The `taint` command informs Terraform that a particular resource needs to be rebuilt even if there has been no configuration change for that resource. Terraform represents this by marking the resource as "tainted" in the Terraform state, in which case Terraform will propose to replace it in the next plan you create.

- Task 1: Manually mark a resource to be rebuilt by using the terraform `taint` command.
- Task 2: Observe a `remote-exec` provisoner failing, resulting in Terraform automatically tainting a resource.
- Task 3: Untaint a resource
- Task 4: Use the `-replace` option rather than `taint`

## Task 1: Manually mark a resource to be rebuilt by using the terraform `taint` command



There are some situations where we want to recreate a resource without modifying any terraform configuration. An example of this might be to rebuild a server and force it to rerun it's bootsrap process. This can be accomplished by manually "tainting" the resoruce.

### Step 1.1 - Create a new Web Server


Let's add a new webserver to our configuration that we can work on. Update your `main.tf` to include the new webserver.

```hcl
# Terraform Resource Block - To Build Web Server in Public Subnet
resource "aws_instance" "web_server" {
  ami                         = data.aws_ami.ubuntu.id
  instance_type               = "t3.micro"
  subnet_id                   = aws_subnet.public_subnets["public_subnet_1"].id
  security_groups             = [aws_security_group.vpc-ping.id, 
     aws_security_group.ingress-ssh.id, aws_security_group.vpc-web.id]
  associate_public_ip_address = true
  key_name                    = aws_key_pair.generated.key_name
  connection {
    user        = "ubuntu"
    private_key = tls_private_key.generated.private_key_pem
    host        = self.public_ip
  }

  # Leave the first part of the block unchanged and create our `local-exec` provisioner
  provisioner "local-exec" {
    command = "chmod 400 ${local_file.private_key_pem.filename}"
  }

  provisioner "remote-exec" {
    inline = [
      "sudo rm -rf /tmp",
      "sudo git clone https://github.com/hashicorp/demo-terraform-101 /tmp",
      "sudo sh /tmp/assets/setup-web.sh",
    ]
  }

  tags = {
    Name = "Web EC2 Server"
  }

  lifecycle {
    ignore_changes = [security_groups]
  }

}
```

Execute a `plan` and `apply` to build out the web server.

```shell
terraform validate
terraform plan
terraform apply
```

### Step 1.2 - Reference the Web Server



Now that that server has been built, let's validate it's resource ID. If you're unsure of the correct ID for the resource you want to taint, you can use `terraform state list`:

```shell
terraform state list
```


### Step 1.3 - Mark the webserver to be recreated with the `taint` command



We can the force the resource to be destroyed and recreated with the taint command:

```shell
terraform taint aws_instance.web_server
Resource instance aws_instance.web_server has been marked as tainted.
```

### Step 1.4 - Recreate the Web Server


Now we we execute a `terraform plan` and `terraform apply` we will notice that terraform has marked the resource to be recreated. This is because the resource has been tainted.

```shell
terraform plan
```

## Task 2: Observe a `remote-exec` provisoner failing, resulting in Terraform automatically tainting a resource


In addition to being able to `taint` a resource manually, Terraform will automatically taint a resource if it is configured with a creation-time provisioner and that provisioner fails. A tainted resource will be planned for destruction and recreation upon the next terraform apply. Terraform does this because a failed provisioner can leave a resource in a semi-configured state. Because Terraform cannot reason about what the provisioner does, the only way to ensure proper creation of a resource is to recreate it.

Modify the `remote-exec` provisioner within the `aws_instance.web_server` resource block to intentionally include a bad command.

```hcl
resource "aws_instance" "web_server" {
  ami             = data.aws_ami.ubuntu.id
  instance_type   = "t3.micro"
  subnet_id       = aws_subnet.public_subnets["public_subnet_1"].id
  security_groups = [aws_security_group.vpc-ping.id, aws_security_group.ingress-ssh.id, aws_security_group.vpc-web.id]
  key_name        = aws_key_pair.generated.key_name
  connection {
    user        = "ubuntu"
    private_key = tls_private_key.generated.private_key_pem
    host        = self.public_ip
  }
  associate_public_ip_address = true
  tags = {
    Name = "Web EC2 Server"
  }

  provisioner "local-exec" {
    command = "chmod 600 ${local_file.private_key_pem.filename}"
  }

  provisioner "remote-exec" {
    inline = [
      "exit 2",
      "git clone https://github.com/hashicorp/demo-terraform-101",
      "cp -a demo-terraform-101/. /tmp/",
      "sudo sh /tmp/assets/setup-web.sh",
    ]
  }
}
```

Manaully `taint` the resource and run a `terraform apply` and observe that the `remote-exec` provisioner fails.

```shell
terraform taint aws_instance.web_server
terraform apply
```

```shell
| Error: remote-exec provisioner error
|
|   with aws_instance.web_server,
|   on main.tf line 169, in resource "aws_instance" "web_server":
|  169:   provisioner "remote-exec" {
|
| error executing "/tmp/terraform_1714387465.sh": Process exited with status 2
```

This time Terraform automatically tainted the resource. You can see resource has been marked as `tainted` by looking at the resource using the `terraform show` command.

```shell
terraform state show aws_instance.web_server
```

```shell
# aws_instance.web_server: (tainted)
resource "aws_instance" "web_server" {
```

You will notice that because the `remote-exec` provisioner failed, Terraform automatically marked it as `tainted`. This informs Terraform that this resource needs to be rebuilt upon the next terraform apply.

## Untaint a resource

You can also `untaint` a resource by using the `terraform untaint` command.

```shell
terraform untaint aws_instance.web_server
```

```shell
Resource instance aws_instance.web_server has been successfully untainted.
```

This informs Terraform that this resource does not need to be rebuilt upon the next terraform apply.

## Task 4: Use the `-replace` option rather than `taint`

As of Terraform v0.15.2 and later the `taint` command is deprecated, because there are better alternatives available.

If your intent is to force replacement of a particular object even though there are no configuration changes that would require it, it is recommended to use the `-replace` option with terraform apply in place of the depcreated `taint` command.

Remove the offending error from the `remote-exec` provisioner and rebuild the web server resource using the `terraform apply -replace` command.

```hcl
provisioner "remote-exec" {
    inline = [
      "git clone https://github.com/hashicorp/demo-terraform-101",
      "cp -a demo-terraform-101/. /tmp/",
      "sudo sh /tmp/assets/setup-web.sh",
    ]
  }
```

```shell
terraform apply -replace="aws_instance.web_server"
```

```
Plan: 1 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes
```


Using the `-replace` command to rebuild a resource is the recommended approach moving forward.


-----
# 11 Lab: Terraform Import


We've already seen many benefits of using Terraform to build out our cloud infrastructure. But what if there are existing resources that we'd also like to manage with Terraform?

Enter `terraform import`.

With minimal coding and effort, we can add our resources to our configuration and bring them into state.

- Task 1: Prepare for a Terraform Import
- Task 2: Import the Resource in Terraform


## Task 1: Prepare for Import



> Note: This is most likely already configured in your `main.tf` from previous labs.

You must also have a destination resource to store state against. Add an empty resource block now. We will add an EC2 instance called "aws_linux".

```hcl
resource "aws_instance" "aws_linux" {}
```

We're now all set to import our instance into state!

## Task 3: Import the Resource into Terraform



Using the instance ID provided by your instructor, run the `terraform import` command now. The import command is comprised of four parts.

Example:

- `terraform` to call our binary
- `import` to specify the action to take
- `aws_instance.aws_linux` to specify the resource in our config file (`main.tf`) that this resource corresponds to
- `i-0bfff5070c5fb87b6` to specify the real-world resource (in this case, an AWS EC2 instance) to import into state

> **Note**: The resource name and unique identifier of that resource are unique to each configuration.

See what happens below when we've successfully run `terraform import <resource.name> <unique_identifier>`.

The `<unique_identifier>` is the ID you captured at the end of Task 1.

```
terraform import aws_instance.aws_linux i-0bfff5070c5fb87b6
aws_instance.linux: Importing from ID "i-0bfff5070c5fb87b6 "...
aws_instance.linux: Import prepared!
  Prepared aws_instance for import
aws_instance.linux: Refreshing state... [id=i-0bfff5070c5fb87b6]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.
```

Great! Our resource now exists in our state. But what happens if we were to run a plan against our current config?

```shell
terraform plan

  Error: Missing required argument

    on main.tf line 5, in resource "aws_instance" "linux":
     5: resource "aws_instance" "linux" {

  The argument "ami" is required, but no definition was found.


  Error: Missing required argument

    on main.tf line 5, in resource "aws_instance" "linux":
     5: resource "aws_instance" "linux" {

  The argument "instance_type" is required, but no definition was found.
```

We're missing some required attributes. How can we find those without looking at the console? Think back to our work with the workspace state. What commands will show us the information we need?

We know the exact resource to look for in our state, so let's query it using the `terraform state show` command.

```shell
terraform state show aws_instance.aws_linux
# aws_instance.aws_linux:
resource "aws_instance" "aws_linux" {
    ami                                  = "ami-013a129d325529d4d"
    arn                                  = "arn:aws:ec2:us-west-2:508140242758:instance/i-0bfff5070c5fb87b6"
...
```

Using the output from the above command, we can now piece together the minimum required attributes for our configuration. Add the required attributes to your resource block and rerun the apply.

```hcl
resource "aws_instance" "aws_linux" {
  ami           = "ami-013a129d325529d4d"
  instance_type = "t3.micro"
}
```

Your `ami` and `instance_type` may differ. Be sure to use the values provided in the previous step.

```
terraform plan
...
 # aws_instance.aws_linux will be updated in-place
  ~ resource "aws_instance" "aws_linux" {
        id                                   = "i-0bfff5070c5fb87b6"
        tags                                 = {}
      ~ tags_all                             = {
          + "Owner"      = "Acme"
          + "Provisoned" = "Terraform"
        }
        # (27 unchanged attributes hidden)
        # (6 unchanged blocks hidden)
    }
```

You've successfully imported **and** declared your existing resource into your Terraform configuration. Notice that Terraform wants to update the default tags for this instance based on the default tags we specified in previous labs.

To apply these default tags you can run a `terraform apply`

```shell
terraform apply
```

This verifies that you can now modify, update, or destroy this EC2 server using the traditional Terraform configuration and CLI commands now that it has been imported into Terraform.

You can now remove the item from your configuration as this server will no longer be required for future labs.

----- 
# 12 Lab: Debugging Terraform



- Task 1: Enable Logging
- Task 2: Set Logging Path
- Task 3: Disable Logging

## Task 1: Enable Logging



Terraform has detailed logs which can be enabled by setting the TF_LOG environment variable to any value. This will cause detailed logs to appear on stderr.

You can set TF_LOG to one of the log levels TRACE, DEBUG, INFO, WARN or ERROR to change the verbosity of the logs, with TRACE being the most verbose.

Linux

```shell
export TF_LOG=TRACE
```

PowerShell

```shell
$env:TF_LOG="TRACE"
```

Run Terraform Apply.

```shell
terraform apply
```

Example Output

```shell
2020/03/20 13:14:41 [INFO] backend/local: apply calling Apply
2020/03/20 13:14:41 [INFO] terraform: building graph: GraphTypeApply
2020/03/20 13:14:41 [TRACE] Executing graph transform *terraform.ConfigTransformer
2020/03/20 13:14:41 [TRACE] ConfigTransformer: Starting for path:
2020/03/20 13:14:41 [TRACE] Completed graph transform *terraform.ConfigTransformer with new graph:
  data.vsphere_compute_cluster.cluster (prepare state) - *terraform.NodeApplyableResource
  data.vsphere_datacenter.dc (prepare state) - *terraform.NodeApplyableResource
  data.vsphere_datastore.datastore (prepare state) - *terraform.NodeApplyableResource
  data.vsphere_network.network (prepare state) - *terraform.NodeApplyableResource
  data.vsphere_virtual_machine.windows_template (prepare state) - *terraform.NodeApplyableResource
  vsphere_tag.tag_release (prepare state) - *terraform.NodeApplyableResource
  vsphere_tag.tag_tier (prepare state) - *terraform.NodeApplyableResource
  vsphere_tag_category.category (prepare state) - *terraform.NodeApplyableResource
  vsphere_virtual_machine.windows_vm (prepare state) - *terraform.NodeApplyableResource
  ------
2020/03/20 13:14:41 [TRACE] Executing graph transform *terraform.DiffTransformer
```

## Task 2: Enable Logging Path


To persist logged output you can set TF_LOG_PATH in order to force the log to always be appended to a specific file when logging is enabled. Note that even when TF_LOG_PATH is set, TF_LOG must be set in order for any logging to be enabled.

```shell
export TF_LOG_PATH="terraform_log.txt"
```

PowerShell

```shell
$env:TF_LOG_PATH="terraform_log.txt"
```

Run terraform init to see the initialization debugging information.

```shell
terraform init -upgrade
```

Open the `terraform_log.txt` to see the contents of the debug trace for your terraform init. Experiment with removing the provider stanza within your Terraform configuration and run a `terraform plan` to debug how Terraform searches for where a provider is located.

## Task 3: Disable Logging


Terraform logging can be disabled by clearing the appropriate environment variable.

Linux

```shell
export TF_LOG=""
```

PowerShell

```shell
$env:TF_LOG=""
```
# 13 Lab: Terraform Workspaces - OSS


Those who adopt Terraform typically want to leverage the principles of DRY (Don't Repeat Yourself) development practices. One way to adopt this principle with respect to IaC is to utilize the same code base for different environments (development, quality, production, etc.)

Workspaces is a Terraform feature that allows us to organize infrastructure by environments and variables in a single directory.

Terraform is based on a stateful architecture and therefore stores state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures.

The persistent data stored in the state belongs to a Terraform workspace. Initially the backend has only one workspace, called "default", and thus there is only one Terraform state associated with that configuration.

- Task 1: Using Terraform Workspaces (Open Source)
- Task 2: Create a new Terraform Workspace for Development State
- Task 3: Deploy Infrastructure within the Terraform development workspace
- Task 4: Changing between Workspaces
- Task 5: Utilizing the ${terraform.workspace} interpolation sequence within your configuration

## Task 1: Using Terraform Workspaces (Open Source)



Terraform starts with a single workspace named "default". This workspace is special both because it is the default and also because it cannot ever be deleted. If you've never explicitly used workspaces, then you've only ever worked on the "default" workspace.

You can check the Terraform workspace you are in with the `terraform workspace` command.

```shell
terraform workspace show
default
```

To see a list of the options you have within the terraform workspace command issue a `terraform workspace -help`

```shell
terraform workspace -help

Usage: terraform [global options] workspace

  new, list, show, select and delete Terraform workspaces.

Subcommands:
    delete    Delete a workspace
    list      List Workspaces
    new       Create a new workspace
    select    Select a workspace
    show      Show the name of the current workspace
```

We will utilize the current `default` workspace to store the state information for our `us-east-1` aws region.

## Task 2: Create a new Terraform Workspace for Development State



Leveraging the same code base let's perform a development deployment into the `us-west-2` region while not affecting the infrastructure that was built out in our `default` workspace.

To begin, let's create a new terraform workspace called `development`

```shell
terraform workspace new development

Created and switched to workspace "development"!

You're now on a new, empty workspace. Workspaces isolate their state, so if you run "terraform plan" Terraform will not see any existing state
for this configuration.
```

You can validate that we are no longer in the `default` workspace by issuing a `terraform workspace show` command

```shell
terraform workspace show
development
```

You can also see that the state is empty for this workspace by issuing a `terraform show`

```shell
terraform show
No state.
```

## Task 3: Deploy Infrastructure within the Terraform development workspace


Modify your `main.tf` to change the `region` of the aws `provider` block to `us-west-2`.

`main.tf`

```hcl
# Configure the AWS Provider
provider "aws" {
  region = "us-west-2"
  default_tags {
    tags = {
      Owner      = "depi"
      Provisoned = "Terraform"
    }
  }
}
```

Save your file and issue a `terraform plan` to see Terraform's dry run for execution

```shell
terraform plan
Plan: 26 to add, 0 to change, 0 to destroy.
```

Because the state information is new for the `development` workspace, Terraform will go and deploy all of the infrastructure declared in the configuration now into `us-west-2` which is our development region.

```shell
terraform apply

Do you want to perform these actions in workspace "development"?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes
```

## Task 4: Changing between Workspaces



To move between terraform workspaces you can use the `terraform workspace` command.

To move back to the infrastructure residing in `us-east-1` issue:

```shell
terraform workspace select default
```

To move back to the infrastructure residing in `us-west-2` issue:

```shell
terraform workspace select development
```

You can issue a `terraform show` in either workspace to see the resources that each of the workspaces is managing.

## Task 5: Utilizing the ${terraform.workspace} interpolation sequence within your configuration



Now that we see the benefit of isolating our resource state information using terraform workspaces, we may wish to reflect the workspace name information into our code base.

Within your Terraform configuration, you may include the name of the current workspace using the ${terraform.workspace} interpolation sequence.

Modify the environment default tag for `main.tf` inside the AWS provider to reflect the terraform workspace name

```hcl
provider "aws" {
  region = "us-west-2"
  default_tags {
    tags = {
      Environment = terraform.workspace
      Owner       = "TF Hands On Lab"
      Project     = "Infrastructure as Code"
      Terraform   = "true"
    }
  }
}
```

```
  # aws_vpc.vpc will be updated in-place
  ~ resource "aws_vpc" "vpc" {
        id                               = "vpc-00d26110d48784808"
      ~ tags                             = {
          ~ "Environment" = "demo_environment" -> "development"
            # (2 unchanged elements hidden)
        }
      ~ tags_all                         = {
          ~ "Environment" = "demo_environment" -> "development"
            # (2 unchanged elements hidden)
        }
        # (14 unchanged attributes hidden)
    }
```

## Reference

[Terraform Workflow](https://www.terraform.io/docs/cloud/guides/recommended-practices/part1.html)


-----
# 14 Terraform Modules


Terraform configuration can be separated out into modules to better organize your configuration. This makes your code easier to read and reusable across your organization. A Terraform module is very simple: any set of Terraform configuration files in a folder is a module. Modules are the key ingredient to writing reusable and maintainable Terraform code. Complex configurations, team projects, and multi-repository codebases will benefit from modules. Get into the habit of using them wherever it makes sense.

- Task 1: Create a local Terraform module
- Task 2: Reference a module within Terraform Configuration
- Task 3: Terraform module reuse

## Task 1: Create a local Terraform Module


A Terraform module is just a set of Terraform configuration files. Modules are just Terraform configurations inside a folder - there's nothing special about them. In fact, the code you’ve been writing so far is a module: the root module. For this lab, we'll create a local module for a new server configuration.

### Step 1.1



Create a new directory called `server` in your `/workspace/terraform` directory and create a new file inside of it called `server.tf`.

### Step 1.2


Edit the file `server/server.tf`, with the following contents:

```hcl
variable "ami" {}
variable "size" {
  default = "t3.micro"
}
variable "subnet_id" {}
variable "security_groups" {
  type = list(any)
}
resource "aws_instance" "web" {
  ami                    = var.ami
  instance_type          = var.size
  subnet_id              = var.subnet_id
  vpc_security_group_ids = var.security_groups

  tags = {
    "Name"        = "Server from Module"
    "Environment" = "Training"
  }
}

output "public_ip" {
  value = aws_instance.web.public_ip
}

output "public_dns" {
  value = aws_instance.web.public_dns
}
```

### Step 1.3


In your root configuration (also called your root module) `/workspace/terraform/main.tf`, we can call our new `server` module with a Terraform module block. Remember that terraform only works with the configuration files that are in it's current working directory. Modules allow us to reference Terraform configuration that lives outside of our working directory. In this case we will incorporate all configuration that is both inside our working directory (root module) and inside the `server` directory (child module).

```hcl
module "server" {
  source          = "./server"
  ami             = data.aws_ami.ubuntu.id
  subnet_id       = aws_subnet.public_subnets["public_subnet_3"].id
  security_groups = [
    aws_security_group.vpc-ping.id,
    aws_security_group.ingress-ssh.id,
    aws_security_group.vpc-web.id
  ]
}
```

### Step 1.4 Install and Apply Module

Now run `terraform init` to install the module. Terraform configuration files located within modules are pulled down by Terraform during initialization, so any time you add or update a module version you must run a `terraform init`.

```shell
terraform init
```

You can see that our configuaration now depends on this module to be installed and used by using the `terraform providers` command.

```shell
terraform providers

Providers required by configuration:
.
|-- provider[registry.terraform.io/hashicorp/aws] ~> 3.0
|-- provider[registry.terraform.io/hashicorp/http] 2.1.0
|-- provider[registry.terraform.io/hashicorp/random] 3.1.0
|-- provider[registry.terraform.io/hashicorp/local] 2.1.0
|-- provider[registry.terraform.io/hashicorp/tls] 3.1.0
|-- module.server
    |-- provider[registry.terraform.io/hashicorp/aws]

Providers required by state:

    provider[registry.terraform.io/hashicorp/aws]

    provider[registry.terraform.io/hashicorp/local]

    provider[registry.terraform.io/hashicorp/random]

    provider[registry.terraform.io/hashicorp/tls]
```

Run `terraform apply` to create a new server using the `server` module. It may take a few minutes for the server to be built using the module.

```
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

module.server.aws_instance.web: Creating...
module.server.aws_instance.web: Still creating... [10s elapsed]
```

## Task 2: Reference a Module within Terraform Configuration



When used, Terraform modules will be listed within Terraform's state file and can be referenced using their module name.

```shell
terraform state list

# Resource defined in root module/working directory
aws_instance.web_server

# Resource defined in `server` module
module.server.aws_instance.web
```

We can look at all the details of the server created using our `server` module.

```shell
terraform state show module.server.aws_instance.web
```

We can add two output blocks to our `main.tf` to report back the IP and DNS information from our `server` module. Notice how Terraform references (interpolation syntax) information about the server build from a module.

```hcl
output "public_ip" {
  value = module.server.public_ip
}

output "public_dns" {
  value = module.server.public_dns
}
```

## Task 3: Reuse the module to build a server in a different subnet


One of the benefits of Terraform modules is that they can easily be reused across your organization. Let's use our local module again to build out another server in a seperate subnet.

[![Desired Infrastructure](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/obj-1-desired-infrastructure.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/obj-1-desired-infrastructure.png)

```hcl
module "server_subnet_1" {
  source          = "./server"
  ami             = data.aws_ami.ubuntu.id
  subnet_id       = aws_subnet.public_subnets["public_subnet_1"].id
  security_groups = [
    aws_security_group.vpc-ping.id,
    aws_security_group.ingress-ssh.id,
    aws_security_group.vpc-web.id
  ]
}
```

Run `terraform apply` to create a new server using the `server` module. It may take a few minutes for the server to be built using the module.

```
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

module.server_subnet_1.aws_instance.web: Creating...
module.server_subnet_1.aws_instance.web: Still creating... [10s elapsed]
```

You

```hcl
output "public_ip_server_subnet_1" {
  value = module.server_subnet_1.public_ip
}

output "public_dns_server_subnet_1" {
  value = module.server_subnet_1.public_dns
}
```

# 15 Terraform Module Sources



Modules can be sourced from a number of different locations, including both local and remote sources. The Terraform Module Registry, HTTP urls and S3 buckets are examples of remote sources, while folders and subfolders are examples of local sources. Support for various module sources allow you to include Terraform configuration from a variety of locations while still providing proper organization of code.

- Task 1: Source a local Terraform module
- Task 2: Explore the Public Module Registry and install a module
- Task 3: Source a module from GitHub

## Task 1: Source a local Terraform module



While not required, local modules are commonly saved in a folder named `modules`, and each module is named for its respective function inside that folder. In support of this practice let's move our server module into a `modules` directory and observer the impact.

### Step 1.1 - Refactor to use local modules directory



Create a `modules` directory and move your `server` directory into this directory as a subdirectory.

```shell
|-- modules
|   |-- server
|       |-- server.tf
```

Update the `source` of your module block to point to the modified source.

```
module "server" {
  source          = "./modules/server"
  ami             = data.aws_ami.ubuntu.id
  subnet_id       = aws_subnet.public_subnets["public_subnet_3"].id
  security_groups = [aws_security_group.vpc-ping.id, 
  aws_security_group.ingress-ssh.id, 
  aws_security_group.vpc-web.id]
}

module "server_subnet_1" {
  source          = "./modules/server"
  ami             = data.aws_ami.ubuntu.id
  subnet_id       = aws_subnet.public_subnets["public_subnet_1"].id
  security_groups = [aws_security_group.vpc-ping.id, 
  aws_security_group.ingress-ssh.id, 
  aws_security_group.vpc-web.id]
}
```

Any time that the source of a module is update, the working directory (root module) needs to be reintilized.

```shell
terraform init
```

We can follow that by issuing a `terraform plan` to make sure that moving our module source did not incur any changes to our infrastructure. This is expected because we have not changed any of the Terraform configuration, just the source of our module that was moved.

```shell
terraform plan

No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no differences, so no changes are
needed.
```

### Step 1.2 - Create a new module source locally


Within our `modules` directory let's create another directory where we will include some enhancements to our `server` module. We will create these enhancments in a new directory called `web_server` and make a copy of our `server.tf` folder to this directory.

```shell
|-- modules
|   |-- server
|       |-- server.tf
|   |-- web_server
|       |-- server.tf
```

Let's update the `server.tf` inside our our `web_server` directory to now to allow us to provision our web application.

```
variable "ami" {}
variable "size" {
  default = "t3.micro"
}
variable "subnet_id" {}

variable "user" {}

variable "security_groups" {
  type = list(any)
}

variable "key_name" {

}

variable "private_key" {

}

resource "aws_instance" "web" {
  ami                         = var.ami
  instance_type               = var.size
  subnet_id                   = var.subnet_id
  vpc_security_group_ids      = var.security_groups
  associate_public_ip_address = true
  key_name                    = var.key_name
  connection {
    user        = var.user
    private_key = var.private_key
    host        = self.public_ip
  }


  provisioner "remote-exec" {
    inline = [
      "sudo rm -rf /tmp",
      "sudo git clone https://github.com/hashicorp/demo-terraform-101 /tmp",
      "sudo sh /tmp/assets/setup-web.sh",
    ]
  }

  tags = {
    "Name"        = "Web Server from Module"
    "Environment" = "Training"
  }

}

output "public_ip" {
  value = aws_instance.web.public_ip
}

output "public_dns" {
  value = aws_instance.web.public_dns
}
```

### Step 1.2 - Update our `server_subnet_1` module to use the new `web_server` source



Let's now update our `server_subnet_1` module to use the new web_server source configuaration by updating the `source` arguement.

```hcl
module "server_subnet_1" {
  source          = "./modules/web_server"
  ami             = data.aws_ami.ubuntu.id
  key_name        = aws_key_pair.generated.key_name
  user            = "ubuntu"
  private_key     = tls_private_key.generated.private_key_pem
  subnet_id       = aws_subnet.public_subnets["public_subnet_1"].id
  security_groups = [aws_security_group.vpc-ping.id, 
  aws_security_group.ingress-ssh.id, 
  aws_security_group.vpc-web.id]
}
```

Any time that the source of a module is updated or added to our configuration, the working directory needs to be reintilized.

```shell
terraform init
```

You can make sure that the syntax is validate and formated properly by running the following:

```shell
terraform validate
terraform fmt -recursive
```

### Step 1.2 - Apply our configuration with the updated module

Now that we have updated the source of our `server_subnet_1` module, we are ready to use it. Let's first see the ramifications of this change via a `terraform plan`

```shell
terraform plan
```

You will see that because we are now updating our server configuration via the new module to specify a key pair, that the server will need to be rebuilt.

```
Plan: 1 to add, 0 to change, 1 to destroy.
```

```shell
terraform apply
```

Now we will see that our new `web_server` module deploys a web application when used, versus the `server` module which simply deploys a generic server. We can of course switch between which modules are used by updating the `source` argument of our module - just be sure to run a `terraform plan` after making any changes to fully understand the impact of that change.

## Task 2: Explore the Public Module Registry and install a module

Terraform Public Registry is an index of modules shared publicly. This public registry is the easiest way to get started with Terraform and find modules created by others in the community. You can also use a private registry as a feature of Terraform Cloud/Terraform Enterprise.

Modules on the public Terraform Registry can be sourced using a registry source address of the form //, with each module's information page on the registry site including the exact address to use.

We will use the AWS Autoscaling module to deploy an AWS Autoscaling group to our environment. Update your `main.tf` to include this module from the Terraform Module Registry.

```hcl
module "autoscaling" {
  source  = "terraform-aws-modules/autoscaling/aws"
  version = "8.0.1"
 
  # Autoscaling group
  name = "myasg"
 
  vpc_zone_identifier = [aws_subnet.private_subnets["private_subnet_1"].id, 
  aws_subnet.private_subnets["private_subnet_2"].id, 
  aws_subnet.private_subnets["private_subnet_3"].id]
  min_size            = 0
  max_size            = 1
  desired_capacity    = 1
 
  # Launch template
  image_id      = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"
  instance_name = "asg-instance"
 
  tags = {
    Name = "Web EC2 Server 2"
  }
 
}
```

Any time that the source of a module is updated or added to our configuration, the working directory needs to be reintilized.

```shell
terraform init
```

We can follow that by issuing a `terraform plan` to see that additional resources that will be added by using the module.

```shell
terraform plan
```

Once we are happy with how the module is behaving we can issue a `terraform apply`

```shell
terraform apply
```

## Task 3: Source a module from GitHub



Another source of modules that we can use are those that are published directly on GitHub. Terraform will recognize unprefixed github.com URLs and interpret them automatically as Git repository sources. Let's update the `source` of our autoscaling group module from the Public Module registry to use github.com instead. This will require us to remove the `version` argument from our module block.

```
module "autoscaling" {
  source = "github.com/terraform-aws-modules/terraform-aws-autoscaling?ref=v4.9.0"

  # Autoscaling group
  name = "myasg"

  vpc_zone_identifier = [aws_subnet.private_subnets["private_subnet_1"].id,
  aws_subnet.private_subnets["private_subnet_2"].id, 
  aws_subnet.private_subnets["private_subnet_3"].id]
  min_size            = 0
  max_size            = 1
  desired_capacity    = 1

  # Launch template
  use_lt    = true
  create_lt = true

  image_id      = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"

  tags_as_map = {
    Name = "Web EC2 Server 2"
  }

}
```

These GitHub schemes are treated as convenient aliases for the general Git repository address scheme, and so they obtain credentials in the same way and support the ref argument for selecting a specific revision. You will need to configure credentials in particular to access private repositories.

Now that our module source has been change we must reinitialize our working directory, plan and apply.

```shell
terraform init
```

We can follow that by issuing a `terraform plan` to see that additional resources that will be added by using the module.

```shell
terraform plan
```

Once we are happy with how the module is behaving we can issue a `terraform apply`

```shell
terraform apply
```

# 16 Terraform Modules - Public Module Registry


Hashicorp maintains a public registry that helps you to consume Terraform modules from others. The Terraform Public Registry is an index of modules shared publicly and is the easiest way to get started with Terraform and find modules created by others in the community. It includes support for module versioning and searchable and filterable list of available modules for quickly deploying common infrastructure configurations.

Modules on the public Terraform Registry can be sourced using a registry source address of the form `<NAMESPACE>/<NAME>/<PROVIDER>`, with each module's information page on the registry site including the exact address to use.

- Task 1: Consuming Modules from the Terraform Module Registry
- Task 2: Exploring other modules from the Terraform Module Registry

## Task 1: Consuming Modules from the Terraform Module Registry



In previous labs we begain using modules from the Terraform Public Module Registry, including the auto scaling module. Let's add an S3 bucket to our configuration using the S3 public module.

`main.tf`

```hcl
module "s3-bucket" {
  source  = "terraform-aws-modules/s3-bucket/aws"
  version = "2.11.1"
}

output "s3_bucket_name" {
  value = module.s3-bucket.s3_bucket_bucket_domain_name
}
```

```shell
terraform init
terraform plan


  # module.s3-bucket.aws_s3_bucket.this[0] will be created
  + resource "aws_s3_bucket" "this" {
      + acceleration_status         = (known after apply)
      + acl                         = "private"
      + arn                         = (known after apply)
      + bucket                      = (known after apply)
      + bucket_domain_name          = (known after apply)
      + bucket_regional_domain_name = (known after apply)
      + force_destroy               = false
      + hosted_zone_id              = (known after apply)
      + id                          = (known after apply)
      + region                      = (known after apply)
      + request_payer               = (known after apply)
      + tags_all                    = (known after apply)
      + website_domain              = (known after apply)
      + website_endpoint            = (known after apply)

      + versioning {
          + enabled    = (known after apply)
          + mfa_delete = (known after apply)
        }
    }

  # module.s3-bucket.aws_s3_bucket_public_access_block.this[0] will be created
  + resource "aws_s3_bucket_public_access_block" "this" {
      + block_public_acls       = false
      + block_public_policy     = false
      + bucket                  = (known after apply)
      + id                      = (known after apply)
      + ignore_public_acls      = false
      + restrict_public_buckets = false
    }
```

```shell
terraform apply

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

s3_bucket_name = "terraform-20211220113638832700000001.s3.amazonaws.com"
```

## Task 2: Exploring other modules from the Terraform Module Registry


Another useful module that we may wish to utilize is the [VPC Module](https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws/latest). This is a simple Terraform module for creating VPC resource in AWS

Let's this to our configuration inside the `main.tf` of our root module:

```hcl
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"

  name = "my-vpc-terraform"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b", "us-east-1c"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway = true
  enable_vpn_gateway = true

  tags = {
    Name = "VPC from Module"
    Terraform = "true"
    Environment = "dev"
  }
}
```

```shell
terraform init
terraform plan
terraform apply
```

[![VPC Module](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/module_vpc.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/module_vpc.png)

You can see that we can simplify our code base through the use of modules. The last two examples showcased building out an entire AWS VPC with private and public subnets, route tables, NAT gateways, VPN and Internet Gateways along with an S3 Bucket all via Terraform modules.

# 17 Terraform Modules Inputs and Outputs


To make a Terraform module configurable you can add input parameters to the module. These are defined within the module using input variables. A module can also return values to the configuration that called the module. These module returns or outputs are defined using terraform output blocks.

- Task 1: Refactor module using code organization principles
- Task 2: Required and Optional Module inputs
- Task 3: Module outputs and returns
- Task 4: Reference module outputs

## Task 1: Refactor module using code organization principles


You can create a module with a single .tf file, or use any other file structure you like. Modules can be a bit daunting at first. We are suddenly working with a number of files in different file hierarchies, and those files are referencing each other in a few different ways. An example of this can be found in the diagram below:

[![](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/module-structure.png)

The example modules contain the following files:

`main.tf` will contain the main set of configuration for your module. You can also create other configuration files and organize them however makes sense for your project.

`variables.tf` will contain the variable definitions for your module. When your module is used by others, the variables will be configured as arguments in the module block. Since all Terraform values must be defined, any variables that are not given a default value will become required arguments. Variables with default values can also be provided as module arguments, overriding the default value.

`outputs.tf` will contain the output definitions for your module. Module outputs are made available to the configuration using the module, so they are often used to pass information about the parts of your infrastructure defined by the module to other parts of your configuration.

### Step 1.1 - Refactor the server module

Our `server` module is very simplistic, and we want to incorporate the code organization principles to follow the file structure above. Create three new files inside the `server` folder: `main.tf`, `variables.tf`, `outputs.tf`

Copy the appropriate code out of the `server.tf` and place it into these appropriate files:

`main.tf`

```hcl
resource "aws_instance" "web" {
  ami                    = var.ami
  instance_type          = var.size
  subnet_id              = var.subnet_id
  vpc_security_group_ids = var.security_groups

  tags = {
    "Name"        = "Server from Module"
    "Environment" = "Training"
  }
}
```

`variables.tf`

```hcl
variable "ami" {}
variable "size" {
  default = "t3.micro"
}
variable "subnet_id" {}
variable "security_groups" {
  type = list(any)
}
```

`outputs.tf`

```hcl
output "public_ip" {
  value = aws_instance.web.public_ip
}

output "public_dns" {
  value       = aws_instance.web.public_dns
}
```

You can run a `terraform init` along with a `terraform plan` and there should be no changes if we refactored the module correctly.

```shell
terraform init
terraform plan
```

## Task 2: Module required and optional inputs



Variables within modules work almost exactly the same way that they do for the root module. When you run a Terraform command on your root configuration, there are various ways to set variable values, such as passing them on the commandline, or with a .tfvars file. When using a module, variables are set by passing arguments to the module in your configuration. You will set some of these variables when calling this module from your root module's main.tf.

Variables defined in modules that aren't given a default value are required, and so must be set whenever the module is used. Comment out the `size` variable within the `server` module to make it required.

`variables.tf`

```
variable "ami" {}
variable "size" {
  # default = "t3.micro"
}
variable "subnet_id" {}
variable "security_groups" {
  type = list(any)
}
```

Run a `terraform validate` from the root module/working directory and notice that the module now requires the `size` argument to be passed into the module block, because it is now required.

```shell
terraform validate

|Error: Missing required argument
|
|  on main.tf line 316, in module "server":
| 316: module "server" {
|
|The argument "size" is required, but no definition was found.

```

Update the `server` module block to know specify the new required argument: `size`

```hcl
module "server" {
  source          = "./modules/server"
  ami             = data.aws_ami.ubuntu.id
  size            = "t3.micro"
  subnet_id       = aws_subnet.public_subnets["public_subnet_3"].id
  security_groups = [aws_security_group.vpc-ping.id, aws_security_group.ingress-ssh.id, aws_security_group.vpc-web.id]
}
```

Validate that the all required inputs into the `server` module block have been satisfied.

```shell
terraform validate
Success! The configuration is valid.
```

## Task 3: Module outputs and returns

Like variables, outputs in modules perform the same function as they do in the root module but are accessed in a different way. A module's outputs can be accessed as read-only attributes on the module object, which is available within the configuration that calls the module. You can reference these outputs in expressions as `module.<MODULE NAME>.<OUTPUT NAME>.`

Outputs are required for common modules that define resources. Variables and outputs are used to infer dependencies between modules and resources. Without any outputs we cannot properly order your module in relation to their Terraform configurations.

We can add a return to our `server` module by adding an output block within the module. Add a `size` variable within the `outputs.tf` of our `server` module.

`output.tf`

```hcl
output "public_ip" {
  description = "IP Address of server built with Server Module"
  value       = aws_instance.web.public_ip
}

output "public_dns" {
  description = "DNS Address of server built with Server Module"
  value       = aws_instance.web.public_dns
}

output "size" {
  description = "Size of server built with Server Module"
  value       = aws_instance.web.instance_type
}
```

Add an output inside the `main.tf` of our working directory to reference the new output provided by the module.

```hcl
output "size" {
  value = module.server.size
}
```

```shell
terraform init
terraform apply
```

Outputs should have meaningful descriptions you should make an effort to output all the useful values root modules would want to reference or share with modules. Particularly for open source or heavily used modules, expose all outputs that have potential for consumption.

## Task 4: Reference module outputs

In order to reference items that are returned by modules (by the module's `outputs.tf` file) you must use the interpolation syntax referring to the output name returned by the module. Eg: `module.server.public_ip`

`outputs.tf` of server module

```hcl
output "public_ip" {
  description = "IP Address of server built with Server Module"
  value       = aws_instance.web.public_ip
}
```

Refering to the `public_ip` of the server module within the root module:

`main.tf` of root module:

```hcl
output "public_ip" {
  value = module.server.public_ip
}
```

Notice that both output blocks have an output named `public_ip`, but their values reference a different interpolation. The output within the module itself references the value of the `public_ip` argument of the resource itself, while the output within the root module/working directory's configuration references the value of `public_ip` returned by the module.


# 18 Terraform Module Scope


Deciding what infrastructure to include is the one of the most challenging aspects about creating a new Terraform module.

Modules should be opinionated and designed to do one thing well. If a module's function or purpose is hard to explain, the module is probably too complex. When initially scoping your module, aim for small and simple to start.

- Task 1: Resources within Child Modules
- Task 2: Scoping Module Inputs and Outputs
- Task 3: Reference Child Module Outputs
- Task 4: Invalid Module References

## Task 1: Resources within Child Modules


In principle any combination of resources and other constructs can be factored out into a module, but over-using modules can make your overall Terraform configuration harder to understand and maintain, so we recommend moderation. A good module should raise the level of abstraction by describing a new concept in your architecture that is constructed from resource types offered by providers.

Let's take a closer look at the auto scaling group module that we are calling to further understand which resources are used to construct the module. Inside our `main.tf` we can see that the autoscaling module we are calling is being sourced from the [Terraform Public Module registry](https://registry.terraform.io/modules/terraform-aws-modules/autoscaling/aws/latest), and we are passing 10 inputs into the module.

`main.tf`

```hcl
module "autoscaling" {
  source  = "terraform-aws-modules/autoscaling/aws"
  version = "8.0.1"
 
  # Autoscaling group
  name = "myasg"
 
  vpc_zone_identifier = [aws_subnet.private_subnets["private_subnet_1"].id, 
  aws_subnet.private_subnets["private_subnet_2"].id, 
  aws_subnet.private_subnets["private_subnet_3"].id]
  min_size            = 0
  max_size            = 1
  desired_capacity    = 1
 
  # Launch template
  image_id      = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"
 
  tags = {
    Name = "Web EC2 Server 2"
  }
 
}
```

[![Autoscaling Module](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/autoscale_scope.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/autoscale_scope.png)

This module combines four different AWS resources, accepts up to 86 inputs and returns 20 possible outputs. It also has a dependency on the AWS provider.

[![Autoscaling Module](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/autoscale_scope_resources.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/autoscale_scope_resources.png)

```
aws_autoscaling_group
aws_autoscaling_schedule
aws_launch_configuration
aws_launch_template
```

Execute a `terraform init` and `terraform apply` to build out the infrastructure including the Auto Scaling group module. View the items that this module built by running a `terraform state list`

```hcl
terraform state list

module.autoscaling.data.aws_default_tags.current
module.autoscaling.aws_autoscaling_group.this[0]
module.autoscaling.aws_launch_template.this[0]
```

This module built out an autoscaling group and launch template as well as looked up default tags via a data block. You will notice that while this module could have built out more resources, these items were all that needed based on the configuration we passed into the module.

## Task 2: Scoping Module Inputs and Outputs


When looking at the scope of a module block, this diagram provides a helpful way to understand the relationship between root modules and child modules.

[![](https://github.com/btkrausen/hashicorp/raw/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/fileStructure-4.png)](https://github.com/btkrausen/hashicorp/blob/master/terraform/Hands-On%20Labs/Section%2006%20-%20Interact%20with%20Terraform%20Modules/img/fileStructure-4.png)

Modules are simply terraform configuration files that have optional/required inputs and will return a specified number of outputs. The configuration within the module can be akin to a black box, as the module is abstracting away the configuration blocks which it contains. The module code for child modules is still typically availabe for us to review if we like, but not required to be able to get resources built out without having to worry about all of the details within the child module.

When creating a module, consider which resource arguments to expose to module end users as input variables. In our example, the autoscaling module provides up to 86 different inputs that can be used for configuring the ASG. Variables declared in child module map to arguments within root module block, where outputs declared in child module map to attributes that can used by the root module. You should also consider which values to add as outputs, since outputs are the only supported way for users to get information about resources configured by the module. In our example, the autoscaling module provides 20 available outputs that the module will return.

To view the outputs returned by our autosclaing module and their values you can issue the following:

```shell
terraform console

> module.autoscaling

{
  "autoscaling_group_arn" = "arn:aws:autoscaling:us-east-1:508140242758:autoScalingGroup:2a33891c-6c8b-4434-9386-bf1f1574523d:autoScalingGroupName/myasg-20211218123153166900000003"
  "autoscaling_group_availability_zones" = toset([
    "us-east-1b",
    "us-east-1c",
    "us-east-1d",
  ])
  "autoscaling_group_default_cooldown" = 300
  "autoscaling_group_desired_capacity" = 1
  "autoscaling_group_health_check_grace_period" = 300
  "autoscaling_group_health_check_type" = "EC2"
  "autoscaling_group_id" = "myasg-20211218123153166900000003"
  "autoscaling_group_load_balancers" = toset(null) /* of string */
  "autoscaling_group_max_size" = 1
  "autoscaling_group_min_size" = 0
  "autoscaling_group_name" = "myasg-20211218123153166900000003"
  "autoscaling_group_target_group_arns" = toset(null) /* of string */
  "autoscaling_group_vpc_zone_identifier" = toset([
    "subnet-01dcabb8c2474bd4f",
    "subnet-0d29fb83c81f6278b",
    "subnet-0e509d03fb7841876",
  ])
  "autoscaling_schedule_arns" = (known after apply)
  "launch_configuration_arn" = (known after apply)
  "launch_configuration_id" = (known after apply)
  "launch_configuration_name" = (known after apply)
  "launch_template_arn" = "arn:aws:ec2:us-east-1:508140242758:launch-template/lt-0bdc46cf90ccdad50"
  "launch_template_id" = "lt-0bdc46cf90ccdad50"
  "launch_template_latest_version" = 1
}
```

## Task 3: Reference Child Module Outputs



In order to reference items that are returned by modules (by the child module's `outputs.tf` file) you must use the interpolation syntax referring to the output name returned by the module. Eg: `module.autoscaling.autoscaling_group_max_size`

Refering to the `autoscaling_group_max_size` of the autoscaling module within the root module:

Let's add an output block inside the `main.tf` of root module to showcase the `autoscaling_group_max_size` returned by the autoscaling group child module.

```hcl
output "asg_group_size" {
  value = module.autoscaling.autoscaling_group_max_size
}
```

```shell
terraform apply

Outputs:
asg_group_size = 1
```

## Task 4: Invalid Module References


Module outputs are the only supported way for users to get information about resources configured within the child module. Individual resource arguments are not accessible outside the child module.

If we look at the `outputs.tf` of autoscaling group child module we can see the one of the items returned by this module is the `autoscaling_group_max_size`. Looking at the code this is returned based on the value of the `aws_autoscaling_group.this[0].max_size` resource. We don't need to be too occupied with how this value is set since the module is abstracting away these complexities for us.

```hcl
output "autoscaling_group_max_size" {
  description = "The maximum size of the autoscale group"
  value       = try(aws_autoscaling_group.this[0].max_size, "")
}
```

All we need to be concerned about is the `autoscaling_group_max_size` output that is returned. In fact, unless a child module provides us with an output that we can consume we will not be able to reference items within the child module. Individual resource arguments are not accessible outside the child module.

```
module "my-module" {
  # Source can be any URL or file path
  source = "../../my-module"

  argument_1 = "value"
  argument_2 = "value"
}

# Valid
output "example" {
  value = module.my-module.public_ip
}

# Invalid
output "example" {
  value = module.my-module.aws_instance.db.public_ip
}
```

To showcase this, create an output block within the root module `main.tf` that references a resource argument directly within the autoscaling child module.

`main.tf`

```hcl
output "asg_group_size" {
  value = module.autoscaling.aws_autoscaling_group.this[0].max_size
}
```

```shell
terraform validate

|Error: Unsupported attribute
|
|  on main.tf line 382, in output "asg_group_size":
| 382:   value = module.autoscaling.aws_autoscaling_group.this[0].max_size
|    |---------------
|    |module.autoscaling is a object, known only after apply
|
|This object does not have an attribute named "aws_autoscaling_group".
```

Now correct this to reference the valid output returned by the module:

```hcl
output "asg_group_size" {
  value = module.autoscaling.autoscaling_group_max_size
}
```

```shell
teraform validate

Success! The configuration is valid.
```

It is therefore a best practice when creating terraform modules to output as much information as possible, even if you do not currently have a use for it. This will make your module more useful for end users who will often use multiple modules, using outputs from one module as inputs for the next.

## Notes about building Terraform Modules
-+
When building a module, consider three areas:

- **Encapsulation:** Group infrastructure that is always deployed together. Including more infrastructure in a module makes it easier for an end user to deploy that infrastructure but makes the module's purpose and requirements harder to understand
- **Privileges:** Restrict modules to privilege boundaries. If infrastructure in the module is the responsibility of more than one group, using that module could accidentally violate segregation of duties. Only group resources within privilege boundaries to increase infrastructure segregation and secure your infrastructure
- **Volatility:** Separate long-lived infrastructure from short-lived. For example, database infrastructure is relatively static while teams could deploy application servers multiple times a day. Managing database infrastructure in the same module as application servers exposes infrastructure that stores state to unnecessary churn and risk.

A simple way to get start with creating modules is to:

- Always aim to deliver a module that works for at least 80% of use cases.
- Never code for edge cases in modules. An edge case is rare. A module should be a reusable block of code.
- A module should have a narrow scope and should not do multiple things.
- The module should only expose the most commonly modified arguments as variables. Initially, the module should only support variables that you are most likely to need.