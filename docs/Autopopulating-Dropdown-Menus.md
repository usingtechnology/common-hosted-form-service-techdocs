[Home](.) > [CHEFS Components](CHEFS-Components) > [Custom Components](Custom-components) > **Autopopulating Dropdown Menus**
***

## Examples
> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=a71bed59-de8b-4f91-a699-fd86b6dbe6ad)

> Download this example file and [import](Importing-and-exporting-form-designs) it into a new form to try it out<br>
> [example__autopopulating_dropdown_menus_schema.json](examples/example__autopopulating_dropdown_menus_schema.json)  
> When you are ready to implement it into your existing form you can follow these instructions to recreate it.

(Experimental Feature) Autopopulates the values of select list drop-downs with some advanced settings. For instance, the list of ministry names, or the list of ministry sectors.  
Demonstrates how to implement the cascading dropdown menu effect, where the selected value of one dropdown populates the values of another select list.
***

## Autopopulate values of the Select component (Tutorial)
**[Back to top](#top)**

## Option 1 - Autopopulate a "Ministry Name" Select field with the full list of ministries   
### Using a URL to a raw JSON file as the source for your "select" component dropdown menu values
This example uses JSON data from a BCGov github repo called [Ministry Org Names](https://github.com/bcgov/ministry-org-names).  

1. Drag on a new Select field from the Advanced Fields section
2. Give it a label "Ministry"
3. check the API tab that the Property Value shows as "ministry"
4. On the Data tab use the following configuration for each of the required fields in the table below  

| Configuration Field | Comments       | Value to Enter.            |     
| ------------------- | -------------- | -------------------------- |  
| Data Source Type    |                | URL                        |  
| Data Source URL     || ```https://raw.githubusercontent.com/bcgov/ministry-org-names/main/organization-groups.json``` |   
| Lazy Load Data      | your choice    | checked                    |  
| Data Path           || ```items[0].organizations[5].ministries``` |   
| Storage Type        | your choice    |  ```Autotype```            |   
| Value Property      |can be ```name``` or ```acronym```|```name```|   
| Item Template       || ```<span>{{ item.name }}</span>```         |   
| Enable Static Search| your choice    | checked                    |   

For all other values use the defaults. If done correctly, the preview window will now show the JSON data in the select list drop-down.  
![Screenshot 2023-07-10 at 11 35 34 AM](https://github.com/bcgov/common-hosted-form-service/assets/25111805/2236c1be-a2da-4e61-b752-a503ef544520)

## Option 2 - Autopopulate a "Sector Name" Select field with the full list of sectors  
### Using a URL to a raw JSON file as the source for your "select" component dropdown menu values
This example uses JSON data from a BCGov github repo called [Ministry Org Names](https://github.com/bcgov/ministry-org-names).  

1. Drag on a new Select field from the Advanced Fields section
2. Give it a label "Sector"
3. check the API tab that the Property Value shows as "sector"
4. On the Data tab use the following configuration for each of the required fields in the table below  

| Configuration Field | Comments       | Value to Enter.          |     
| ------------------- | -------------- | ------------------------ |  
| Data Source Type    |                | URL                      |  
| Data Source URL     || ```https://raw.githubusercontent.com/bcgov/ministry-org-names/main/organization-groups.json``` |   
| Lazy Load Data      | your choice    | unchecked                |  
| Data Path           |                | ```items[1].sectors```   |   
| Storage Type        | your choice    | ```Autotype```           |   
| Value Property      |                | ```sectorname```         |   
| Item Template       || ```<span>{{ item.sectorname }}</span>``` |   
| Enable Static Search| your choice    | checked                  |   


## Option 3 - Auto populate the values of a "Ministry" Select component based on the selected Sector name  
### Uses the selected value (a JSON object) of Option 2 as the source for your "Text Field" component value   

1. Drag on a new Text Field from the Advanced Fields section
2. Give it a label "Sector Ministry"
3. For the Placeholder, type ```To begin, first select a Sector```
4. On the Data tab use the following configuration for each of the required fields in the table below  

| Configuration Field            | Comments       | Value to Enter or Select   |     
| ------------------------------ | -------------- | -------------------------- |  
| Data Source Type               |                | Custom                     |  
| Storage Type                   |                | Autotype                   |   
| Item Template                  |clear this field|                            |   
| Refresh Option On              |                | Sector                     |  
| Clear Value On Refresh Options |                | checked                    |  
| Enable Static Search           | your choice    | unchecked                  |
| Custom Default Value   | To automatically select first item in the prepopulated dropdown   |`value = instance.defaultDownloadedResources[0];`    |
| Custom Values                  | javascript code| see below                  |  

Custom Values JavaScript code  

```javascript
if (data.sector !== "") {
  values = Promise.resolve(
    fetch('https://raw.githubusercontent.com/bcgov/ministry-org-names/main/organization-groups.json')
      .then((response) => response.json())
      .then((json) => {
          const ministries = json.items[1].sectors.filter(sector => sector.sectorname === data.sector)[0].ministries;
          return ministries.map(m => m.name);
      })
    );
}
```

For all other values use the defaults.  
If done correctly, selecting a value for Sector will autopopulate the values of this select list drop-down.   

<details>
<summary>**TLDR** Explanation of the **Custom Values** JavaScript</summary>     
```data.sector``` contains the value that was selected for the question named "sector".   
The value contains a JSON Object that consisting of the sectorname as well as a list of ministries.  

Example for the Natural Resource Sector:  

```json  
    {
      "sectors": [
        {
          "sectorname": "Natural Resource Sector",
          "ministries": [
            {"name": "Agriculture and Food", "acronym": "AF"},
            {"name": "Energy, Mines and Low Carbon Innovation", "acronym": "EMLI"},
            {"name": "Environment and Climate Change Strategy", "acronym": "ENV"},
            {"name": "Forests", "acronym": "FOR"},
            {"name": "Indigenous Relations & Reconciliation", "acronym": "IRR"},
            {"name": "Water, Land and Resource Stewardship", "acronym": "WLRS"}
          ]
        }
      ]
    }  
```  
The block of JavaScript fetches the full list of all sectors and ministries and uses the data.sector value to filter the list of values that it will display as the options in this Select component.   
</details>

## Option 4 - Auto populate the values of a "Primary Sector" Select component based on the selected Ministy name  
### Uses the selected value (a JSON object) of Option 1 as the source for your "Select" component value   

1. Drag on a new Select component from the Advanced Fields section
2. Give it a label "Primary Sector"
3. For the Placeholder, type ```To begin, first select a Ministry```
4. On the Data tab use the following configuration for each of the required fields in the table below  

| Configuration Field            | Comments       | Value to Enter or Select   |     
| ------------------------------ | -------------- | -------------------------- |  
| Data Source Type               |                | Custom                     |  
| Storage Type                   |                | Autotype                   |   
| Item Template                  |clear this field|                            |   
| Refresh Option On              |                | Sector                     |  
| Clear Value On Refresh Options |                | checked                    |  
| Enable Static Search           | your choice    | unchecked                  |
| Custom Default Value   | To automatically select first item in the prepopulated dropdown   |`value = instance.defaultDownloadedResources[0];`    |
| Custom Values                  | javascript code| see below                  |  

Custom Values JavaScript code  

```javascript
if (data.ministry !== "") {
  values = Promise.resolve(
    fetch('https://raw.githubusercontent.com/bcgov/ministry-org-names/main/organization-groups.json')
      .then((response) => response.json())
      .then((json) => {
          return [json.items[0].organizations[5].ministries.filter(min => min.name === data.ministry)[0].sectors[0].sectorname];
      })
    );
}
```

For all other values use the defaults.  
If done correctly, selecting a value for Sector will autopopulate the values of this select list drop-down.   

<details>
<summary>**TLDR** Explanation of the **Custom Values** JavaScript</summary>     
```data.sector``` contains the value that was selected for the question named "sector".   
The value contains a JSON Object that consisting of the sectorname as well as a list of ministries.  

Example for the Natural Resource Sector:  

```json  
"sectors": [
    {
     "sectorname": "Governance Sector"
    },
    {
     "sectorname": "Economy Sector"
     }
   ] 
```  
The block of JavaScript fetches the full list of all sectors and ministries and uses the data.ministry value to filter the list of values that it will display as the options in this Select component.  
</details>

### Conditional logic
Show and hide form fields with [conditional logic](Conditional-forms-fields).
In the provided example for this page we used a Simple Conditional for the "Secondary Sector" field which hides itself when "Primary Sector" has an empty value.  To express an empty value or a field that has nothing entered, just leave the "Has the value:" field blank.

**[Back to top](#top)**