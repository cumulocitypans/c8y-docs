---
weight: 80
title: SmartREST templates
layout: redirect
---

### Introduction

SmartREST templates are a collection of request and response templates used to convert CSV data and Cumulocity Rest API calls. For example, you can use SmartREST templates to easily add devices to the platform instead of manually writing the requests each time.

To ease the device integration, Cumulocity supports static templates that can be used without the need for creating your own templates. These templates focus only on the most commonly used messages for device management. For further information on static templates, refer to the [Device SDK guide](/guides/device-sdk/mqtt#static-templates).

Open the **SmartREST template** page from the **Device Types** menu in the navigator. 

![template view](/guides/images/users-guide/DeviceManagement/devmgmt-devicetypes-smartrest.png)

For each template, the following information is provided:

* Template name
* Template ID
* Number of send messages
* Number of responses

There are two ways to add a SmartRest template:

- Import an already existing template
- Create a new template

### How to import an existing SmartREST template

1. Click **Import** at the right of the top menu bar.
2. In the resulting dialog box, choose a file to upload by browsing for it.
3. Enter a template name and a unique template ID (both mandatory fields). 
4. Click **Import** to import the template.

![Import template](/guides/images/users-guide/DeviceManagement/devmgmt-devicetypes-smartrest-import.png)

### How to create a new SmartREST template

1. Click **New** at the right of the top menu bar.
2. In the resulting dialog box, enter a template name and a unique template ID (both mandatory fields). 
4. Click **Continue** to proceed adding messages or responses.

![Add new template](/guides/images/users-guide/DeviceManagement/devmgmt-devicetypes-smartrest-new.png)

#### How to add a message

The message template contains all necessary information to convert the SmartRest request into a corresponding Rest API call which is then sent to the platform.

1. To add a new message, navigate to the **Messages** tab in your desired SmartREST template and click **Add message**. 

1. Complete the following fields:

	|Field|Description|
|:---|:---|
|Message ID|Unique integer that will be used as a message identifier. It must be unique among all message and response templates.
|Name|Name for the message. Mandatory.
|Target REST API|REST API for the target. Dropdown list. May be one of Measurement, Inventory, Alarm, Event, Operation.
|Method|Request method. May be one of POST, PUT, GET, depending on the selected Target REST API.
|Include Responses|Select this checkbox if you want to process the results of the request with response templates.
|REST API built-in fields|These fields are optional and vary depending on the target REST API selected. In case no value is provided, a device will be able to set it when sending an actual message.
|REST API custom fields|Additional fields can be added by clicking **Add field**. Enter the API key and select the desired data type.

	![Add message](/guides/images/users-guide/DeviceManagement/devmgmt-devicetypes-smartrest-addmessage.png)

	Under **Preview** you can see a preview of your request message.

3. Click **Save**.

The message will be added to the SmartREST template.

#### How to remove a message

To remove a message, open it and click **Remove** at the bottom.

The message will be removed from the SmartREST template.

#### How to add a response

A response template contains the necessary information to extract data values from a platform REST API call response, which is then sent back to the client in a CSV data format.

1. To add a new response, navigate to the **Response** tab in your desired SmartREST template and click **Add response**. 
 
2. Complete the following fields:

	|Field|Description|
|:---|:---|
|Response ID|Unique integer that will be used as a response identifier. 
|Name|Name for the response. Mandatory.
|Base Pattern|Base pattern for the response.
|Condition|Condition value of the response.
|Pattern|At least one pattern is required. Click **Add pattern** and enter a pattern value.

	![Add template response](/guides/images/users-guide/DeviceManagement/devmgmt-devicetypes-smartrest-addresponse.png)

3. Click **Save**.

The response will be added to the SmartREST template.
 
#### How to remove a response
 
To remove a response, open it and click **Remove** at the bottom.

The response will be removed from the SmartREST template.

### How to edit a SmartREST template

To edit a SmartREST template, either click the desired template or click the menu icon and then click **Edit**.

After editing the template, click **Save**.

Your settings will be saved to the template.

### How to delete a SmartREST template

To delete a SmartREST template, click the menu icon and then click **Remove**.

The template will be deleted.


### How to export a SmartREST template

To export a SmartREST template, click the menu icon and then click **Export**. The template will automatically be downloaded.

To export a SmartREST template as CSV file follow these steps:

1. Open the template you want to export and select the **CSV preview** tab. 
2. In the resulting dialog box, specify the preferred options for the field separator, decimal separator and character set.
3. In the **CSV preview** tab, which provides additional information on messages and responses, click **Copy to clipboard**. 

![CSV preview tab](/guides/images/users-guide/DeviceManagement/devmgmt-devicetypes-smartrest-csv.png)

The SmartREST template will be exported as CSV file.