# Linked Profile (Account Linking) Sample Skill - Setup Skill using ASK CLI

In this section, you will create a configured skill and AWS Lambda function using the ASK and AWS CLI. If you prefer to use the GUI, click [here](./setup-skill.md).

1. Clone this repo to your local machine if you haven't already.
```
ask new --url https://github.com/alexa/skill-sample-nodejs-linked-profile.git --skill-name linked-profile
```
1. From your command prompt, navigate to the root folder of the skill project. The skill.json file is found in this folder.
```
cd linked-profile
```
1. Deploy the skill and function using the `ask deploy` command.
```
ask deploy
```
1. Note the Skill-Id in the output and copy it to your **Scratch-Pad**.
1. The newly created Lambda function does not use the IAM Role you created in the previous step. Use this command to update the AWS Role used by the Lambda function using the AWS CLI:
```
aws lambda update-function-configuration --function-name \\
ask-linked-profile –role ask-linked-profile-role --runtime nodejs8.10 –timeout 8
```
TODO - check if the runtime and timeout can be left off to simplify the command.
> Note: if you did not setup the AWS CLI, you can adjust the execution role for your function from the AWS Lambda console by clicking [here]](https://console.aws.amazon.com/lambda/ask-linked-profile).  Scroll down to the Execution Role selection and select **ask-linked-profile-role** from the list and click **Save**.
1. Update the skill with account linking details using the ASK CLI:
```
ask api create-account-linking -s <Skill-ID>
? Authorization URL:  https://<your-domain>/oauth2/authorize?redirect_url=https://pitangui.amazon.com/api/skill/link/<VID>
? Client ID:  <client-ID>
? Scopes(separate by comma): openid, profile, aws.cognito.signin.user.admin
? Domains(separate by comma): <your-domain>
? Authorization Grant Type:  AUTH_CODE
? Access Token URI:  https://<your-domain>/oauth2/token
? Client Secret:  <client-secret>
? Client Authentication Scheme:  HTTP Basic
? Optional* Default Access Token Expiration Time In Seconds: 3600
```
TODO: when is the lambda function trigger setup with the skill id?

## Summary

Great job!  You've created and configured your skill, including the Lambda function, and now you're ready to try it out!  To continue, click [here](./try-it-out.md).
