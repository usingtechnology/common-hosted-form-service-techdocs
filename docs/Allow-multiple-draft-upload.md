[Home](.) > [CHEFS Capabilities](CHEFS-Capabilities) > [CHEFS functionalities](CHEFS-functionalities) > **Allow multiple draft upload**
***

This new feature allows you to upload your draft submissions using the User Interface by simply providing a JSON file. Each object in this JSON file serves as a separate draft submission. You can download a Form-specific JSON file, also known as a Template file, and modify it to add multiple submissions as objects. So, you can easily submit multiple drafts with just one file upload!

**Things to remember:**

* Each submission created via this feature will be saved as a draft.
* Template files may vary for particular form versions.
* To enable this feature form designer/owner should enable the Save and Edit option under Form Functionality.
* In order to use Number fields as a bulk upload component, Number field must be enabled as required field or supply any value.
* In order to add a number component into sample/template for bulk upload, number component must be supplied with a default value like 0.

**How it works:**

Step 1: By default, Allow multiple draft upload option is disabled under form functionality. One can enable it by checking the checkbox. Remember that Enabling this “Allow multiple draft upload” feature will automatically enable the “Save and Edit Drafts” option.

![image](https://user-images.githubusercontent.com/87393930/232624089-c9afa2a4-6d6b-4093-8203-847e056d273d.png)

When Submitters access the form, they can see an option in the Top-Right corner to switch to Multiple draft uploads. The position of this icon may look like this.

![image](https://user-images.githubusercontent.com/87393930/232624312-8d191efa-117c-49ad-a106-8ea035289b1c.png)

When the Submitter clicks on that icon, Submitter can see a changing view on the page. This view has a drag-and-drop area to upload a Template file with all the draft submissions.

![image](https://user-images.githubusercontent.com/87393930/232624488-f6568f48-65d0-4440-bac7-e9e06b3b2b5a.png)

As you can see, there are two comments on the last screenshot. One is to download the template for the form. Remember that templates may vary for a specific version of the form. The other area is to upload a JSON file containing draft submissions. Submitter can use the same template file and modify it as per requirement. Remember that JSON has multiple objects, and each object is a draft submission.

When you modify the JSON template file for a basic form that has only two text fields i.e. First name and Last Name, then the Jason file may look like this.
![image](https://user-images.githubusercontent.com/87393930/232624604-be548c26-9d90-4f1d-99eb-92de333bbcf3.png)

In this JSON template, there are three Draft submissions. See the video below to know how to upload a JSON template. Once you upload JSON it will process the file and submit all the draft submissions collected from the JSON template file.

https://user-images.githubusercontent.com/87393930/232624770-6c31c760-f5be-40af-b253-9154e04e1148.mp4

**[Back to top](#top)**
