[Home](index) > [Developer](Developer) > [Form.io](Form.io) > **Form.io validation**
***

[Form.io](http://form.io/) not only serves as a Form platform for your Serverless applications but can also serve as a complete REST API platform as well. This is because everything that happens within [Form.io](http://form.io/), does so through the use of a robust REST API call within the form platform.

The following documentation outlines a complete walkthrough of using the [Form.io](http://form.io/) API platform for validating a form.

To use [Form.io](http://form.io/) first we have to create an account next create a project, setup it, and create a form.

How to use the [Form.io](http://form.io/) API to validate a form.

1. We have to login 

![image](images/formio1.png)

From the response’s header get the x-jwt-token and save it in a variable if you are using POSTMAN and from the body of response you will find login info about the user and list project.

2) To validate a form we need 2 things the PROJECT_ID and the FORM_NAME  now we can format the ENDPOINT like that 

![image](images/formio2.png)

To validate a form there is 3 sections that interest us:

Validation 

Conditional 

Logic

For the validation section  all constraint  work except  JSONLogic Validation

For Conditional section nothing works, the API does not react on any code.

And for the logic section only simple logic works

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)