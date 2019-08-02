# Linked Profile (Account Linking) Sample Skill

In this section, you will use the AWS CLI to create an AWS IAM Role (with Policy) which will be used by the Lambda function that backs your skill. If you prefer to use the AWS Console, click [here](./setup-iam.md).

## IAM Setup

Creating policy, role and trust policy via the AWS CLI. The policy files are provided in the skill package (extracted zip file) under the “IAM-Policies” directory:

1. On the command line, navigate to the skill project's root folder.  You will see the file **skill.json** in this folder.
1. Create the policy from the [linked-profile-policy.json](./resources/linked-profile-policy.json) file using this command:
    ```
    aws iam create-policy --policy-name linked-profile-skill-policy --policy-document file://resources/linked-profile-policy.json
    ```
1. Create the role from the [linked-profile-trust-policy.json](./resources/linked-profile-trust-policy.json) file using this command:
    ```
    aws iam create-role --role-name linked-profile-role --assume-role-policy-document file://resources/linked-profile-trust-policy.json
    ```
1. In the output from the previous command, locate the **ARN** for the role which was just created.
1. Attach the policy to the role using the following command, substituting in the Role's ARN for the placeholder value `<ARN>`.
    ```
    aws iam attach-role-policy --role-name linked-profile-role --policy-arn <ARN>
    ```

## Summary

You've created the role required to be used by the AWS Lambda function.  You're now ready to create the skill and function.
 
To continue using the CLI for setup, click [here](./setup-skill-using-cli.md).
If you'd prefer to switch to the GUI, click [here](./setup-skill.md).
