[Home](.) > [CHEFS Capabilities](CHEFS-Capabilities) > [Integrations](Integrations) > **Excel Power Query Integration**
***

## Excel Integration 

Microsoft Excel is one of many ways to work with form submission data. 

### Excel Power Query 

By getting data from the Web and creating a new Power Query you can work with the submission data. 

### CHEFS Form Information 
You will need this information about your form:   
* The formId. One way to retrieve this is to navigate to your form The URL in the browser window will contain ```.../form?f={formId}```   
* Your form's [API Key](https://github.com/bcgov/common-hosted-form-service/wiki/Generating-API-keys) 

### Query Configuration: Submissions 

* In the ribbon at the top of Excel in the Data menu, select: 
```Get Data > From Other Sources > From Web ```

![excelPowerQuery1](https://github.com/bcgov/common-hosted-form-service/assets/25111805/f049d28a-ee28-4c9a-80fb-018f01730ee4)   

* Enter the following URL replacing the {formId}:  
```https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/export?format=json ```
  * Choose ```Basic``` for the authorization type, 
  * For "User name" use your formId and "Password" set to your API Key 
  * In “Select which level to apply these settings to”, choose a URL with the formId included in it so that the password only applies to this form. 

* Double-click the file to open it   
![excelPowerQuery2](https://github.com/bcgov/common-hosted-form-service/assets/25111805/9e4d76b8-cddb-47a7-9be4-b2b75380d8a6)   
* Edit Settings   
![excelPowerQuery3](https://github.com/bcgov/common-hosted-form-service/assets/25111805/6322c09b-8d22-4f1e-9c44-766b6da6e9e8)   
* Choose Json and OK   
![excelPowerQuery4](https://github.com/bcgov/common-hosted-form-service/assets/25111805/0e9b0fc5-9fbe-4dc1-a962-0206e040946d)   
* You should now see submission Records   
![excelPowerQuery5](https://github.com/bcgov/common-hosted-form-service/assets/25111805/8d864f40-bad6-47a7-8e21-9a82a11f1f5e)  
* Convert to a Table   
![excelPowerQuery6](https://github.com/bcgov/common-hosted-form-service/assets/25111805/8204dc18-293a-417f-b6aa-02b2bd5b80a0)  
![excelPowerQuery7](https://github.com/bcgov/common-hosted-form-service/assets/25111805/b78e1a76-1714-4ba4-9b34-27a092e41028)

* Now we need to Expand the submission Records. Click the Column Select button:   
![excelPowerQuery8](https://github.com/bcgov/common-hosted-form-service/assets/25111805/0b1e898e-b64f-45ab-99dd-6497a0fc9f1d)   
* Select the columns you’d like to keep and OK   
![excelPowerQuery9](https://github.com/bcgov/common-hosted-form-service/assets/25111805/f1090944-c92f-4d58-b45f-587bf114b3a9)  
* Scan the columns. Some nested data may need to be expanded further. Follow the same process to expand the data   
![excelPowerQuery10](https://github.com/bcgov/common-hosted-form-service/assets/25111805/0be5f675-cacc-4b9f-9692-c8af36f128b5)   
![excelPowerQuery11](https://github.com/bcgov/common-hosted-form-service/assets/25111805/5fdbee7e-73a8-401d-bed4-b20fe562d28d)  
* Expanded data will be listed   
![excelPowerQuery12](https://github.com/bcgov/common-hosted-form-service/assets/25111805/f9b1263a-951a-4585-9f99-625e903b3649)  
* [Transform and/or Combine data](https://support.microsoft.com/en-us/office/about-power-query-in-excel-7104fbee-9e62-4cb9-a02e-5bfb1a6c536a) (optional, e.g. parse dates, format text, filter form version, etc)   
* Close and Load the data 
![excelPowerQuery13](https://github.com/bcgov/common-hosted-form-service/assets/25111805/12fe1ccf-08a7-44c8-9ddd-841adfc8b109)  
* Edit the query if needed   
![excelPowerQuery14](https://github.com/bcgov/common-hosted-form-service/assets/25111805/c86e3498-673e-49b4-980e-bea143f7ee94)  
* Refresh data on demand, or review Connection Properties to set a refresh schedule   
![excelPowerQuery15](https://github.com/bcgov/common-hosted-form-service/assets/25111805/11733905-9530-4e89-9150-ec1124d12a1c)  
