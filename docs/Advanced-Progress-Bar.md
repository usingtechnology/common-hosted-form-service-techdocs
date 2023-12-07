[Home](.) > [CHEFS Components](CHEFS-Components) > [Custom Components](Custom-components) > **Advanced Progress Bar**
***

## Examples
> Try a working example<be>
> * [View Example: Progress Bar with Validation](https://submit.digital.gov.bc.ca/app/form/submit?f=4e702761-c6af-4b10-91d0-0950b964cf4d)
> * [View Example: Progress Bar Using Layout](https://submit.digital.gov.bc.ca/app/form/submit?f=f20ac79e-14a7-464f-8139-f5c5de9133e1)
> * [View Example: Progress Bar Using Layout with Validation](https://submit.digital.gov.bc.ca/app/form/submit?f=ba809aaa-f975-42a8-bc20-8de12c11ec22)


> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<be>
> *  [example_progress_bar_with_validation_schema.json](examples/example_progress_bar_with_validation_schema.json)
>*  [example_progress_bar_using_layout_schema.json](examples/example_progress_bar_using_layout_schema.json)
>*  [example_progress_bar_using_layout_with_validation_schema.json](examples/example_progress_bar_using_layout_with_validation_schema.json)

---
## Advanced Progress Bar (Tutorial)

A custom progress bar can be added to the form to enhance the user experience and indicate the remaining steps within the form. More features have been added to advance the functionalities of the progress bar.

**Features added**

- ability to perform validity checks on all the components ( e.g. input component) in each tab component
- ability to indicate error colour in case the validity checks fail
- each progress bar step has a title that corresponds with the title of each tab of the tab component

### Type A: Progress Bar with Tab Component

This Progress Bar is designed to work with Tab Component, and with the Next and Previous Buttons

![ap1](https://user-images.githubusercontent.com/91633223/204036758-601b0034-ea20-439f-972d-b86285fa895a.png)

**Step 1**: Start by dragging an ‘HTML Component’ into the form builder.

**Step 2**: change the ‘HTML tag’ field from `p` to `div`, and in the ‘Display’ tag enter a unique and custom class name in the ‘CSS Class'. In this screenshot, we used `healthStepper`

![ec495eda-f81c-423b-82f7-6f4a025ad090](https://user-images.githubusercontent.com/91633223/204038147-e5687a6f-7716-4a88-89bb-b4dfe3d8fada.png)

**Step 3**: Copy the following code into the ‘Content’ section

```
<ol class="c-stepper">
    <li class="c-stepper__item active">
        <h3 class="c-stepper__title">Step 1</h3>
        <p class="c-stepper__desc">Facility Information</p>
    </li>
    <li class="c-stepper__item disabled">
        <h3 class="c-stepper__title">Step 2</h3>
        <p class="c-stepper__desc">Bed Occupancy</p>
    </li>
     <li class="c-stepper__item disabled">
        <h3 class="c-stepper__title">Step 3</h3>
        <p class="c-stepper__desc">Staffing Level</p>
    </li>
     <li class="c-stepper__item disabled">
        <h3 class="c-stepper__title">Step 4</h3>
        <p class="c-stepper__desc">Operating Level</p>
    </li>
    <!-- Other steps -->
</ol>
```

![ap3](https://user-images.githubusercontent.com/91633223/204038227-78443077-4ccd-4d8f-94f1-f1a2c5126b66.png)

**Step 4**: Click on the ‘Logic’ tab and click on the ‘Add Logic’ button

![ap4](https://user-images.githubusercontent.com/91633223/204038257-8064e91c-5e24-4430-82e4-f6fd64a8b216.png)

**Step 5**: Enter any name as the 'Logic Name'

![ap5](https://user-images.githubusercontent.com/91633223/204038439-3a6bad17-4151-4517-b90f-130caea4c2a4.png)

**Step 6**: In ‘Trigger' section, click on ‘Type’ dropdown menu, and select 'Javascript’

![ap6](https://user-images.githubusercontent.com/91633223/204038526-9562753f-f4a2-40e2-935c-eddde572e2a0.png)

**Step 7**: Click “Add Action“ button

![ap7](https://user-images.githubusercontent.com/91633223/204038579-7b9dd430-f113-4991-90e7-f38a95a59928.png)

**Step 8**: Enter any name in “Action Name“

![ap8](https://user-images.githubusercontent.com/91633223/204038629-8968be71-3852-436e-ac67-7aa611ce961c.png)

**Step 9**: In ‘Trigger' section, click on ‘Type’ dropdown menu, and select 'Javascript’

![ap9](https://user-images.githubusercontent.com/91633223/204038654-6da31308-b428-4f14-bc6f-f4147c7baa6b.png)

**Step 10**: Copy the following code into the ‘Text Area’ section

```
let cssId = 'myCss'; 
const head  = document.getElementsByTagName('head')[0];
if (!document.getElementById(cssId))
{
    const link  = document.createElement('link');
    link.id   = cssId;
    link.rel  = 'stylesheet';
    link.type = 'text/css';
    link.href = 'https://bcgov-citz-ccft.github.io/forminators/customprogresssteppercss/chefsCustomCss.css';
    link.media = 'all';
    head.appendChild(link);
}
```

![ap10](https://user-images.githubusercontent.com/91633223/204038753-ae1f72f5-b643-4576-85f2-668f5dec9ec6.png)

**Step 11**: Click on ‘Save Logic’ and then ‘Save’ the component.

**Step 12**: Next, add a ‘Tabs’ component from the ‘Advanced Fields’ into the builder

**Step 13**: Enter a unique name in the label field. 

![ap11](https://user-images.githubusercontent.com/91633223/204038808-e397aee9-906d-4ab3-b15d-3e54c7817dee.png)

**Step 14**: Add as many tabs as you want and details for each tab added

![ap12](https://user-images.githubusercontent.com/91633223/204038857-ed3daa9f-5f19-4a0a-af18-b1cdbd10f51c.png)

**Step 15**: Under the ‘Logic’ tab, click on the ‘Add Logic’ button and add any ‘Logic Name’

![ap13](https://user-images.githubusercontent.com/91633223/204038880-051feea0-a4d1-43de-8da6-0feaf1f98fd7.png)

**Step 16**: Under 'Logic Name', enter any name. Under ‘Trigger', select ‘Type’ dropdown menu, and select 'Event’

![ap14](https://user-images.githubusercontent.com/91633223/204038968-1bf0432b-6a7b-49a0-b644-e987b249f0de.png)

**Step 17**: enter “change“ in the “Event Name“ field and click on “Add Action“ button

![ap15](https://user-images.githubusercontent.com/91633223/204039004-1d79024b-fb63-47ca-9f69-25a53ec0d6cd.png)

**Step 18**: Click on the “Add Action“ Button

![ap16](https://user-images.githubusercontent.com/91633223/204039028-2e383337-3542-464e-81b5-67af2d0a2259.png)

**Step 19**: enter any name in the “Action Name“ field, select the “Type“ dropdown menu, and select the “Custom Action“

![ap17](https://user-images.githubusercontent.com/91633223/204039058-907b29f1-a6b3-439b-9a8d-18239f047ad2.png)

**Step 20**: paste the following code into the “Custom Action (Javascript)“ field

```
const { root} = instance;
root.setPristine(false);

const comp = root ? root.getComponent('data') : null;
const index = comp.currentTab;

const progressStepper = document.querySelectorAll(".healthStepper ol li");
leftOfIndex(index);

rightOfIndex(index, progressStepper.length)
progressStepper[index].classList.remove('errors');
progressStepper[index].classList.remove('disabled');
progressStepper[index].classList.add('active');
progressStepper[index].classList.remove('completed');


function leftOfIndex(index){
  for(let i=0; i<index; i++) {
    if(i===0) {
      if(!validateFacilityInformationTabComponents()) {
        progressStepper[i].classList.remove('completed');
        progressStepper[i].classList.remove('disabled');
        progressStepper[i].classList.remove('active');
        progressStepper[i].classList.add('errors');
      } else {
        progressStepper[i].classList.remove('errors');
        progressStepper[i].classList.remove('disabled');
        progressStepper[i].classList.remove('active');
        progressStepper[i].classList.add('completed');
      } 
    } else {
      progressStepper[i].classList.remove('errors');
      progressStepper[i].classList.remove('disabled');
      progressStepper[i].classList.remove('active');
      progressStepper[i].classList.add('completed');
    }
  }
}
function rightOfIndex(index, endIndex){
  for (let i=(endIndex-1); i>index; i--){
    progressStepper[i].classList.remove('completed');
    progressStepper[i].classList.remove('errors');
    progressStepper[i].classList.remove('active');
    progressStepper[i].classList.add('disabled');
  }
}

function validateFacilityInformationTabComponents() {
  const firstNameComp = root.getComponent('firstName');
  const lastNameComp = root.getComponent('lastName');
  let isAllFieldValue = true;
  isAllFieldValue = firstNameComp.checkValidity();
  isAllFieldValue = lastNameComp.checkValidity();
  return isAllFieldValue;
}
```

![ap18](https://user-images.githubusercontent.com/91633223/204039128-02c813c2-96ed-411c-9c5d-3afd465e0a6e.png)

> **Note**

> Change the ‘data' in the `root.getComponent('data')` to the name you entered in the “label” field of the Tab Component in Step 13

> ```
> const comp = root ? root.getComponent('data') : null;
> ```

> Change the 'healthStepper' in the `document.querySelectorAll(".healthStepper ol li")` to the name you enter in the “CSS Class“ field in Step 2

> ```
> const progressStepper = document.querySelectorAll(".healthStepper ol li");
> ```

> In this demo, we are only validating two input components in the first tab of the TabComponent which is why the line of code if the index is equal to zero `if(i===0){`

> The lines of codes below read the two input components in the first tab of the TabComponent and execute a validity check on them. See Step 2 for reference.

> ```
> function validateFacilityInformationTabComponents() {
>   const firstNameComp = root.getComponent('firstName');
>   const lastNameComp = root.getComponent('lastName');
>   let isAllFieldValue = true;
>   isAllFieldValue = firstNameComp.checkValidity();
>   isAllFieldValue = lastNameComp.checkValidity();
>   return isAllFieldValue;
> }
> ```

**Step 21**: Drag the button component to the builder, and change the label to “Next“. Under “Action“, click the dropdown and change select “Custom“

![ap19](https://user-images.githubusercontent.com/91633223/204052448-b8a9fe3d-e9c3-4efc-adef-35ad52b8b8e3.png)

**Step 22**: Copy the following code into “Button Custom Logic“ field

```
const tab = form.getComponent('data');
form.setPristine(false);
const index = tab.currentTab;
const progressStepper = document.querySelectorAll(".healthStepper ol li");
progressStepper[index].classList.remove('active');
progressStepper[index].classList.remove('disabled');

if(index===0) {
  if(!validateFacilityInformationTabComponents()) {
    progressStepper[index].classList.remove('completed');
    progressStepper[index].classList.add('errors');
  } else {
    progressStepper[index].classList.remove('errors');
    progressStepper[index].classList.add('completed');
  }
}

progressStepper[(index+1)].classList.add('active');
progressStepper[(index+1)].classList.remove('disabled');
progressStepper[(index+1)].classList.remove('errors');
progressStepper[(index+1)].classList.remove('completed');
tab.setTab((index+1)); 


function validateFacilityInformationTabComponents() {
  const firstNameComp = form.getComponent('firstName');
  const lastNameComp = form.getComponent('lastName');
  let isAllFieldValue = true;
  isAllFieldValue = firstNameComp.checkValidity();
  isAllFieldValue = lastNameComp.checkValidity();
  return isAllFieldValue;
}
```

![ap20](https://user-images.githubusercontent.com/91633223/204052521-50dcdf1b-ec0c-4f17-82f7-bd524ac7c5b1.png)


> **Note**

> Change the ‘data' in the `form.getComponent('data')` to the name you entered in the “label” field of the TabComponent in Step 13

> ```
> const tab = form.getComponent('data');
> ``` 

> Change the 'healthStepper' in the `document.querySelectorAll(".healthStepper ol li")` to the name you entered in the “CSS Class“ field in Step 2

> ```
> const progressStepper = document.querySelectorAll(".healthStepper ol li");
> ```

**Step 23**: Drag a button component to the builder, and change the label to “Previous“. Under “Action“, click the dropdown and change select “Custom“

![a21](https://user-images.githubusercontent.com/91633223/204052841-c20c6ce8-e8f1-4590-8954-509cb3887ff5.png)

**Step 24**: Copy the following code into “Button Custom Logic“ field

```
const tab = form.getComponent('data');
const progressStepper = document.querySelectorAll(".healthStepper ol li");
const index = tab.currentTab;
progressStepper[index].classList.remove('errors');
progressStepper[index].classList.remove('completed');
progressStepper[index].classList.remove('active');
progressStepper[index].classList.add('disabled');
progressStepper[(index-1)].classList.add('active');
progressStepper[(index-1)].classList.remove('errors');
progressStepper[(index-1)].classList.remove('completed');
tab.setTab((index-1));
```

![a22](https://user-images.githubusercontent.com/91633223/204052933-d84f6398-6a5f-437c-b17a-30401f9b34fc.png)

> **Note**

> Change the ‘data' in the `form.getComponent('data')` to the name you entered in the “label” field of the TabComponent in Step 13

> ```
> const tab = form.getComponent('data');
> ``` 

> Change the 'healthStepper' in the `document.querySelectorAll(".healthStepper ol li")` to the name you entered in the “CSS Class“ field in Step 2

> ```
> const progressStepper = document.querySelectorAll(".healthStepper ol li");
> ```

---

### Type B: Progress Bar with any Layout Component

This Progress Bar is designed to work with any layout component and with the Next and Previous Buttons. Its functionality has been developed almost similarly to Formio Wizard.  You switch between each layout using the Previous and Next buttons. It uses the `hide` attribute of each layout by setting it to true or false and using the triggerRedraw function to redraw the component to the screen.

![ap2](https://user-images.githubusercontent.com/91633223/204036962-61c5845e-366f-4caf-8a6b-99b8e9f12196.png)

**Step 1**: Start by dragging an ‘HTML Component’ into the form builder.

**Step 2**: change the ‘HTML tag’ field from `p` to `div`, and in the ‘Display’ tag enter a unique and custom class name in the ‘CSS Class. In this screenshot, we used `healthStepper`

![a23](https://user-images.githubusercontent.com/91633223/204053468-2ef2e7ed-1bb5-46a3-96fc-c49e5f89cf37.png)

**Step 3**: Copy the following code into the ‘Content’ section

```
<ol class="c-stepper">
    <li class="c-stepper__item active">
        <h3 class="c-stepper__title">Step 1</h3>
        <p class="c-stepper__desc">Facility Information</p>
    </li>
    <li class="c-stepper__item disabled">
        <h3 class="c-stepper__title">Step 2</h3>
        <p class="c-stepper__desc">Bed Occupancy</p>
    </li>
     <li class="c-stepper__item disabled">
        <h3 class="c-stepper__title">Step 3</h3>
        <p class="c-stepper__desc">Staffing Level</p>
    </li>
     <li class="c-stepper__item disabled">
        <h3 class="c-stepper__title">Step 4</h3>
        <p class="c-stepper__desc">Operating Level</p>
    </li>
    <!-- Other steps -->
</ol>
```

![a24](https://user-images.githubusercontent.com/91633223/204053515-fa3cd7cb-2b0d-4d61-8d53-198a883923f0.png)

**Step 4**: Click on the ‘Logic’ tab and click on the ‘Add Logic’ button

![a25](https://user-images.githubusercontent.com/91633223/204053555-c9b82ef6-ae57-4076-9e7e-a1dc688d5fdf.png)

**Step 5**: Enter any Logic Name

![a26](https://user-images.githubusercontent.com/91633223/204053608-d68a81b5-5b78-4191-9318-61b20e95bb2d.png)

**Step 6**: In ‘Trigger' section, click on ‘Type’ dropdown menu, and select 'Javascript’

![a27](https://user-images.githubusercontent.com/91633223/204053654-6976e3b1-cbc8-49a3-926e-570b6288e964.png)

**Step 7**: Click “Add Action“ button

![a28](https://user-images.githubusercontent.com/91633223/204053682-29b5643c-9fe3-45f6-be9a-ae8d4cecbb31.png)

**Step 8**: Enter any name in “Action Name“

![a29](https://user-images.githubusercontent.com/91633223/204053714-a573e58f-ddcf-4e15-a79d-db713a183649.png)

**Step 9**: In ‘Trigger' section, click on ‘Type’ dropdown menu, and select 'Javascript’

![a30](https://user-images.githubusercontent.com/91633223/204053739-74b81fcc-7bdf-4846-bed6-144fe7dff321.png)

**Step 10**: Copy the following code into the ‘Text Area’ section

```
let cssId = 'myCss'; 
const head  = document.getElementsByTagName('head')[0];
if (!document.getElementById(cssId))
{
    const link  = document.createElement('link');
    link.id   = cssId;
    link.rel  = 'stylesheet';
    link.type = 'text/css';
    link.href = 'https://bcgov-citz-ccft.github.io/forminators/customprogresssteppercss/chefsCustomCss.css';
    link.media = 'all';
    head.appendChild(link);
}
```

![a31](https://user-images.githubusercontent.com/91633223/204053781-b1e0dac4-c89a-4314-b310-c54835f10fad.png)

**Step 11**: Click on ‘Save Logic’ and then ‘Save’ the component.

**Step 12**: Next, add a ‘Tabs’ component from the ‘Advanced Fields’ into the builder

**Step 13**: Drag a button component to the builder, and change the label to “Previous“. Under “Action“, click the dropdown and change select “Custom“

![a32](https://user-images.githubusercontent.com/91633223/204053849-7fa2a0ef-d2f5-471d-a0c2-ee3e12732f5e.png)

**Step 14**: Copy the following code into “Button Custom Logic“ field

```
const componentList = ["facilityInformationPanel", "bedOccupancyPanel","staffingLevelPanel",
"operatingLevelPanel"];

const stepperssHiddenValue = form.getComponent('stepperssHiddenValue');
const index = parseInt(stepperssHiddenValue.getValue());

const progressStepper = document.querySelectorAll(".multiComponentStepper ol li");

progressStepper[index].classList.remove('completed');
progressStepper[index].classList.remove('errors');
if(index===0){
  const currentComponent =form.getComponent(componentList[index]);
  currentComponent.hidden=false;
  currentComponent.component.hidden=false;
  currentComponent.triggerRedraw();
  progressClassName(index);
  
}else if (index>0){
  const currentComponent =form.getComponent(componentList[index]);
  currentComponent.hidden=true;
  currentComponent.component.hidden=true;
  currentComponent.triggerRedraw();
  
  const previousComponent =form.getComponent(componentList[(index-1)]);
  previousComponent.hidden=false;
  previousComponent.component.hidden=false;
  previousComponent.triggerRedraw();
  progressStepper[index].classList.add('disabled');
  progressStepper[index].classList.remove('active');
  progressStepper[index].classList.remove('completed');
  progressStepper[index].classList.remove('erros');
  if((index-1)===0){
    progressClassName((index-1));
  } else{
     progressClassName(index);
  }
  
  
  stepperssHiddenValue.setValue((index-1));
}

function progressClassName(index){
  if(index===0) {
    progressStepper[index].classList.add('active');
    progressStepper[index].classList.remove('disabled');
    progressStepper[index].classList.remove('errors');
    progressStepper[index].classList.remove('completed');
  } else {
    progressStepper[(index-1)].classList.add('active');
    progressStepper[(index-1)].classList.remove('disabled');
    progressStepper[(index-1)].classList.remove('completed');
    progressStepper[(index-1)].classList.remove('erros');
}
}
```

![a33](https://user-images.githubusercontent.com/91633223/204053911-33ed0e35-cf6b-4f56-93a9-8ebe52534feb.png)

**Step 15**: Drag a button component to the builder, and change the label to “Next“. Under “Action“, click the dropdown and change select “Custom“

![a34](https://user-images.githubusercontent.com/91633223/204053949-37e7a5da-41e7-4716-b848-c0443b34aabd.png)

**Step 16**: Copy the following code into “Button Custom Logic“ field

```
const componentList = ["facilityInformationPanel", "bedOccupancyPanel","staffingLevelPanel",
"operatingLevelPanel"];
const stepperssHiddenValue = form.getComponent('stepperssHiddenValue');
const index = parseInt(stepperssHiddenValue.getValue());

const progressStepper = document.querySelectorAll(".multiComponentStepper ol li");


if(index<(parseInt(progressStepper.length)-1)){
  progressStepper[index].classList.remove('active');
  progressStepper[index].classList.remove('disabled');
  if(index===0) {
    if(!validateFacilityInformationTabComponents()) {
      progressStepper[index].classList.remove('completed');
      progressStepper[index].classList.add('errors');
    } else {
      progressStepper[index].classList.remove('errors');
      progressStepper[index].classList.add('completed');
    }
  } else {
    progressStepper[index].classList.remove('errors');
    progressStepper[index].classList.add('completed');
  }

  const currentComponent =form.getComponent(componentList[(index)]);
  currentComponent["hidden"] = true;
  currentComponent.component["hidden"]=true;
  
  const nextComponent =form.getComponent(componentList[(index+1)]);
  nextComponent.hidden=false;
  nextComponent.component.hidden=false;
  nextComponent.triggerRedraw();
  progressStepper[(index+1)].classList.add('active');
  progressStepper[(index+1)].classList.remove('disabled');
  stepperssHiddenValue.setValue((index+1))
} else if(index===(parseInt(progressStepper.length)-1)){
   progressStepper[index].classList.remove('active');
  progressStepper[index].classList.remove('errors');
  progressStepper[index].classList.remove('disabled');
  progressStepper[index].classList.add('completed');
}


function validateFacilityInformationTabComponents() {
  const firstNameComp = form.getComponent('firstName1');
  const lastNameComp = form.getComponent('lastName1');
  let isAllFieldValue = true;
  isAllFieldValue = firstNameComp.checkValidity();
  isAllFieldValue = lastNameComp.checkValidity();
  return isAllFieldValue;
}
```

![a35](https://user-images.githubusercontent.com/91633223/204054012-abb31309-ecf4-4ae5-bd3f-61e622b18f8c.png)

> **Note**

> Replace this array with an array of layout components you want to hide and show using the “Previous“ and “Next“ button.

> ```
> const componentList = ["facilityInformationPanel", "bedOccupancyPanel","staffingLevelPanel",
> "operatingLevelPanel"];
> ```

**[Back to top](#top)**