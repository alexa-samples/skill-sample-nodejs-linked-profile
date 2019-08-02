# Linked Profile (Account Linking) Sample Skill - Alexa Skill Setup

In this section, you will create a skill configured to support account linking with the Cognito system created earlier. If you prefer to use the CLI, click [here](./setup-skill-using-cli.md)

## Create Skill
1. Login to the Alexa Skills Kit developer console using your Amazon Developer account:
https://developer.amazon.com/alexa/console/ask
1. From the **Alexa Skills Kit Developer Console**, click **Create Skill**.
1. Specify the basic settings for your skill:
    * Enter a skill name such as `Linked Profile Sample`.
    * Select one of the supported locales (English-AU, English-US or English-UK)
    * Select the **Custom** interaction model
    * Select **Self Hosted**
1. Select the **Start from scratch** template.
1. Click the **Create a skill** button on the top-right. 
1. Select **Interaction Model** >> **JSON Editor** on the left-side menu. Select the corresponding model for your locale from the [models](../models/) folder.  (E.g. for English-AU use en-AU.json)  Either drag/drop the file into the area of the JSON Editor that says **Drag and drop a .json file**, or copy/paste the contents of the file, being sure to replace the entirety of the existing interaction model.
1. Click the **Save Model** and then the **Build Model** buttons.

## Create AWS Lambda Function

1. Create an AWS Lambda function using the premium facts skill application as a template.
    1. Start the creation process by clicking [here](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/create/app?applicationId=arn:aws:serverlessrepo:us-east-1:173334852312:applications/alexa-skills-kit-nodejs-premium-facts-skill)
    1. Update the **Application name** to `Linked-Profile-Sample-Skill`.
    1. Update the **SkillDescription** field.
    1. Update the **SkillFunctionName** to `ask-linked-profile`.
    1. Click **Deploy**.
    1. Once the application has been deployed, click on **SkillFunctionResource** link.
1. Scroll down to the **Function Code** section.
1. Replace the contents of the **index.js** file with the contents of the [index.js](../lambda/custom/index.js) from this repo.
1. Scroll down to the **Environment variables** section.
1. If your Cognito User Pool was not created in the us-east-1 (N. Virginia) region, create an environment variable named `COGNITO_REGION`.
    1. In the **Key** field, enter `COGNITO_REGION`.
    2. In the **Value** field, enter the corresponding region code (e.g. us-east-1):
        * For N. Virginia, enter `us-east-1`
        * For Oregon, enter `us-west-2`
        * For Tokyo, enter `ap-northeast-1`
        * For Ireland, enter `eu-west-1`
1. Scroll down to the **Execution Role** section. 
1. Set the **Execution Role** to the role name that you created previously, i.e. **linked-profile-role**.
1. Select **Save** at the top of the page.
1. Copy the full function ARN to your **Scratch-Pad**.
1. Leave the Lambda console open as you can come back to restrict the function to be used by just your skill.

## Connect the Skill with the Lambda Function

1. Select **Endpoint** on the left-side menu and select the **AWS Lambda ARN** circle.
1. Enter the Lambda function ARN (copied to the scratchpad) into the **Default Region** field.
    > If you attempt to save the endpoint pointing to the Lambda function before a valid Alexa Skill Kit trigger has been added to the function, you will see a "Save Failed" error stating "The trigger setting for the Lambda {arn} is invalid."  Simply continue with adding the trigger and save it after adding the trigger. 
1. Copy **Your Skill ID** (click the **Copy to Clipboard** link) and go back to the Lambda console, leaving the developer portal tab/browser open.
1. If there is an existing **Alexa Skills Kit** trigger, click it, then click the **Delete** button.
1. Under **Add triggers** on the left-side, select **Alexa Skills Kit**.
1. Scroll down and find the **Skill ID** field, and paste in the skill ID from your clipboard.
1. Ensure that the **Enable** option is selected and then click the **Add** button.
1. Click **Save** near the top-right of the Lambda console.
1. Go back to the Alexa developer portal and select the **Save Endpoints** button.
1. Select **JSON Editor** on the left-side menu and then select the **Build Model** button at the top (next to Save Model). When the build is finished, move to next step.

## Configure Account Linking for the Skill
1. Select **ACCOUNT LINKING** on the left-side menu and change the slider switch to on.
    1. In most scenarios, you will also enable the setting **Allow users to enable skill without account linking**.  This will allow customers to engage with your skill prior to being required to either link or create an account for it.  In our case, there is no meaningful functionality if the account is not linked, so we are not enabling this option.
1. Select **Auth Code Grant** for Authorization Grant Type. 
1. For **Authorization URI**, replace `<your_domain>` with your domain and `<VID>` with your VendorID in the following URL:
    ```
    https://<your_domain>/oauth2/authorize?redirect_url=https://pitangui.amazon.com/api/skill/link/<VID>
    ```
    > The domain and Vendor ID should be saved in your **Scratch-Pad**.
    The example Authorization URL for the domain of myoauth and vendor ID of M12AB34CD56EF7 would be:
    ```
    https://myoauth.auth.us-east-1.amazoncognito.com/oauth2/authorize?redirect_url=https://pitangui.amazon.com/api/skill/link/MXXXXXXXXXXX
    ```
    > This URL is where the customer is sent when starting the account linking process.
1. For **Access Token URI**, replace `<your_domain>` with your domain in the following URL:
    ```
    https://<your_domain>/oauth2/token
    ```
    An example Access Token URI for the domain of myoauth would be:
    ```
    https://myoauth.auth.us-east-1.amazoncognito.com/oauth2/token
    ```
1. For **Client ID** and **Client Secret**, enter the corresponding values that you saved in your **Scratch-Pad**.
1. Leave Client Authentication Scheme as **HTTP Basic (Recommended)**.
1. Click **+ Add scope** and enter `openid`.
1. Click **+ Add scope** and enter `profile`.
1. Click **+ Add scope** and enter `aws.cognito.signin.user.admin`.
1. Click **+ Add domain** and enter your domain name stored in your **Scratch-Pad**.
    > **Important!** Do not include the `https://` in the Domain List value, just include the domain.
1. Click the **Save** button on the top-right and you are done.

## Summary

Great job!  You've created and configured your skill, including the Lambda function, and now you're ready to try it out!  To continue, click [here](./try-it-out.md).
