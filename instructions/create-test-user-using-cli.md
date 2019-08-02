# Linked Profile (Account Linking) Sample Skill - Create test user

In this section, you will create a test user using the AWS CLI.

1. Create the user, specifying a username of your choice by replacing `<username>` and by replacing `<user-pool-id>` with the User Pool Id you stored in your **Scratch-Pad**:
```
aws cognito-idp admin-create-user --user-pool-id <user-pool-id> \
--username <username> --user-attributes Name=email,Value=<username>
```
Example:
```
aws cognito-idp admin-create-user --user-pool-id us-east-1_AbCdef0XY --username myusername --user-attributes Name=email,Value=myemail@myemaildomain.com
```
1. Update the newly created user, adding given_name, family_name, phone_number and address with the following command (replacing the placeholder values).  The `<username>` must be same as specified in previous step, and `<user-pool-id>` again is the value stored in your **Scratch-Pad**.
> You might find it easier to update the command in your scratch space and paste it to the command line.
```
aws cognito-idp admin-update-user-attributes --user-pool-id <user-pool-id> --username <username> --user-attributes \
Name=given_name,Value=<given-name> \
Name=family_name,Value=<family-name> \
Name=phone_number,Value=<phone-number> \
Name=address,Value=<address>
```
Example:
```
aws cognito-idp admin-update-user-attributes --user-pool-id us-east-1_AbCdef0XY --username myusername --user-attributes \
Name=given_name,Value=myfirstname \
Name=family_name,Value=mylastname \
Name=phone_number,Value=+181818181 \
Name=address,Value="1 Anywhere Lane\, Seattle\, Washington"
```
> Note: Values with spaces must be quoted.  Values with commas must have the command escaped by preceding it with a back-slash "\".

## Summary

Your user has been created.  Now, return to the previous page to continue by [confirming the test user](./try-it-out.md#confirm-the-test-user).
