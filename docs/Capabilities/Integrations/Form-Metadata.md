[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Custom Form Metadata** 
***  
# Custom Form Metadata

CHEFS has added Custom Form Metadata support for each form to support integration with external systems better. Custom Form Metadata allows the owner/designer to add attributes such as external identifiers, categories, classifications or labels to aid in filtering and mapping between CHEFS and external systems.

The Custom Form Metadata will be added to [External API](./Calling-External-API.md) calls as a base64 encoded header: `X-FORMS-METADATA`. [Event Stream Service](./Event-Stream-Service.md) notifications will include the Custom Form Metadata in the `metadata` payload as `formMetadata`.

**IMPORTANT**  do not include sensitive or private information in the Custom Form Metadata.

## Adding Form Metadata

When Managing a Form, under Form Settings, there is a Form Metadata section. This section requires a JSON object. Note that you must enter the attributes and values using double-quotes " so the value can be parsed into a valid JSON object.

## Decoding Header

When the Custom Form Metadata is sent to External APIs, the JSON object is turned to a `utf-8` string then `base64` encoded. You will have to decode it. The following is an example for decoding using `JavaScript`.

Note: the header will be added if attributes are in the Custom Form Metadata. If the Custom Form Metadata is an empty object, then we will not add the header.

```
  let bufferObj = Buffer.from(headers["X-FORM-DATA"], "base64");
  let decodedString = bufferObj.toString("utf8");
  let o = JSON.parse(decodedString); // Custom Form Metadata as JSON Object.
```

## Event Stream 
When the Custom Form Metadata is sent to Event Stream messages, the JSON object is added to the `meta` section.

Note: the `formMetadata` section will be added if attributes are in the Custom Form Metadata. If the Custom Form Metadata is an empty object, then we will not add `formMetadata`.

```json
{
  meta: {
    source: 'chefs',
    domain: 'forms',
    class: 'submission'
    type: 'modified',
    formId: <uuid>,
    formVersionId: <uuid>,
    submissionId: <uuid>,
    draft: false,
    formMetadata: {
      externalId: 'AB-0123456789',
    }
  },
  payload: {
    data: <encrypted>
  }

```

## API - Get Form and Get Submission.
Form Metadata is returned as part of the form object for Get Form and Get Submission API calls. This will be returned regardless of any attributes in the `metadata` object.

### Get Form
```
{
    "id": "b0c75fb6-de06-4e2d-a9e6-16b117971d51",
    "name": "Custom Form Metadata Example",
    "description": "This form is used as an example for Custom Form Metadata",
    "active": true,
    "labels": [],
    ...
    "formMetadata": {
        "id": "eb2554d8-d2d9-4b3d-b0a5-69bde4797dfd",
        "formId": "b0c75fb6-de06-4e2d-a9e6-16b117971d51",
        "headerName": "X-FORM-METADATA",
        "attributeName": "formMetadata",
        "metadata": {
            "externalId": "AB-0123456789"
        },
        "createdBy": "JASHERMA@idir",
        "createdAt": "2024-10-07T22:27:40.081Z",
        "updatedBy": null,
        "updatedAt": "2024-10-07T22:27:39.932Z"
    },
    "identityProviders": [...],
    "versions": [...],
    "snake": "custom_form_metadata_example"
}
```

### Get Submission

Note that this is the same as above. The `form.formMetadata` object contains the Custom Form Metadata.

```
{
    "submission": {
        "id": "07acbae6-e1c0-4ac4-b560-25456413c4bf",
        "formVersionId": "a5158028-9126-46b9-99d6-c899d585d045",
        "confirmationId": "07ACBAE6",
        "draft": false,
        "deleted": false,
        "submission": {
            "data": {
                "submit": true,
                "lateEntry": false,
                "simpleemail": "jason@idir.com"
            },
            ...
        },
        ...
    },
    "version": {
        "id": "a5158028-9126-46b9-99d6-c899d585d045",
        "formId": "b0c75fb6-de06-4e2d-a9e6-16b117971d51",
        "version": 1,
        "schema": {
            "type": "form",
            "display": "form",
            "components": [...]
        },
        "createdBy": "JASHERMA@idir",
        "createdAt": "2024-10-07T22:27:52.834Z",
        "updatedBy": null,
        "updatedAt": "2024-10-07T22:27:52.800Z",
        "published": true
    },
    "form": {
        "id": "b0c75fb6-de06-4e2d-a9e6-16b117971d51",
        "name": "Custom Form Metadata Example",
        "description": "This form is used as an example for Custom Form Metadata",
        ...
        "formMetadata": {
            "id": "eb2554d8-d2d9-4b3d-b0a5-69bde4797dfd",
            "formId": "b0c75fb6-de06-4e2d-a9e6-16b117971d51",
            "headerName": "X-FORM-METADATA",
            "attributeName": "formMetadata",
            "metadata": {
                "externalId": "AB-0123456789"
            },
            "createdBy": "JASHERMA@idir",
            "createdAt": "2024-10-07T22:27:40.081Z",
            "updatedBy": null,
            "updatedAt": "2024-10-07T22:27:39.932Z"
        },
        "identityProviders": [...],
        "snake": "custom_form_metadata_example"
    }
}
```

