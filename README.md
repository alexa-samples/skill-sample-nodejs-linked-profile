# Linked Profile (Account Linking) Sample Skill

# ** This repository has been archived **
This repository is still available as a point-in-time reference, but no further updates or support will be prioritized.

This sample custom skill demonstrates account linking for the purposes of utilizing a linked profile.  While any compliant oAuth identity provider could be used with account linking, Amazon Cognito will be used in this sample.

These instructions will cover how to setup a user account and oAuth service using Amazon Cognito User Pools, coupled with an example skill (written using the Alexa Skills Kit SDJ for Node.js) that links to the Cognito OAuth service and provides personalized responses.

This sample may provide a starting point for skill developers who need but do not have existing user account or OAuth infrastructure. If the Cognito feature of additional user attributes/properties is not required, consider using [Login with Amazon](https://login.amazon.com) or other identity providers.

> NOTE: This sample does not constitute a full solution for user account management and OAUTH, nor does it provide functionality as-is which would be suitable for publishing to the Alexa Skill store.

## Pre-requisites

In order to completely setup this sample, the following are required:

1. AWS account which can:
    * Create Amazon Cognito User Pools
    * Create AWS IAM roles
    * Create AWS Lambda functions
1. Amazon Developer account
1. Your developer account's Vendor Id. To lookup your Vendor ID, go to https://developer.amazon.com/settings/console/mycid and sign in with your Amazon Developer account if prompted. Once you have it, copy it to your **Scratch-Pad**.
    > What's a **Scratch-Pad**?  In addition to your Vendor Id, there will be a number of values you will obtain from one step and then need to use at a later time.  We recommend creating a new text file using your favorite text editor to use as a "scratch pad". We will refer to this text file as the **Scratch-Pad**.
TODO: decide if a template for the scratch pad is worthwhile.
1. (Optional) Domain, optionally hosted in Amazon Route53
    > Note: if you will be creating a linked skill for testing or demo purposes only, access to a domain is not required.  If you are creating something for production use, you will need the ability to create a domain name that can be used by Amazon Cognito.
1. (Optional) Alexa Skills Kit (ASK) Command-Line Interface (CLI)
    > Using the ASK CLI is optional.  Both GUI and CLI based instructions are provided. If you'd like to setup the ASK CLI click [here](https://alexa.design/cli-setup) for a quick start to set it up on your machine.  As an alternative, you can setup the ASK CLI on an AWS Cloud9 instance in ~5 minutes with instructions found [here](https://alexa.design/cli-cloud9). To learn more about Cloud9, click [here](https://aws.amazon.com/cloud9).
1. (Optional) AWS CLI setup
    > Like the ASK CLI, using the AWS CLI is optional.  Both GUI and CLI based instructions are provided.  If you'd like to setup the AWS CLI click [here](https://aws.amazon.com/cli) and follow the instructions appropriate to your operating system.  If you opted to use CLoud9 for setting up the ASK CLI, the AWS CLI is installed by default on your Cloud9 instance.

## Setup Outline

During this walk through you will setup the following:
* Amazon Cognito User Pool w/custom attributes
* AWS IAM role to allow the AWS Lambda function to access Amazon Cognito
* Alexa Skill configured with Account Linking
* AWS Lambda function to power your skill
* A test account in your User Pool

To get started by creating the Amazon Cognito User Pool, click [here](./instructions/setup-cognito.md).

## License

This library is licensed under the Amazon Software License.
