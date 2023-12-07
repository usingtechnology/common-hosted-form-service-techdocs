[Home](.) > [Developer](Developer) > [Contributors](Contributors) > **Keycloak configuration**
***

In a fresh install of Keycloak, you’ll need to start by creating a realm. You will need to remember this name or use the name chefs.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/ad41ab47-62fd-4478-80ce-a3efec0d7bcc)

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/f2813f7a-7416-4c29-8954-27e3aefebd61)

Once created, you’ll need to click on the Login tab and then disable Login with email and then enable Duplicate emails.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/9fbfce91-37c1-4c84-9072-37f5b88734a3)

Then you’ll need to create your clients by going to the clients tab, and clicking the Create button at the top right of the table.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/bc2f2a43-3345-4840-860d-ee5eca2424e8)

You’ll be creating one called chefs which will be your back end and one called chefs-frontend which will be your front end.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/cc66e74c-7f28-461a-b5e5-e6a12f1fe49d)

For your chefs back end, under the settings, do the following: change the access type to confidential, disable standard flow and direct access grants. Optionally, enable service accounts. Then click Save at the bottom of the page.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/03791d72-8e84-4854-81c7-73c2a2daf3f2)

In the credentials tab, you’ll want to take note of your client secret, this is used in your local.json configuration for CHEFS.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/4c4de7d2-c409-43ae-94ed-be960517a1d4)

In the scope tab, disable full scope.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/300dc228-2b30-4b93-972f-b80490edc3e4)

In the roles tab, create 4 roles.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/83e84e27-4e6d-4a01-b50f-837060934928)

First, create the user role and the admin role.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/85c6ff2e-6464-4827-b495-f42ff657bb20)

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/2ed6090a-8a36-42b8-8f04-4cedff975d83)

Then create a role called CHEFS User.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/f07d0ae1-4b2a-4758-9980-0365dba09b61)

Enable Composite Roles , in the drop down for Client Roles, select chefs and then select the user role and click Add selected.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/0ddfc4c3-7f54-452d-86e9-bd5fbdfcb6a5)

Create the role CHEFS Admin.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/c827baad-9be8-413a-8e46-29ddf99e9006)

Enable Composite Roles, in the drop down for Client Roles, select chefs and then select the CHEFS User and admin role and click Add selected for both.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/cdd7cd5f-5e13-498d-8faa-3ea14f07b843)

Back in the clients page, create another client called chefs-frontend for your front end.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/9db26eff-2d77-4bb4-a5f6-35c25aa6363f)

In the settings tab, make sure the Access Type is public and disable Direct Access Grants.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/d388d707-e68e-4b27-8d84-2a40d2e78be7)

Set the Root URL and Admin URL to the host your CHEFS app will be listening on. In this example, it’s listening on http://localhost:8081. Set the Web Origins to * to allow all origins. Then click Save at the bottom of the page.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/3dd88f10-4d8b-4ef4-9a0e-7bd829afbcf9)

In the Client Scopes tab, select chefs in the Default Client Scopes under Available Client Scopes and then click Add selected.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/9b5e14fe-281a-4910-96fd-0ccc15124346)

In the roles tab, click the Add Role button to create a role.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/feeee258-6a12-4e9f-81da-5f20319de80f)

Name the first one developer.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/8e453921-902a-4a09-946d-8b4fecd5b62d)


Then create another one called Frontend Developer. Enable Composite Roles, in the Client Roles dropdown, select chefs-frontend and then click on developer and click Add selected

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/11fd42f3-1b1e-40aa-8c79-79c07b98334a)

In the Client Scopes tab, click the Create button at the top right to create a client scope.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/9b46edfa-714d-45c8-aaa2-0e318e774e0a)

Name the first one chefs and disable Display On Consent Screen.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/4d97bc94-00e4-4227-aa55-b9545e2c7dd1)

Create a protocol mapper called idir_user_guid, set the Mapper type to User Attribute then set the User Attribute to idir_user_guid, set the Token Claim Name to idp_userid, and set the Claim JSON Type to String.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/10a5cdfa-d862-45e3-87b7-cc28b1bd2677)

Create another protocol mapper called idir_username, set the Mapper type to User Attribute then set the User Attribute to idir_username, set the Token Claim Name to idp_username, and set the Claim JSON Type to String.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/3dee1521-cc5d-48e2-ab36-867279be62fb)

Create another protocol mapper called bceid_user_guid, set the Mapper type to User Attribute then set the User Attribute to bceid_user_guid, set the Token Claim Name to idp_userid, and set the Claim JSON Type to String.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/00c2ca85-0cf3-4e14-94f0-a835b281ea38)

Create another protocol mapper called bceid_username, set the Mapper type to User Attribute then set the User Attribute to bceid_username, set the Token Claim Name to idp_username, and set the Claim JSON Type to String.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/2fa2f676-c227-41b8-9ec4-467c1cdee574)

Create another protocol mapper called identity_provider, set the Mapper type to User Session Note then set the User Attribute to identity_provider, set the Token Claim Name to identity_provider, and set the Claim JSON Type to String.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/2e42fbd3-540b-46ed-8726-23cef5968aeb)

Create another protocol mapper called chefs aud, set the Mapper type to Audience then set the Included Client Audience to chefs.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/1c790858-2986-4cea-a6fc-5ec7bec04905)

Back on the Mappers tab, click the Add Builtin button.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/734bc96f-edcc-4f9f-bf67-725bcb31934f)

Check the family name, email, client roles, given name, full name, audience resolve, and username then click Add selected.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/d32ff2c0-756a-45bf-9d96-5b876ef970c2)

In the Scope tab, select chefs in the Client Roles and then select admin and user and click Add selected for both of them.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/e17834d8-1f60-47a8-93bd-4ca6ab3cf815)

Create another Client Scope called chefs-frontend and disable Display On Consent Screen.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/7883f97c-ce03-4957-956f-ef483c170ffb)

Click on the Mappers tab and then click the Create button to create some mappers.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/ecde5347-040c-4b4f-88ed-bd77d3cb8116)

Create a protocol mapper called chefs-frontend-aud, set the Mapper type to Audience then in the Included Client Audience dropdown select chefs-frontend.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/c327f961-e69f-409a-85e0-41c50297b313)

Check the family name, email, client roles, given name, full name, audience resolve, and username then click Add selected.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/b67a73b9-0960-4964-984e-51af25921d1c)

In the roles page, click on default-roles-chefs

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/0c41b1ea-53d9-4e84-a4b9-957c6cfb55d0)

In the dropdown for Client Roles, select chefs then select CHEFS User and then click Add selected.

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/cbc42cc4-3883-4c3a-b20b-9e803fd9255d)

You’ll then need to add in your required identity providers, the guide to doing so can be found:

https://stackoverflow.developer.gov.bc.ca/a/891/57

After setting up your keycloak, you’ll need to configure your local.json file for CHEFS.

There should be a block that looks like:

![image](https://github.com/bcgov/common-hosted-form-service/assets/87393930/679ea713-ff66-4572-bff0-d61c3fbff90f)

Make sure that your clientSecret is the one found in the chefs client under the Credentials tab. The serverUrl should be the host your keycloak is listening on.























