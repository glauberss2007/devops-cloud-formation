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

## Parameters

## Resources

## Mapping

## Outputs

## Conditions

## Rules

## Metadata

## CFN init - use case

## Nested stack

## Stracksets

## Deployments

## CI/CD

## Advanced

## IMports, SAM, CDK & Macros

## 3rd projects for CF

## Final examples

## References





