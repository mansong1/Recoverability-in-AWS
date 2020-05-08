# Data durability and recovery

In this project we will be creating highly available solutions to common use cases.  We will build a Multi-AvailabilityZone, Multi-Region database and show how to use it in multiple geographically separate AWS regions.  We will also build a website hosting solution that is versioned so that any data destruction and accidents can be quickly and easily undone.

## Getting Started

To get started, clone this repo.  Aside from instructions, it contains a CloudFormation script to build an AWS VPC with public and private subnets.  It also contains an example website that you will host in an AWS S3 bucket in your account.

### Cloud formation
In this project, you will use the AWS CloudFormation to create Virtual Private Clouds. CloudFormation is an AWS service that allows you to create "infrastructure as code". This allows you to define the infrastructure you'd like to create in code, just like you do with software. This has the benefits of being able to share your infrastructure in a common language, use source code control systems to version your infrastructure and allows for documenting and reviewing of infrastructure and infrastructure proposed changes.

CloudFormation allows you to use a configuration file written in a YAML file to automate the creation of AWS resources such as VPCs. In this project, you will use a pre-made CloudFormation template to get you started. This will allow you to create some of the infrastructure that you'll need without spending a lot of time learning details that are beyond the scope of this course.

You can find the YAML file in the repo: **cloudformation/vpc.yml

In order to build a VPC from the YAML file, we will use `create-stack.sh` located under the cloudformation folder which takes the following arguments:

```
  stack-name     - the stack name
  template-file  - the cloudformation template file
  parameter-file - json file with parameters
  region         - the AWS region
  aws-cli-opts   - extra options passed directly to create-stack/update-stack
```

1. In AWS Console go to Services -> CloudFormation
2. Run `./create-stack.sh active vpc.yml primary.json us-west-1`
3. Wait for the stack to build out.  Refresh until status becomes CREATE_COMPLETE
4. Observe the “Outputs” tab for the created IDs.  These will be used later.
5. Repeat for "standby" VPC `./create-stack.sh standby vpc.yml secondary.json us-west-2`

Once the CloudFormation Stack has completed, you can look at the "Resources" tab to see all of the AWS resources that the stack has created.  You can see both the type of resources that have been created, as well as the AWS identifiers for those resources so that you can locate these resources in the AWS service that they are a part of.

The "Outputs" tab shows you custom output from the CloudFormation Stack that is labeled and described for you.  These descriptions are custom descriptions that were added to the CloudFormation template and make it easier for you to find specific values that have been created as a part of the CloudFormation stack.  Here, you can find the VPC ID that has been created, the subnet IDs including which subnets are public and which are private, and the Security Groups that have been created and a description of each.

## License
