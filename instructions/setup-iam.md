# Linked Profile (Account Linking) Sample Skill - AWS IAM Setup

In this section, you will create an AWS IAM Role (with Policy) which will be used by the Lambda function that backs your skill. If you prefer to use the AWS CLI, click [here](./setup-iam-using-cli.md).

1. Navigate to the [AWS IAM Console](https://console.aws.amazon.com/iam).
1. Click **Policies** on the left-side menu.
1. Click the **Create Policy** button.
1. Click on the **JSON** tab.
1. Replace the placeholder JSON with the following:
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "cognito-idp:GetUser",
                    "logs:CreateLogGroup",
                    "logs:CreateLogStream",
                    "logs:PutLogEvents"
                ],
                "Resource": "*"
            }
        ]
    }
    ```
1. Click **Review Policy**.
1. Enter a name such as `linked-profile-skill-policy`.
1. Click **Create policy**.
1. Select **Roles** on the left-side menu.
1. Click the **Create role** button.
1. Under **Select type of trusted entity**, select **AWS service**.
1. Under **Choose the service that will use this role**, select  **Lambda**.
1. Click the **Next:Permissions** button.
1. Search for the policy (**linked-profile-skill-policy**) created in an earlier step and tick the box next to your policy.
1. Click the **Next:Tags** button, then the **Next:Review** button.
1. Enter a name such as `linked-profile-role`.
1. Click the **Create role** button.
1. Copy the Role name to your **Scratch-Pad**. You will need this later in the process.

## Summary

You've created the role required to be used by the AWS Lambda function.  You're now ready to create the skill and function.

To continue using the GUI for setup, click [here](./setup-skill.md).
If you'd prefer to switch to the CLI, click [here](./setup-skill-using-cli.md). 
