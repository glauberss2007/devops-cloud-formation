# devops-cloud-formation

Project with several CloudFormation templates related to various AWS resources.

## Table of Contents

1. [Benefits of CloudFormation](#Benefits-of-CloudFormation)
2. [Introduction](#Introduction)
3. [Getting Started](#Getting-Started)
   - 3.1 [Install Visual Studio Code](#1-Install-Visual-Studio-Code)
   - 3.2 [Install Necessary Extensions](#2-Install-Necessary-Extensions)
   - 3.3 [Configure AWS Credentials](#3-Configure-AWS-Credentials)
   - 3.4 [Create a CloudFormation Template](#4-Create-a-CloudFormation-Template)
   - 3.5 [Utilize the AWS Toolkit](#5-Utilize-the-AWS-Toolkit)
   - 3.6 [Validate Your Template](#6-Validate-Your-Template)
4. [How It Works](#How-It-Works)
   - 4.1 [Manually](#Manually)
   - 4.2 [Automated](#Automated)
5. [Parameters](#Parameters)
   - 5.1 [Example 1](#Examples-1)
   - 5.2 [Example 2](#Example-2)
6. [Resources](#Resources)
   - 6.1 [Common Optional Attributes](#Common-Optional-Attributes)
7. [Mapping](#Mapping)
8. [Outputs](#Outputs)
9. [Conditions](#Conditions)
10. [Rules](#Rules)
11. [Metadata](#Metadata)
12. [CFN Init and User Data](#CFN-Init-and-User-Data)
13. [Drift](#Drift)
14. [Nested Stack and Cross-Stack](#Nested-Stack-and-Cross-Stack)
15. [StackSets](#StackSets)
16. [Deployment Options](#Deployment-Options)
17. [CI/CD](#CICD)
18. [Custom Resources](#Custom-Resources)
19. [Imports, SAM, CDK & Macros](#Imports-SAM-CDK--Macros)
20. [3rd Party Projects for CloudFormation](#rd-Party-Projects-for-CloudFormation)
21. [Final Examples](#Final-Examples)
22. [References](#References)

## Benefits of CloudFormation

1. **Infrastructure as Code (IaC):** Ensures consistency and enables version control by defining infrastructure using templates.
2. **Automation:** Automates deployment, reducing human error and allowing for repeatability across environments.
3. **Scalability and Flexibility:** Manages AWS resources to allow for scaling and adjustments without manual intervention.
4. **Cost Efficiency:** Automates resource lifecycle management to optimize costs.
5. **Security and Compliance:** Maintains consistent security and compliance configurations.
6. **Dependency Management:** Automatically handles resource dependencies to prevent deployment failures.
7. **Update and Change Management:** Offers change sets and rollback support for safer updates.
8. **Integration:** Seamlessly works with AWS and can integrate third-party resources through custom scripts.

## Introduction

AWS CloudFormation is a service provided by Amazon Web Services that allows users to define and provision cloud infrastructure using code. With CloudFormation, you can create and manage a collection of related AWS resources, such as EC2 instances, S3 buckets, and RDS databases, in a predictable and repeatable manner. By using templates written in JSON or YAML, users can automate the deployment and management of their cloud resources, simplifying operations and reducing the risk of errors. This enables developers and operations teams to implement infrastructure as code and manage resources efficiently.

## Getting Started

To start using AWS CloudFormation with Visual Studio Code (VS Code), you'll need to set up the environment and install helpful extensions for writing and managing code templates. Here's a step-by-step guide:

### 1. Install Visual Studio Code

- If you haven’t already, download and install Visual Studio Code from the [official website](https://code.visualstudio.com/).

### 2. Install Necessary Extensions

Enhance your VS Code experience with extensions that specifically support AWS CloudFormation templates. Here are some recommended extensions:

- **AWS Toolkit for Visual Studio Code:**
  - Allows interaction with AWS services directly from VS Code.
  - **Installation:**
    1. Open VS Code.
    2. Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side or pressing `Ctrl+Shift+X`.
    3. Search for "AWS Toolkit" and click "Install."

- **YAML Support:**
  - Helpful for writing CloudFormation templates in YAML.
  - **Installation:**
    1. In the Extensions view, search for "YAML" and install the one provided by Red Hat.

- **AWS CloudFormation Linter (optional):**
  - Validates CloudFormation YAML templates.
  - **Installation:**
    1. Search for "CloudFormation Linter" in the Extensions view and install it.

### 3. Configure AWS Credentials

To interact with AWS services, configure your AWS credentials:

- Open a terminal (in VS Code or your operating system terminal).
- Use the AWS CLI to configure your credentials:
  ```bash
  aws configure
  ```
- Enter your AWS Access Key ID, Secret Access Key, region, and output format when prompted.

### 4. Create a CloudFormation Template

- Create a new file with a `.yaml` or `.json` extension for your CloudFormation template.
- Start writing your template using the YAML format, benefiting from syntax highlighting and formatting features of the installed extensions.

### 5. Utilize the AWS Toolkit

- The AWS Toolkit allows running CloudFormation stacks, viewing resources, and obtaining information about your AWS setup.
- Access AWS Toolkit features using the Activity Bar or command palette (`Ctrl+Shift+P`).

### 6. Validate Your Template

- Use the CloudFormation Linter to validate your template to ensure it adheres to AWS syntax.

### Final Notes

Regularly check AWS documentation for the latest practices and features when working with CloudFormation. With these tools in place, you’ll be well-equipped to create and manage AWS CloudFormation templates effectively!

## How It Works

![image](https://github.com/user-attachments/assets/9ef73d81-d00f-423b-80c4-7683532cfa5b)

### Manually

- Using Application Composer or code editor.
- Using console input parameter

![image](https://github.com/user-attachments/assets/c473a901-2a39-49c8-8333-6fa5e79b2968)

### Automated

- Using AWS CLI to deploy it or an integrated CI/CD tool.

![image](https://github.com/user-attachments/assets/ab90d8e7-ff60-448a-9924-a7c8ee117e8e)

## Parameters

In AWS CloudFormation, parameters are dynamic values that allow users to customize templates at runtime. They enable you to create reusable templates where you can specify input values when launching the stack, making the stack configuration more flexible and adaptable to varying environments. Parameters can be strings, numbers, or lists, and they help collect inputs like instance type, region, key names, and more.

The SSM Parameter type refers to parameters stored in the AWS Systems Manager Parameter Store. Using this type in CloudFormation allows you to reference parameters that may contain sensitive information, configurations, or environment variables without hardcoding them into your templates.

### Examples 1

This CloudFormation template example defines essential parameters and resources for setting up an EC2 environment in AWS. It includes a security group description, a numeric port parameter with value constraints, and a default EC2 instance type. Additionally, it incorporates a masked database admin password for security, a KeyPair for SSH access, and a CIDR IP range for controlling incoming traffic. The template also specifies the VPC and subnet IDs for resource organization, ultimately creating an EC2 instance, security group, and subnets that adhere to user-defined configurations.

Link: [params-example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/2-parameters-use.yaml)  

### Example 2

This CloudFormation template example is designed to provision an Amazon EC2 instance while leveraging AWS Systems Manager (SSM) Parameter Store to retrieve configuration values dynamically. 

Link: [ssm-param-example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/2-ssm-parameters-use.yaml)

## Resources

In an AWS CloudFormation template, resources are the fundamental components that define the AWS infrastructure you want to create. Each resource corresponds to an AWS service or feature, and these resources are specified in the "Resources" section of the template.

In AWS CloudFormation, each resource type can have optional attributes that allow additional configurations beyond the required properties. These optional attributes can vary by resource type. Below are some common optional attributes that can be used in CloudFormation resources, along with examples for clarity:

### Common Optional Attributes

1. **DependsOn:**
   - Specifies that the creation of a resource follows another resource.
   - **Example:**
     ```yaml
     MyInstance:
       Type: 'AWS::EC2::Instance'
       DependsOn: MySecurityGroup
     ```

2. **Condition:**
   - Allows you to control whether a resource is created based on a condition.
   - **Example:**
     ```yaml
     MyBucket:
       Type: 'AWS::S3::Bucket'
       Condition: CreateBucketCondition
     ```

3. **Metadata:**
   - Provides additional information about the template or resources.
   - **Example:**
     ```yaml
     MyInstance:
       Type: 'AWS::EC2::Instance'
       Metadata:
         Comment: "This instance is for processing data."
     ```

4. **UpdatePolicy:**
   - Specifies how CloudFormation handles updates to a resource.
   - **Example:**
     ```yaml
     MyAutoScalingGroup:
       Type: 'AWS::AutoScaling::AutoScalingGroup'
       UpdatePolicy:
         AutoScalingRollingUpdate:
           MaxBatchSize: 1
     ```

5. **DeletionPolicy:**
   - Controls what happens to a resource when its stack is deleted.
   - **Example:**
     ```yaml
     MyDatabase:
       Type: 'AWS::RDS::DBInstance'
       DeletionPolicy: Snapshot
     ```

6. **Properties Specific to Resource Type:**
   - Many AWS resources have their own optional attributes.
     - **AWS::S3::Bucket**: Includes `VersioningConfiguration`, `LifecycleConfiguration`, etc.
     - **AWS::EC2::Instance**: Includes `UserData`, `BlockDeviceMappings`, etc.

## Mapping

Mapping in AWS CloudFormation is a way to create a nested set of key-value pairs that help you customize configurations for different environments, regions, or conditions within your CloudFormation templates. It's essentially a lookup table that allows you to reference different values based on specific input parameters.

### Example

The provided CloudFormation template example is designed to create an Amazon EC2 instance while allowing the user to specify key parameters regarding the deployment environment and ensuring the correct Amazon Machine Image (AMI) is used based on the specified AWS region. 

Link: [mapping-example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/3-mappings-ec2.yaml)

## Outputs

In AWS CloudFormation, Outputs are used to return information about the resources that you create within a stack. This section allows you to specify values that you want to be easily accessible after the stack is created, making it easier for users to retrieve important information about the infrastructure.

Link: [Output example template](https://github.com/glauberss2007/devops-cloud-formation/blob/main/4-create-ssh-security-group.yaml)

Link: [Using the output in another template](https://github.com/glauberss2007/devops-cloud-formation/blob/main/4-reference-ssh-security-group.yaml)

## Conditions

Conditions allow you to control the creation of resources or outputs based on specific criteria. They enable you to define logical statements that can determine whether certain resources are created, properties are applied, or outputs are returned, depending on the values of parameters, pseudo parameters, or other conditions.

Link: [Condition use example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/5-conditions.yaml)

## Rules

In AWS CloudFormation, Rules are a feature that allows you to validate parameter values when launching a CloudFormation stack. They enable the specification of conditions that the input parameters must meet to ensure they conform to certain requirements or constraints. 

Link: [Rules hands on](https://github.com/glauberss2007/devops-cloud-formation/blob/main/6-rules-hands-on.yaml)

## Metadata

In AWS CloudFormation, Metadata provides additional information about the resources in your template. It allows you to define custom data that can be useful for documentation, tooling, or reference purposes but does not directly affect the behavior of the infrastructure being provisioned. Metadata is particularly useful for developers, DevOps teams, and deployment automation tools.

## CFN Init and User Data

`cfn-init` is a helper script provided by AWS CloudFormation to manage the lifecycle of resources in your CloudFormation stacks. It is primarily used to handle configuration and installation tasks on EC2 instances after they have been launched. Here are some of the configurations you can perform with `cfn-init`:

- **Packages:** Specify software packages to be installed on your instance.
- **Groups and Users:** Create Linux groups and users directly within CloudFormation templates.
- **Sources:** Manage and download resources from locations like S3 buckets or public URLs.
- **Files:** Specify local files to create/manage on instances.
- **Authentication:** Facilitate authentication for applications and dependencies stored in private repositories.
- **Commands:** Execute commands at different stages of instance launch.
- **Services:** Define services to be enabled, started, stopped, or restarted.
- **cfn-hup:** A daemon that checks for updates to CloudFormation metadata.
- **Creation Policy:** Ensures stack resources are created successfully before being marked complete.

`EC2 User Data` refers to the script or instructions you can pass to an EC2 instance at launch time:

- Install packages
- Run scripts
- Configure settings

For more template examples and how to initialize configurations using `cfn-init`, you can check the following [link](https://github.com/glauberss2007/devops-cloud-formation/tree/main/8-cfn-init).

## Drift

CloudFormation Drift refers to a situation where the actual state of resources provisioned and managed by AWS CloudFormation differs from the expected state as defined in the CloudFormation template. This can occur when changes are made directly to the resources outside of CloudFormation's control, such as manual updates in the AWS Management Console or API calls that modify resource settings.

AWS CloudFormation provides drift detection capabilities:

- **Identify Drifted Resources:** Determine which resources have drifted and see the properties that differ.
- **Mitigate Configuration Issues:** Use drift detection reports to understand discrepancies.
- **Audit and Compliance:** Ensure resources remain compliant over time by checking for drifts.

Example: [Drift Detection Example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml).

## Nested Stack and Cross-Stack

In AWS CloudFormation, nested stacks and cross-stack references are strategies to manage resources across different CloudFormation templates efficiently:

- **Nested Stacks:** Allow creating stacks within other stacks, enabling modular and reusable designs.
  - Encourages decomposition of large architectures into simpler parts.
  - Update components without affecting the entire infrastructure.

- **Cross-Stack References:** Allow values to be shared between independent stacks.
  - Use Outputs to export a value and import it using `Fn::ImportValue`.
  - Suitable for sharing common resources like VPCs or security groups across stacks.

## StackSets

StackSets in AWS CloudFormation allows deploying and managing stacks across multiple AWS accounts and regions from a single template. This feature is useful for organizations needing consistent infrastructure across environments or locations.

- **Centralized Management:** Define AWS resource configurations in a template to create stacks across accounts/regions.
- **Two Types of Deployments:**
  - **Self-Managed:** You specify target accounts and regions.
  - **Service-Managed:** Utilizes AWS Organizations for seamless account and permission management.
- **Propagation of Updates:** Automatically propagate updates to all associated stacks.

Example configurations: [AWS Config](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml), [StackSet Admin Role](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml), and [StackSet Exec Role](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml).

## Deployment Options

- **Change Sets:** Preview proposed changes before applying them to the stack.
- **Stack Policies:** Define specific update actions allowed on resources, providing governance and protection.

Example: [Deployment Example](https://github.com/glauberss2007/devops-cloud-formation/tree/main/12-deployment-options).

## CI/CD

![image](https://github.com/user-attachments/assets/0a2cadbb-75fe-419b-999a-69577b778444)

CI/CD (Continuous Integration and Continuous Deployment) with AWS CodePipeline and AWS CloudFormation automates integration, testing, and deployment processes. It starts with CodePipeline retrieving code from a version control system, followed by testing via AWS CodeBuild. Successful builds trigger deployment using AWS CloudFormation, ensuring consistent environments.

Example: [CD with CodePipeline](https://github.com/glauberss2007/devops-cloud-formation/tree/main/13-cd-with-codepipeline)

## Custom Resources

CloudFormation custom resources extend AWS CloudFormation functionalities to manage resources not natively supported or execute custom logic. You define a custom resource in your template and provide a ServiceToken pointing to an AWS Lambda function for resource operations.

- **Event Data:** Trigger Lambda with data to perform actions (Create, Update, Delete).
- **Asynchronous Handling:** For long operations, use AWS Step Functions or other mechanisms to communicate with CloudFormation.

Example: [Custom Resources](https://github.com/glauberss2007/devops-cloud-formation/tree/main/14-advanced-resources).

## Imports, SAM, CDK & Macros


## 3rd Party Projects for CloudFormation


## Final Examples


## References

1. AMAZON Web Services. **AWS CloudFormation Documentation**. Available at: https://docs.aws.amazon.com/cloudformation/. Accessed on: 11 Sep. 2024.
2. AMAZON Web Services. **AWS CloudFormation Best Practices**. Available at: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html. Accessed on: 11 Sep. 2024.
3. AMAZON Web Services. **AWS CloudFormation Sample Templates**. Available at: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html. Accessed on: 11 Sep. 2024.
4. AMAZON Web Services. **AWS CloudFormation StackSets User Guide**. Available at: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-concepts.html. Accessed on: 11 Sep. 2024.
5. AMAZON Web Services. **AWS Management Console**. Available at: https://aws.amazon.com/console/. Accessed on: 11 Sep. 2024.
6. AMAZON Web Services. **AWS Developer Forums**. Available at: https://forums.aws.amazon.com/forum.jspa?forumID=27. Accessed on: 11 Sep. 2024.
7. AMAZON Web Services. **AWS Quick Start Templates**. GitHub. Available at: https://github.com/aws-quickstart. Accessed on: 11 Sep. 2024.
