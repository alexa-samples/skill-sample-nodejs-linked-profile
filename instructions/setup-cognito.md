# Linked Profile (Account Linking) Sample Skill- Amazon Cognito Setup
In this section, you will create an Amazon Cognito User Pool. As part of this process, you will note the details that you need in order to complete the Account Linking details section when creating the Alexa skill.

## Create the User Pool
1. Login to the AWS Console and navigate to the Cognito service.  Click [here](https://console.aws.amazon.com/cognito) to go directly there.
1. Check the AWS region being used by looking in the upper right of the console.  Change it if desired.
    > You can use any region supported by Cognito, however we recommend that you use one of the four regions that supports the Alexa Skills trigger so you can keep all the related resources in the same region.  Those four regions are us-east-1 (N. Virginia), us-west-2 (Oregon), eu-west-1 (Ireland) and ap-northeast-1 (Tokyo).  If necessary, switch to your desired region.
1. Click **Manage User Pools**.
1. Click **Create a user pool**.
    > For the purposes of this sample, only the minimum required settings are being changed. For production use, be sure to review each section and update accordingly.
1. Enter a **Pool name**, such as `Alexa Skill Users` and click **Review Defaults**.
1. Select **Attributes** on the left-side menu.
1. Select **Email address or phone number** and choose **Allow email addresses**.
1. In the **Which standard attributes do you want to require?** section, check the following:
    * address
    * email
    * family name
    * given name
    * phone number
1. Click **Next Step**.
1. Select **MFA and verifications** on the left-side menu and set:
    * **Do you want to enable Multi-Factor Authentication (MFA)** to **Off**
    * **Which attributes do you want to verify?** to **Email**
1. Click **Save Changes**.
1. Select **App clients** on the left-side menu, then click **Add an app client**.
1. Enter an App client name such as `AlexaDemoSkill`.
1. Enter `3650` in the **Refresh token expiration (days)** field.
    > For Alexa account linking, it is best practice to have refresh tokens that do not expire. Amazon Cognito allows a maximum expiry time of 3650 days (10 years), so we will use that maximum.
1. Ensure that the **Generate client secret** box is checked. (The remaining boxes should be un-checked.)
1. Click **Create App Client**.
1. Select **Review** on the left-side menu and click **Create pool** at the base of the page. Once created, you will be presented with a message saying **Your user pool was created successfully**.
1. Copy the **Pool Id** to your **Scratch-Pad**.
    > This is only needed if you will be using the CLI to create your test user.
1. The left-sde menu will have changed. Select **General settings** >> **App clients** on the left-side menu, and select **Show Details**.
1. Copy the **App client id** and **App client secret** to your **Scratch-Pad**.
1. Select **App integration** >> **App client settings** on the left-side menu. Under **Enabled Identity Providers**, check the box next to **Cognito User Pool**.
1. Next, construct the Callback URL list.
    1. In a scratch space (like your **Scratch-Pad**), replace the placeholder value `<VID>` in these URL's with your vendor Id (which you should find in your **Scratch-Pad**):
        ```
        https://alexa.amazon.co.jp/api/skill/link/<VID>
        https://layla.amazon.com/api/skill/link/<VID>
        https://pitangui.amazon.com/api/skill/link/<VID>
        ```
        > Note: These three URL’s correspond to the three Alexa regions: FE (co.jp), EU (layla) & NA (pitangui).
    1. Combine them into a single comma-separated value. For example, if your Vendor Id is M12AB34CD56EF7, the result would be:
        ```
        https://alexa.amazon.co.jp/api/skill/link/M12AB34CD56EF7,https://layla.amazon.com/api/skill/link/M12AB34CD56EF7,https://pitangui.amazon.com/api/skill/link/M12AB34CD56EF7
        ```
1. Copy/paste ths comma-separated Callback URL list into the **Callback URL(s)** field. 
1. Further down the same page, under **OAuth 2.0** and **Allowed OAuth Flows**, check the box titled **Authorization code grant**.
1. Under **Allowed OAuth Scopes**, check these boxes:
    * **openid**
    > The openid scope returns all user attributes in the ID token that are readable by the client. The ID token is not returned if the openid scope is not requested by the client.
    * **aws.cognito.signin.user.admin**
    > The aws.cognito.signin.user.admin scope grants access to Amazon Cognito User Pool API operations that require access tokens.
    * **profile**
    > The profile scope grants access to all user attributes that are readable by the client.
    > Note: **phone** and **email** are included in the **profile** scope so no need to tick these boxes.
1. Click **Save changes**.

## Setup Cognito OAuth domain
There are two options for setting your Cognito OAuth domain:
* **Use a Cognito Domain.**  This option can only be used for trial and demonstration purposes. 
* **Use your own domain.** This option is required if you intend to publish a skill that makes use of this Cognito pool.
  > Note: You need to own the OAuth domain if you wish to publish a skill (or skills) that uses this OAuth system.

### Use a Cognito Domain

Since you're just trying this out, you can use a Cognito domain.

1. Select **App integration** >> **Domain name** from the left-side menu.
1. Chose a domain prefix (e.g. **myoauth**) and enter it into the **Domain Prefix** field.
    > Note: The domain prefix has to be unique in the chosen AWS region.
1. Click **Check availability**.
1. If the domain prefix is not available, pick a new one and repeat the checking process.
1. Once you have found an available domain prefix, click **Save changes**.
1. Select **App integration** from the left-side menu.
1. Copy the full URL (e.g. https://myoauth.auth.us-west-2.amazoncognito.com) shown in the **Domain** field to your **Scratch-Pad**.

### Use Your Own Domain

If you are unsure about the management of SSL certificates for your domain, contact your network administrator.  This sample assumes you have a domain managed by Amazon Route 53.  Domains managed elsewhere may have different steps, which are outside the scope of this sample.

1. Select **App integration** >> **Domain name** from the left-side menu.
1. Click **Use your domain**. If you don’t have any existing managed certificates, then you will see the message **We didn't find any AWS managed certificates for this region. To add one, click here.**
    1. Click **click here** to start the Amazon Certificate Manager (ACM) creation process.
    1. Verify you are in the **us-east-1** region for this step. If not, switch to it.
    1. On the **Certificates Manager** console, click **Request a certificate**.
    1. Select **Request a public certificate**.
    1. Click the **Request a certificate** button.
    1. Enter your domain name in the **Domain name** entry field, such as `auth.mydomain.com` and click **Next**.
    1. Select **DNS validation** and click **Review**.
    > If you don't have the necessary permissions to use this method, choose **Email validation** instead.
    1. On the next screen, click **Confirm and request**.
    1. Click **Continue**.
    > Add a CNAME to your domain using the details provided. This process will vary depending o the domain hosting provider (eg, Route 53) which you are using. For Route 53 hosted zones, continue with this section.
    1. Expand the **Domain** entry for the domain you created and is pending validation.  Click **Create record in Route 53**.
    1. Review the details and then click **Create**.
    > It can take 30 minutes or longer for the changes to propagate and for AWS to validate the domain and issue the certificate. 
    1. Once the certificate is validated, return to the Cognito console and the region in which you created your User Pool.
1. Enter the **Domain Name** and select the **AWS Managed Certificate**.
1. Click **Save Changes**.
1. Copy the **Alias Target** to your **Scratch-Pad**.
1. Create the alias record in Route53.
    1. Navigate to the [Route53 console](https://console.aws.amazon.com/route53/home).
    1. Click on **Hosted zones**.
    1. Click on your domain.
    1. Click on **Create Record Set**.
    1. Enter the subdomain into the **Name** field.
    1. Set the type to **A - IPv4 address**.
    1. Set **Alias** to **Yes**.
    1. Paste the Alias Target from your **Scratch-Pad** to the **Alias Target** field.
    1. Click **Create**.
1. Return to the Cognito console.
1. Select **App integration** from the left-side menu.
1. Copy the full URL (e.g. https://auth.mydomain.com) shown in the **Domain** field to your **Scratch-Pad**.

## Summary

Congrats!  You've created your User Pool and are ready to move on to the next step of creating the AWS IAM role which will be used by the AWS Lambda function that backs your skill.

To continue using the AWS Console, click [here](./setup-iam.md).
If you'd prefer to switch to the CLI, click [here](./setup-iam-using-cli.md). 
