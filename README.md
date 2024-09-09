# devops-cloud-formation
Project with several cloud formation templates related to multiple AWS diferent resources.

## Benefits of cloud formation

- **Infrastructure as Code (IaC):** Ensures consistency and enables version control by defining infrastructure using templates.
- **Automation:** Automates deployment, reducing human error and allowing for repeatability across environments.
- **Scalability and Flexibility:** Manages AWS resources to allow for scaling and adjustments without manual intervention.
- **Cost Efficiency:** Automates resource lifecycle management to optimize costs.
- **Security and Compliance:** Maintains consistent security and compliance configurations.
- **Dependency Management:** Automatically handles resource dependencies to prevent deployment failures.
- **Update and Change Management:** Offers change sets and rollback support for safer updates.
- **Integration:** Seamlessly works with AWS and can integrate third-party resources through custom scripts.

## Introduction

AWS CloudFormation is a service provided by Amazon Web Services that allows users to define and provision cloud infrastructure using code. With CloudFormation, you can create and manage a collection of related AWS resources, such as EC2 instances, S3 buckets, and RDS databases, in a predictable and repeatable manner. By using templates written in JSON or YAML, users can automate the deployment and management of their cloud resources, simplifying operations and reducing the risk of errors. This enables developers and operations teams to implement infrastructure as code and manage resources efficiently.

## Getting Start

To start using AWS CloudFormation with Visual Studio Code (VS Code), you'll need to set up the environment and install helpful extensions for writing and managing code templates. Here's a step-by-step guide:

### 1. Install Visual Studio Code
- If you haven’t already, download and install Visual Studio Code from the [official website](https://code.visualstudio.com/).

### 2. Install Necessary Extensions
You can enhance your VS Code experience with extensions that specifically support AWS CloudFormation templates. Here are some recommended extensions:

- **AWS Toolkit for Visual Studio Code**:
  - This extension allows you to interact with AWS services directly from VS Code.
  - **Installation**:
    1. Open VS Code.
    2. Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side or pressing `Ctrl+Shift+X`.
    3. Search for "AWS Toolkit" and click "Install" on the AWS Toolkit for Visual Studio Code.

- **YAML Support**:
  - Since CloudFormation templates are often written in YAML, it's beneficial to have good YAML support.
  - **Installation**:
    1. In the Extensions view, search for "YAML" and install the one provided by Red Hat, which includes syntax highlighting and validation.

- **AWS CloudFormation Linter** (optional):
  - This extension helps to validate CloudFormation YAML templates.
  - **Installation**:
    1. Search for "CloudFormation Linter" in the Extensions view and install it.

### 3. Configure AWS Credentials
To interact with AWS services, you need to configure your AWS credentials:
- Open a terminal (inside VS Code or your operating system terminal).
- Use the AWS CLI to configure your credentials:
  ```bash
  aws configure
  ```
- Enter your AWS Access Key ID, Secret Access Key, region, and output format when prompted.

### 4. Create a CloudFormation Template
- Create a new file with a `.yaml` or `.json` extension for your CloudFormation template.
- You can start writing your template using the YAML format, benefiting from the syntax highlighting and formatting features of the installed extensions.

### 5. Utilize the AWS Toolkit
- The AWS Toolkit allows you to run CloudFormation stacks, view resources, and get information about your AWS setup.
- Access the AWS Toolkit features using the Activity Bar or command palette (`Ctrl+Shift+P`).

### 6. Validate Your Template
- Use the CloudFormation Linter to validate your template to ensure it adheres to AWS syntax.

### Final Notes
Make sure to regularly check AWS documentation for the latest practices and features when working with CloudFormation. With these tools in place, you’ll be well-equipped to create and manage AWS CloudFormation templates effectively!

## How it works

![image](https://github.com/user-attachments/assets/9ef73d81-d00f-423b-80c4-7683532cfa5b)

PS: Stack are identified by names and deleting a stack deletes every single artifact that was created by CF using this stack.

### Manually
- Using Application Composer or code editor.
- Using console input parameter

- ![image](https://github.com/user-attachments/assets/c473a901-2a39-49c8-8333-6fa5e79b2968)


### Automated
- Using AWS CLI to deploy it or a integrated CI/CD tool.

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

PS: AWS pseudo parameters are predefined variables provided by AWS that can be used in your CloudFormation templates. These parameters represent specific information about the stack or resources being created and do not require any user input. 

## Resources

In an AWS CloudFormation template, resources are the fundamental components that define the AWS infrastructure you want to create. Each resource corresponds to an AWS service or feature, and these resources are specified in the "Resources" section of the template.

In AWS CloudFormation, each resource type can have optional attributes that allow additional configurations beyond the required properties. These optional attributes can vary by resource type. Below are some common optional attributes that can be used in CloudFormation resources, along with examples for clarity:

### Common Optional Attributes

1. **DependsOn**:
   - Specifies that the creation of a resource follows another resource. This is useful for enforcing a specific order during resource creation.
   - **Example**:
     ```yaml
     MyInstance:
       Type: 'AWS::EC2::Instance'
       DependsOn: MySecurityGroup
     ```

2. **Condition**:
   - Allows you to control whether a resource is created based on a condition. This is useful for creating resources that are only applicable under certain circumstances.
   - **Example**:
     ```yaml
     MyBucket:
       Type: 'AWS::S3::Bucket'
       Condition: CreateBucketCondition
     ```

3. **Metadata**:
   - Provides additional information about the template or resources. It can be used for tools, documentation, or custom handling.
   - **Example**:
     ```yaml
     MyInstance:
       Type: 'AWS::EC2::Instance'
       Metadata:
         Comment: "This instance is for processing data."
     ```

4. **UpdatePolicy**:
   - Specifies how CloudFormation handles updates to a resource. This can be useful for resources like Auto Scaling groups and AWS::S3::Bucket.
   - **Example**:
     ```yaml
     MyAutoScalingGroup:
       Type: 'AWS::AutoScaling::AutoScalingGroup'
       UpdatePolicy:
         AutoScalingRollingUpdate:
           MaxBatchSize: 1
     ```

5. **DeletionPolicy**:
   - Controls what happens to a resource when its stack is deleted. Options include keeping the resource, deleting it, or snapshotting it.
   - **Example**:
     ```yaml
     MyDatabase:
       Type: 'AWS::RDS::DBInstance'
       DeletionPolicy: Snapshot
     ```

6. **Properties Specific to Resource Type**:
   - Many AWS resources have their own optional attributes that can be configured. For example:
     - **AWS::S3::Bucket** has optional attributes like `VersioningConfiguration`, `LifecycleConfiguration`, etc.
     - **AWS::EC2::Instance** has optional attributes such as `UserData`, `BlockDeviceMappings`, etc.

## Mapping

Mapping in AWS CloudFormation is a way to create a nested set of key-value pairs that help you customize configurations for different environments, regions, or conditions within your CloudFormation templates. It's essentially a lookup table that allows you to reference different values based on specific input parameters.

### Example

The provided CloudFormation template example is designed to create an Amazon EC2 instance while allowing the user to specify key parameters regarding the deployment environment and ensuring the correct Amazon Machine Image (AMI) is used based on the specified AWS region. 

link: [mapping-example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/3-mappings-ec2.yaml)

## Outputs

In AWS CloudFormation, Outputs are used to return information about the resources that you create within a stack. This section allows you to specify values that you want to be easily accessible after the stack is created, making it easier for users to retrieve important information about the infrastructure.

LInk: [Output example template](https://github.com/glauberss2007/devops-cloud-formation/blob/main/4-create-ssh-security-group.yaml)

Link: [Using the output in another template](https://github.com/glauberss2007/devops-cloud-formation/blob/main/4-reference-ssh-security-group.yaml)

## Conditions

Conditions allow you to control the creation of resources or outputs based on specific criteria. They enable you to define logical statements that can determine whether certain resources are created, properties are applied, or outputs are returned, depending on the values of parameters, pseudo parameters, or other conditions.

Link: [Condition use example](https://github.com/glauberss2007/devops-cloud-formation/blob/main/5-conditions.yaml)

## Rules

In AWS CloudFormation, Rules are a feature that allows you to validate parameter values when launching a CloudFormation stack. They enable the specification of conditions that the input parameters must meet to ensure they conform to certain requirements or constraints. 

Link: [Rules hands on](https://github.com/glauberss2007/devops-cloud-formation/blob/main/6-rules-hands-on.yaml)

## Metadata

In AWS CloudFormation, Metadata provides additional information about the resources in your template. It allows you to define custom data that can be useful for documentation, tooling, or reference purposes but does not directly affect the behavior of the infrastructure being provisioned. Metadata is particularly useful for developers, DevOps teams, and deployment automation tools.

## CFN init and user data

`cfn-init` is a helper script provided by AWS CloudFormation that is used to manage the lifecycle of resources in your CloudFormation stacks. It is primarily used to handle configuration and installation tasks on EC2 instances after they have been launched.

`EC2 User Data` refers to the script or instructions that you can pass to an EC2 instance at launch time. This user data runs automatically when the instance is first booted and is often used for:

Link: [initializing with templates](https://github.com/glauberss2007/devops-cloud-formation/tree/main/8-cfn-init)

## Nested stack

## Stracksets

## Deployments

## CI/CD

## Advanced

## IMports, SAM, CDK & Macros

## 3rd projects for CF

## Final examples

## References





