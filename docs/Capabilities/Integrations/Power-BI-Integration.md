[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Power BI Integration** 
***

Microsoft Power BI is one of many ways to work with form submission data. The web version of Power BI doesn't have the features needed to retrieve submissions, so download Power BI from the Microsoft Store.

## Power BI Query

By creating a new Power BI query you can work with the submission data.

### CHEFS Form Information

You will need this information about your form:
- The `formId` and `formVersionId`. One way to retrieve them is to "Manage" your form and in the table at the bottom click "Version 1" (or the version you want). The URL in the new browser window will contain ".../preview?f={formId}&v={formVersionId}"
- Your form's [API Key](../Data-Management/Generating-API-keys)

### Query Configuration: Submissions

- In the ribbon at the top of Power BI click `Get data` and select `Web`
- Use the URL `https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/versions/{formVersionId}/submissions` to get the submissions for a version of your form - you will need to replace `{formId}` and `{formVersionId}` with the values for your form
- Choose "Basic" for the authorization type, with "User name" set to your `formId` and "Password" set to your API Key

### Query Configuration: Submission Statuses

It is also possible to get the list of statuses for each submission.

- In the ribbon at the top of Power BI click `Get data` and select `Web`
- Use the URL `https://submit.digital.gov.bc.ca/app/api/v1/submissions/{formSubmissionId}/status` to get the statuses for each submission - you will need to replace `{formSubmissionId}` with the `id` value for each submission 
- Choose "Basic" for the authorization type, with "User name" set to your `formId` and "Password" set to your API Key

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)