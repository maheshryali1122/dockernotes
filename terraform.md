# Terrraform:
* Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently.
* Terraform creates and manages resources on cloud platforms and other services through their application programming interfaces (APIs).
* Terraform templates written in Hashicorp Configuration Language.
* Terraform workflow consists of three stages:
   1) Write
   2) Plan:
      * Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and configuration
   3) Apply:
      * On approval, Terraform performs the proposed operations in the correct order, respecting any resource dependencies. 

# Provider:
* In Terraform, a provider is a plugin that acts as a bridge between Terraform and the APIs of cloud services or other platforms. It is responsible for understanding the API interactions and exposing the resources and services from the provider (like AWS, Azure, etc.) so that they can be managed using Terraform's configuration files. Providers allow Terraform to create, manage, and update resources on these platforms by translating code into API calls.

# Resource:
* Resources are the most important element in the Terraform language. Each resource block describes one or more infrastructure objects, such as virtual networks, compute instances, or higher-level components such as DNS records.
# Command: init
* The terraform init command initializes a working directory containing Terraform configuration files. This is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control. It is safe to run this command multiple times.
"terraform init"
https://developer.hashicorp.com/terraform/cli/commands/init

# Command: validate
* The terraform validate command validates the configuration files in a directory, referring only to the configuration and not accessing any remote services such as remote state, provider APIs, etc.

# Command: apply
* The terraform apply command executes the actions proposed in a Terraform plan.
* We can pass the "-auto-approve" option to instruct Terraform to apply the plan without asking for confirmation.

# Variables:
* Terraform variables are placeholders for values that we can use to make configurations more dynamic and reusable. They let you define values that can be reused throughout your Terraform configuration, similar to variables in any programming language.
"terraform apply -var="target_region=us-west-2" -var="vpc_range=192.168.0.0/16" -auto-approve"

***To use attribute resource_type.resource_name.attribute***
# Implicit dependency
* An implicit dependency in Terraform is automatically determined by Terraform based on how resources reference each other in the configuration.
# Explicit dependency
* An explicit dependency is manually specified by using the depends_on argument in Terraform. This is used when a resource needs to be created or modified after another resource, but there is no direct reference between them in the configuration.
 
# Block:
* In Terraform, a block is a fundamental unit used to define and configure different aspects of infrastructure. Blocks are written in HashiCorp Configuration Language (HCL) and allow you to declare resources, providers, variables, outputs, and other configuration elements within your Terraform code. 

# Terraform state file:
* Terraform must store state about managed infrastructure and configuration. This state is used by Terraform to map real world resources to configuration, keep track of metadata, and to improve performance for large infrastructures.
* This state is stored by default in a local file named "terraform.tfstate"
## Backend Configuration
* A backend defines where Terraform stores its state data files. By default, Terraform uses a backend called local, which stores state as a local file on disk.
S3:
* Stores the state as a given key in a given bucket on Amazon S3. This backend also supports state locking and consistency checking via Dynamo DB, which can be enabled by setting the dynamodb_table field to an existing DynamoDB table name. A single DynamoDB table can be used to lock multiple remote state files 

# Modules:
* Modules are used to create reusable components inside the infrastructure. There are primarily two types of modules depending on how they are written (root and child modules), and depending if they are published or not, we identify two different types as well (local and published).
## Root module:
* The root module consists of all the resources defined in the .tf files in a Terraform configuration, meaning that all Terraform configurations have their own root module. 
## Child module:
* Calling a child module means to include all the resources defined in that module in the current configuration. This is done by using a module block inside your Terraform configuration
# Local module:
* A local module is a module that wasn’t published in any registry and when it is sourced, it is using the path to that particular module.
# Published module:
* A published module refers to a module that has been pushed to a Terraform Registry, or even simply on a VCS and has a tag associated with it. When a published module is sourced, the URL of that module is used either from the registry or from the VCS itself

# Datasource:
* Datasource help in fetching the information about some resources in the provider.

# Command: taint:
* The terraform taint command informs Terraform that a particular object has become degraded or damaged. Terraform represents this by marking the object as "tainted" in the Terraform state, and Terraform will propose to replace it in the next plan you create.

# Terraform Provisioning
* It allow the execution of various commands or scripts on either local or remote machines, and they can also transfer files from a local environment to a remote one. There are three available provisioners: file (used for copying), local-exec (used for local operations), remote-exec (used for remote operations). The file and remote-exec provisioners need a connection block to be able to do the remote operations.

# Workspaces
* Terraform workspaces enable us to manage multiple deployments of the same configuration. When we create cloud resources using the Terraform configuration language, the resources are created in the default workspace. It is a very handy tool that lets us test configurations by giving us flexibility in resource allocation, regional deployments, multi-account deployments, and so on.

# Null resource:
* In Terraform, a null_resource is a special type of resource used to perform actions that are not directly related to managing infrastructure. It is part of the null provider, which is built into Terraform
* It is used for executing arbitrary code or running actions that do not involve creating or managing actual infrastructure resources. This can include tasks such as running scripts, triggering external processes, or setting up dependencies that are not handled by other Terraform resources

