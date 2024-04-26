[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Excel Power Query Integration**
***

## Excel Integration 

Microsoft Excel is one of many ways to work with form submission data. 

### Excel Power Query 

By getting data from the Web and creating a new Power Query you can work with the submission data. 

### CHEFS Form Information 
You will need this information about your form:   
* The formId. One way to retrieve this is to navigate to your form The URL in the browser window will contain ```.../form?f={formId}```   
* Your form's [API Key](../Data-Management/Generating-API-keys) 

### Query Configuration: Submissions 

* In the ribbon at the top of Excel in the Data menu, select: 
```Get Data > From Other Sources > From Web ```

![excelPowerQuery1](images/ex1.png)   

* Enter the following URL replacing the {formId}:  
```https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/export?format=json ```
  * Choose ```Basic``` for the authorization type, 
  * For "User name" use your formId and "Password" set to your API Key 
  * In “Select which level to apply these settings to”, choose a URL with the formId included in it so that the password only applies to this form. 

* Double-click the file to open it   
![excelPowerQuery2](images/ex2.png)   
* Edit Settings   
![excelPowerQuery3](images/ex3.png)   
* Choose Json and OK   
![excelPowerQuery4](images/ex4.png)   
* You should now see submission Records   
![excelPowerQuery5](images/ex5.png)  
* Convert to a Table   
![excelPowerQuery6](images/ex6.png)  
![excelPowerQuery7](images/ex7.png)

* Now we need to Expand the submission Records. Click the Column Select button:   
![excelPowerQuery8](images/ex8.png)   
* Select the columns you’d like to keep and OK   
![excelPowerQuery9](images/ex9.png)  
* Scan the columns. Some nested data may need to be expanded further. Follow the same process to expand the data   
![excelPowerQuery10](images/ex10.png)   
![excelPowerQuery11](images/ex11.png)  
* Expanded data will be listed   
![excelPowerQuery12](images/ex12.png)  
* [Transform and/or Combine data](https://support.microsoft.com/en-us/office/about-power-query-in-excel-7104fbee-9e62-4cb9-a02e-5bfb1a6c536a) (optional, e.g. parse dates, format text, filter form version, etc)   
* Close and Load the data 
![excelPowerQuery13](images/ex13.png)  
* Edit the query if needed   
![excelPowerQuery14](images/ex14.png)  
* Refresh data on demand, or review Connection Properties to set a refresh schedule   
![excelPowerQuery15](images/ex15.png)  

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)