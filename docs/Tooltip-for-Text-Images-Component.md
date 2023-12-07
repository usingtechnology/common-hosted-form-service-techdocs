[Home](.) > [CHEFS Components](CHEFS-Components) > [Custom Components](Custom-components) > **Tooltip**
***

##  Examples
> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=3897ab9e-b9f2-43d5-ab95-3d1344c1516e)

> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<br>
> [example_tooltip_for_text_images_component_schema.json](examples/example_tooltip_for_text_images_component_schema.json)
***

## Tooltip (Tutorial)

By default, most of the form.io components such as the ‘Number’ and ‘Text’ fields have a tooltip capability which displays information when a user hovers their cursor over it. 

![tooltip1](https://user-images.githubusercontent.com/91633223/203413787-0e8c468d-5c31-411d-abe9-96ed1631aa65.png)

To add a tooltip to a component, simply click on Settings (gear icon), and add the tooltip text in the ‘Tooltip’ field under the ‘Display’ tab.

![tooltip2](https://user-images.githubusercontent.com/91633223/203413846-f29907d1-a74e-4e69-bf03-f53dda32f9f1.png)


However, some fields such as the ‘Text/Images Component' do not have this capability. This limits CHEFS’ ability to display tooltips next to standalone text such as a heading. This limitation can be overcome by using an ‘HTML Component' and adding form.io’s own tooltip HTML class.

![tooltip3](https://user-images.githubusercontent.com/91633223/203413935-4edb4796-cabe-4038-becf-bad24f2d2cf3.png)


To achieve this, add an ‘HTML Element Component’ to your form and click on the Settings (gear) icon. Enter the following HTML code into the ‘Content’ field, replacing ‘HTML Tooltip’ with your custom text. 

![tooltip4](https://user-images.githubusercontent.com/91633223/203413947-8706433b-1639-4f56-8de2-7cdde7cc90ce.png)

```
<h1 class="col-form-label" ref="label" style="font-size: 1.5em">
  HTML Tooltip
  <i data-tooltip="This is a long tooltip containing important information." 
    class="fa fa-question-circle text-muted" tabindex="0" ref="tooltip" 
    aria-expanded="false" style="font-size: 20px"></i>
</h1>
```

**[Back to top](#top)**