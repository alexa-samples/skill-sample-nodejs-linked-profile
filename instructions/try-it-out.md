# Linked Profile (Account Linking) Sample Skill - Try It Out

In this section you will create a user, and use it to link your skill with the profile.

## Create a Test User
The simplest way to create a user is to do so via the account linking process in the Alexa website.

1. Login to the Alexa website for your region (eg, alexa.amazon.com) using the same developer.amazon.com account in which you have created the skill.
> You can also do this using the Alexa App on your phone.
1. Navigate to your skill's detail page.
    1. Click on **Skills**.
    1. Click **Your Skills**.
    1. Click on the **DEV SKILLS** tab.
    1. Find the skill you created and click on it.
1. Click **Enable**.  If already enabled, click **Settings** and then click **Link Account**.
1. A new browser tab will open. If you would prefer to use the AWS CLI to create the user, click [here](./create-test-user-using-cli.md). Otherwise, create the user by:
    1. Click **Sign up** at the base of the login window. This will convert the form into a Cognito account sign-up page.
      > This form's style and branding can be changed from the Amazon Cognito console.  Make the changes in the **App integration** >> **UI customization** section.
    1. Enter an email, address, phone number (including country code!), given name and family name.
        > The email address can be fake, as you can enable the account using the Cognito console. If you use a real email (i.e. one you have access to), then you will receive a verification email.  It can take a few minutes to arrive, so rather than waiting we'll use the console instead.
        > The verification email can be customized using the Amazon Cognito console.  Make changes in the **General settings** >> **Message customizations** section.
    1. Enter a password.
        > The password policy is configurable from the Amazon Cognito console.  Adjust the policy from the **General settings** >> **Policies** section.
    1. Click **Sign up**.
    1. At this point, you will be asked to enter a verification code. If you don't want to wait for the verification email (or you don't have access to the email sent to that address), you can close this browser tab and move to the next section as you can verify the account through the Cognito console.
    1. Enter the verification code and click **Verify**.

## Confirm the Test User and Finish Account Linking
If you verified the test account using the verification code, skip to the next section.

1. Check that the user was created successfully by going to the [Your User Pools](https://console.aws.amazon.com/cognito/users) section of the Cognito console.
1. Click the user pool you created (e.g. **Alexa Skill Users**).
1. Select **General settings** >> **User and groups**.
    > Note: You may notice a **Create User** option.  We don't use the Cognito Console to create users because those users would not have the additional profile fields of address, given_name and family_name.
1. Select the username with the most recent creation date (it should be the only one if this the first user created in the pool).
1. Check that this entry has a value for given_name, family_name, email, phone_number and address.
1. Click **Confirm user** to verify the user.
1. Return to the skill detail page in the Alexa app.
1. Click **Settings** and then **Link Account** to restart the account linking process.
1. Enter the email and password for the newly verified account.
1. Your skill and account are now linked.  Close the browser tab.

## Test it!
1. Go back to the Amazon Developer console and click on the **Test** tab. Test out the skill using utterances such as these:

*open link demo*
*hello*
*what is my name*
*what is my number*
*what’s my address* 
*what’s my number*
*what is my email*
*stop*

> You can also test these utterances out using a device associated with your Developer Account or from the ASK CLI using either the `ask simulate` or `ask dialog` commands.

## Summary

Congratulations!  You should have successfully created a Cognito User Pool, a skill that uses that pool, a user in that pool, and linked the skill with that account.

This sample can be something you're going to use just for learning, or as the basis for a skill you're building to work with Alexa for Business or for the Alexa Skill Store.  Whatever is next, we look forward to seeing what you build!
