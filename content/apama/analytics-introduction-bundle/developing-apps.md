---
weight: 10
title: Developing applications
layout: redirect
---

Follow these steps to develop applications.

**Step 1 - Install Designer**

You can use Software AG Designer to develop your applications. [Download](http://www.apamacommunity.com/downloads/) and install Software AG Designer from the Apama Community. 


**Step 2 - Create a project**

Once installed, create an Apama project in Software AG Designer and enable it for Cumulocity connectivity.

For steps on how to create an Apama project, refer to [Creating Apama Projects](https://documentation.softwareag.com/onlinehelp/Rohan/Apama/v10-3/apama10-3/apama-webhelp/index.html#page/apama-webhelp%2FWIZARD_NEW_APAMA_PROJECT.html).


**Step 3 - Add Apama bundles to the project**

Add the following Apama bundles to the newly created Apama project. For instructions on how to add bundles to a project, refer to [Adding bundles to projects](https://documentation.softwareag.com/onlinehelp/Rohan/Apama/v10-3/apama10-3/apama-webhelp/index.html#page/apama-webhelp%2Fco-UsiApaStu_adding_bundles_to_projects.html).

* Cumulocity IoT > Event Definitions
<br>Provides event APIs required for sending and receiving data to/from Cumulocity IoT.
* Cumulocity IoT > Utilities for Cumulocity
<br>Provides helper utility functions for working with data received from Cumulocity IoT.
* Any Extractor
<br>Provides support for extracting values from the `any` type.
* Time Format
<br>Required to access all the methods of the Time Format plug-in. Useful for formatting and parsing Time.
* HTTP Client Generic Events
<br>Exposes pre-defined generic events used by the HTTP client connectivity plug-in.

**Step 4 - Create sample EPL application**

To create a new Apama EPL file, refer to [Creating new monitor files for EPL applications](https://documentation.softwareag.com/onlinehelp/Rohan/Apama/v10-3/apama10-3/apama-webhelp/index.html#page/apama-webhelp%2FWIZARD_NEW_MONITORSCRIPT.html).

Follow the steps as described in [Using EPL](/guides/concepts/realtime/#using-epl) to create a sample EPL application.

Before you deploy this EPL application to Cumulocity, you might want to test if this application works as expected. To do so, you need to add the following bundles to your Designer project.

* Add Automatic onApplicationInitialized
<br>This starts all connectivity plug-ins immediately on start up.
* Add the HTTP Client > JSON with generic request/response event definitions connectivity transport.
* Add the Cumulocity IoT > Cumulocity Client connecitivity transport.

For further information on [The Cumulocity IoT Transport Connectivity Plug-in](https://documentation.softwareag.com/onlinehelp/Rohan/Apama/v10-3/apama10-3/apama-webhelp/index.html#page/apama-webhelp%2Fco-ConApaAppToExtCom_the_cumulocity_connectivity_plug_in.html%23wwconnect_header), see the Apama documentation.

**Step 5 - Provide credentials**

You will need to provide your Cumulocity credentials in the project configuration. Configure the credentials in the *CumulocityIoT.properties* file under the Cumulocity client as follows:

```
CUMULOCITY_USERNAME=user@example.com 
CUMULOCITY_TENANT=exampleTenant 
CUMULOCITY_PASSWORD=examplePassword 
CUMULOCITY_APPKEY=apamaAppKey 
```

>**Info:** You need to [create an application](/guides/users-guide/administration#managing-applications) in Cumulocity to get a value for CUMULOCITY_APPKEY.

Note that the above description assumes that you are connecting to a tenant hosted on cumulocity.com (Example: mytenant.cumulocity.com). If you want to connect to a tenant hosted at a different location, you can append a custom URL configuration to `CumulocityIoT.yaml`.
      
```
url: ${CUMULOCITY_URL}
```

and append the URL details in *CumulocityIoT.properties*:

```
CUMULOCITY_URL=my_custom_tenant.mydomain.com
```

You can now proceed with testing your EPL in Software AG Designer.

Once the EPL application is ready, refer to [Deploying applications](/guides/apama/analytics-introduction/#deploying-apps) to upload the EPL application as a single .mon file.