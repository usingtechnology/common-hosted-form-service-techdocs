[Home](index) > **Product Roadmap**
***

![img](images/product_roadmap.png)



Below is a rough outline of the features that we are targeting for CHEFS. [Post your ideas, leave a comment or vote on what CHEFS features we should build next ](https://chefs-fider.apps.silver.devops.gov.bc.ca/)






<details>
  <summary><strong>VX.X - FUTURE PLANS....(expand)</summary>
  
  * [ ] Integrate with COMS for file uploads and to allow access to attachments via the API
* [ ] Show notes in exported submissions via API (would need to be configurable, so the form owners could allow that or not)
* [ ] Improve the Submissions View (option to view forms in print or form view, so people can print forms with tabs in one print request)
* [ ] Add time to date range parameter for exporting submissions
* [ ] Reviewers can download multiple submissions at once and attach a template permanently
* [ ] Include fields in email notifications (customizable email templates)
* [ ] Custom spatial form component (click the map and the form records the lat/long)
* [ ] Filter list of submissions with the API
* [ ] Customization submission summary dashboard (counts, totals, or averages on charts)
* [ ] View submission versions
* [ ] Auto-save a form during build
* [ ] Virus scan file uploads; possibly then allow public forms to allow file uploads
* [ ] Multi authentication methods (ie both Business BceId and IDIR??) 
</details>

***



## v1.5.0
<!-- **[Back to top](#top)** -->

* [x] Updated role permissions
* [x] Navigation bar links updated based on identity provider (IDIR/BCeID Basic/BCeID Business)

New Features
* [x] Users can now add BCeID Basic and BCeID Business as team members on their form  - **[Link](https://github.com/bcgov/common-hosted-form-service/wiki/Managing-admin-teams)** 
* [x] Users can now add BCeID Basic and BCeID Business as team members on their drafts
* [x] Ability to create a new submission from an existing one using a property in the form designers basic fields - **[Link](https://github.com/bcgov/common-hosted-form-service/wiki/Copy-an-existing-submission)** 
* [x] Sends a notification email reminder when a form is about to open for submission - **[Link](https://github.com/bcgov/common-hosted-form-service/wiki/Schedule-and-Reminder-notification)** 
* [x] Form schedule in form settings allows a form to open and close on a repeatable date range - **[Link](https://github.com/bcgov/common-hosted-form-service/wiki/Schedule-and-Reminder-notification)** 

Bug Fixes

* [x] The column selection filter in the submissions page now properly saves and loads previously selected columns
* [x] Error when retrieving forms if the request did not include a createdAt property that was an array of dates
* [x] Fixed a bug preventing saving a draft or submitting a form due to a missing property related to form scheduling
* [x] API section for form settings was missing due to an incorrect conditional check

</details>


***


<details>
  <summary><strong>v1.4.0 - New Sidebar, Features and Bug Fixes</strong></summary>
  
 * [x] Improved documentation and tutorials
* [x] Form Administrators are notified on status updates on forms AND can add an optional comment to submitter
* [x] Submitters are notified on status updates including completion
* [x] Authentication with Business BCeID
* [x] Added undo/re-do to the Form Designer
* [x] CHEFS Admins can change form owners
* [x] Technical Debt - confirm load and performance capability
* [x] Remove "manage forms" gear for submitters to avoid unnecessary errors
* [x] Fix file upload timeout issue

New Features

* [x] A user can filter to view their own submissions
* [x] Introduces a user-friendly sidebar to enhance the form-creation process
* [x] Deleted form submissions can now be restored
* [x] Contact information is now configurable as an environment variable

Bug Fixes 

* [x] Fixes a bug which prevented users from deleting components on a form
* [x] Team management in BCeID forms no longer retrieves and lists BCeID users
* [x] Fixes a bug which created two versions of the same form
* [x] Updated landing page videos
* [x] Fixes a bug which failed deployment to the PR environment
* [x] Fixes a bug with the undo/redo feature while tab switching

Documentation

* [x] Updates the disclaimer for public-facing forms
* [x] Updates the PR checklist for contributions

</details>



<details>
  <summary><strong>v1.3.0 - Return to User</strong></summary>
  
  * [x] Update default print header to always show BCGov logo
* [x] Return submission to submitter for edits
* [x] Update dependencies and infrastructure to Node 16 LTS
* [x] Expose JWT Token data to Formio components
</details>




<details>
  <summary><strong>v1.2.0 - Integrations</strong></summary>
  
  * [x] Access form data from external web application
* [x] Generate pdf/xls/doc of submission and reports
* [x] Authentication with BCeID
</details>


<details>
  <summary><strong>v1.1.0 - Drafts, Invitations, and Edit support</strong></summary>
  
  User Improvements

* [x] Create and edit draft submissions
* [x] Invite colleagues to draft submissions

Staff Improvements

* [x] Enhance state management and note support
* [x] Form Designer UI unification
* [x] Add submission edit support
* [x] Add soft delete submission support
* [x] CSV export format updates

Other Improvements

* [x] Update to formiojs 4.13
* [x] Convert application to JSON logging
</details>



<details>
  <summary><strong>MVP - Publishing, Uploads and Status Management</strong></summary>
  
  * [x] Publish and unpublish a form
* [x] Attach a document [Authenticated (IDIR) only]
* [x] Minimal state/status management for each form submission record
* [x] Email notification for state changes
* [x] User orientation/help materials
* [x] OpenAPI and documentation
</details>


<details>
  <summary><strong>Beta - Form Editing and Management</strong></summary>
  
  * [x] Edit form and save new version
* [x] Manage form team members and access
* [x] Marking forms as deleted
* [x] Email notifications for a submission to the form reviewer
* [x] Email notifications for a submission to the submitter
* [x] Public (anonymous) form submissions
</details>



<details>
  <summary><strong>v0.1.0 - Alpha - Functional Submissions</strong></summary>
  
  * [x] View submission page styled without the app navigation header
* [x] Styling fixes for accessibility
* [x] Privacy Risk Assessment (draft)
* [x] Download form schema in the form designer view  
* [x] Back, Refresh or Close warning before leaving the page (designer or submission)  
* [x] Export submissions for a form within date range
* [x] Home page / landing page content
* [x] Ability to refresh your browser without losing your form design progress
* [x] Disclaimer and Statement of Responsibility for Users
</details>



<details>
  <summary><strong>v0.0.1 - Alpha - Initial Proof of Concept</strong></summary>
  
 * [x] View list of forms you have some access on  
* [x] Create a new form  
* [x] Form builder (simple view)  
* [x] Form builder (advanced view)  
* [x] Save Form Design  
* [x] View a form and Submit a form to the database  
* [x] Authentication for IDIR users  
* [x] Form visibility for all IDIR  
* [x] Share button for a form to get the direct link, and generate a QR Code  
* [x] Role based access control to manage a form with 5 roles (owner, team manager, editor, form reviewer, submitter)
</details>

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)

