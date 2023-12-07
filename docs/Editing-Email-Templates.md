[Home](.) > [CHEFS Capabilities](CHEFS-Capabilities) > [CHEFS Functionalities](CHEFS-Functionalities) > **Editing Email Templates**
***

> **EXPERIMENTAL**

CHEFS sends [Email Notifications and Reminders](CHEFS-Notifications-and-Reminders) at various points in the life of a submission. To give form owners some control over the content of these emails, the ability to edit the email templates is being added to CHEFS as an *experimental feature*. This feature is being released with minimal capabilities and will be expanded in the future when time allows.

## Limitations

- Currently only the Submission Confirmation email template is editable. Other email templates will be added in the future if there is demand for them.
- Only plain text can be used in the templates. HTML markup is not supported.
- Data from the submitted form cannot be included in the emails. This is due to potential privacy impacts, but the CHEFS team is looking into being able to offer this capability.

## Submission Confirmation for Submitters

This email can be requested by the form submitter after form submission.

After the user submits the form, the successful submission page has a link to "**EMAIL A RECEIPT OF THIS SUBMISSION**":

![image](https://github.com/bcgov/common-hosted-form-service/assets/35532993/66b1bc15-48d6-41e4-a1c1-b2051398f8f2)

The email sent to the user contains a Subject, Title, and Body:

![image](https://github.com/bcgov/common-hosted-form-service/assets/35532993/8678e3ac-0429-4f60-a328-cedec2ac9fdd)

There is a button on the Form Management page to edit the email template:

![image](https://github.com/bcgov/common-hosted-form-service/assets/35532993/472c7f16-d5e7-4d75-a225-64c1049c46b3)

The default templates for Subject, Title, and Body are displayed and can be edited:

![image](https://github.com/bcgov/common-hosted-form-service/assets/35532993/9f2aca34-1b43-4c64-a212-c9f86f64d5c3)

Mustache syntax can be used to add the following fields to the templates:
- `form.name`: the "Name" of the form.
- `form.description`: the "Description" of the form.

![image](https://github.com/bcgov/common-hosted-form-service/assets/35532993/957479f4-7886-4d51-a9b4-80cff0bb54c4)

All following emails for submission confirmation will use the new templates:

![image](https://github.com/bcgov/common-hosted-form-service/assets/35532993/2b83c5cf-44d1-4966-bdda-f0640784702b)
