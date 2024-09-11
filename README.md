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

`cfn-init` is a helper script provided by AWS CloudFormation that is used to manage the lifecycle of resources in your CloudFormation stacks. It is primarily used to handle configuration and installation tasks on EC2 instances after they have been launched. Here are some of the configurations you can perform with `cfn-init`:

- **Packages**: You can specify software packages to be installed on your instance. This includes specifying package manager types (like `apt`, `yum`, or `msi` for Windows) and listing packages to be installed.

- **Groups and Users**: You can create Linux groups and users directly within CloudFormation templates. This makes it easier to set up initial user configurations and security groups.

- **Sources**: You can manage and download resources such as application source code or configuration files from locations like S3 buckets or public URLs.

- **Files**: Specify local files you need to create or manage on your instances. This might include configuration files or scripts that `cfn-init` can write to disk.

- **Authentication**: The `auth` section in a CloudFormation template is used to facilitate authentication, particularly for applications and dependencies stored in private repositories like a private S3 bucket.

- **Commands**: Execute commands at different stages of instance launch to, for example, complete the software setup process or initialize services.

- **Services**: Define services to be enabled, started, stopped, or restarted at specific stages of instance initialization.

- **cfn-hup**: This is a daemon that checks for updates to CloudFormation metadata and can trigger actions such as redeploying applications, reconfiguring software, or managing rolling updates. It's crucial when using `cfn-init` for applying updates without requiring a complete instance reboot.

- **Creation Policy**: It is used to ensure that the stack resources are created successfully before being marked complete. You can use this along with `cfn-signal` to signal that an EC2 instance has been successfully created and all user data and `cfn-init` tasks have been applied.

`EC2 User Data` refers to the script or instructions that you can pass to an EC2 instance at launch time. This user data runs automatically when the instance is first booted and is often used for:

- Installing packages
- Running scripts
- Configuring settings

For more template examples and how to initialize with configurations using `cfn-init`, you can check the following [link](https://github.com/glauberss2007/devops-cloud-formation/tree/main/8-cfn-init).

## Drift

CloudFormation Drift refers to a situation where the actual state of resources provisioned and managed by AWS CloudFormation differs from the expected state as defined in the CloudFormation template. This can occur when changes are made directly to the resources outside of CloudFormation's control, such as manual updates in the AWS Management Console or API calls that modify resource settings.

AWS CloudFormation provides drift detection capabilities to help identify resources that have drifted from their expected configuration. Using drift detection, you can:

- **Identify Drifted Resources**: Determine which resources have drifted and see the properties that differ from the expected configuration.
- **Mitigate Configuration Issues**: Use drift detection reports to understand discrepancies and decide whether to update the CloudFormation stack to correct the drifts or integrate these changes back into the template if they are desired.
- **Audit and Compliance**: Ensure that resources remain compliant with desired configurations over time by regularly checking for drifts.

You can check the following example [link](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml).

## Nested stack and cross stack

In AWS CloudFormation, nested stacks and cross-stack references are two strategies used to manage resources across different CloudFormation templates efficiently. Nested stacks allow you to create stacks within other stacks, essentially enabling you to include child templates as part of a parent template. This approach is particularly useful for breaking down complex infrastructure designs into smaller, more manageable modules, enhancing readability and reusability. The child templates can be called upon by defining an `AWS::CloudFormation::Stack` resource within the parent template, which then deploys the child as part of the parent stack. This modular design encourages the decomposition of large architectures into simpler parts, allows for reusability across different parent stacks, and provides a way to update components without affecting the entire infrastructure.

On the other hand, cross-stack references allow values to be shared between independent CloudFormation stacks. This is done by exporting values in one stack and importing them into another. In practice, you use the `Outputs` section to export a value with a unique name, which is then imported by another stack using the `Fn::ImportValue` function. Cross-stack references are advantageous for decoupling stacks, thereby simplifying the management of dependencies and allowing for flexible architecture. They are particularly suitable for sharing common resources—such as VPCs or security groups—across multiple stacks without duplicating their definitions. 

## Stacksets

StackSets in AWS CloudFormation is a powerful feature that allows you to deploy and manage CloudFormation stacks across multiple AWS accounts and regions from a single template. This capability is particularly useful for organizations that need to maintain consistent infrastructure across various environments, such as production and development, or across different branches and geographical locations.

With StackSets, you can define the desired AWS resource configurations in a CloudFormation template and then use that template to create stacks across chosen accounts and regions. A single StackSet can manage multiple stacks that are created, updated, or deleted in one operation, ensuring uniformity and consistency of the deployed resources.

StackSets provide a centralized management approach, simplifying operations like rolling out updates and applying compliance and security policies consistently. When you update a StackSet, it automatically propagates the changes to all associated stacks, making it easier to perform large-scale updates without manual intervention in each region or account.

Additionally, StackSets support two types of deployments: self-managed, where you manually specify the target accounts and regions, and service-managed, which utilizes AWS Organizations to automate the process of managing accounts and permissions. The service-managed option greatly simplifies deployments in multi-account environments by granting AWS CloudFormation the necessary permissions using AWS Organizations service control policies.

Overall, StackSets streamline the management of cross-account and cross-region deployments, ensuring that infrastructure is consistently configured and maintained, thereby reducing the complexity and overhead involved in operating multi-account AWS environments.

You can check the following examples [aws config](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml),[stack set admin role](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml) and [stack set exec role](https://github.com/glauberss2007/devops-cloud-formation/blob/main/9-drift-sg.yaml). 

## Deployments option

Change Sets make it possible to before making updates to a stack, you can create a change set to preview how proposed changes might impact existing resources. This preview includes information about the operations that will or might result, such as additions, deletions, or modifications of resources in the stack.

The Stack Policies are JSON documents that define the specific update actions allowed on resources within a stack, providing a level of governance and control. They can prevent certain resources from being unintentionally updated, thus adding an extra layer of protection.

You can check the following examples [deployments example](https://github.com/glauberss2007/devops-cloud-formation/tree/main/12-deployment-options)

## CI/CD

![image](https://github.com/user-attachments/assets/0a2cadbb-75fe-419b-999a-69577b778444)

CI/CD (Continuous Integration and Continuous Deployment) with AWS CodePipeline and AWS CloudFormation streamlines the automation of integrating, testing, and deploying application and infrastructure changes. In this setup, the process starts with CodePipeline retrieving code from a version control system like AWS CodeCommit or GitHub. The code is then built and tested using AWS CodeBuild, which may include validating CloudFormation templates. Successful builds lead to the deployment stage, where AWS CloudFormation automates the provisioning and updating of AWS resources as defined in the templates, ensuring consistent and reliable environments. 

You can check the following examples [cd with code pipeline](https://github.com/glauberss2007/devops-cloud-formation/tree/main/13-cd-with-codepipeline)

## Advanced

## Imports, SAM, CDK & Macros

## 3rd projects for CF

## Final examples

## References





