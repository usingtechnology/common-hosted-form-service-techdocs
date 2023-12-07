> ### How do I decide whether to use the Day component or the Date/Time component?

## Day field  
This field is free of any time data, so if you are recording the Birth Date, this field is a good option. But remember with Birth Date the date should be taken in context of a location. The UTC Date/Time of your birth might be different than what you typically consider to be your birth day.  

## Date/Time field  
**Format**: ```yyyy-MM-dd hh:mm a```  
This component is good to use to track sequence of events where the time of the day that it happens is important. If you only want to track the date, keep in mind that the location (timezone) the user is at when filling out this form will may result in values that are not accurate if for example they were entering birth date, and were born in Alberta, but were then filling out the form in a timezone that crossed the timezone where the date changed. e.g. 12:01AM Mountain time on 2000-01-01 was 11:01AM 1999-12-31 Pacific Time.  

> Example form: [Day versus Date/Time](https://submit.digital.gov.bc.ca/app/form/submit?f=2feb8f40-9c99-4f0c-a416-53d819bc730e)   

