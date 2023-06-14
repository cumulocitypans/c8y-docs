---
weight: 10
title: Registering devices
layout: bundle
section:
  - device_management
helpcontent:
  - label: connecting-devices
    title: Connecting devices
    content: "To connect devices to Cumulocity IoT they must be registered. To register one or more devices, click **Register device** and follow the instructions in the wizard or in the *User guide*.


    All devices which are currently in the registration process are displayed with one of the following statuses:


    **Waiting for connection** - The device has been registered but no device with the specified ID has tried to connect

    **Pending acceptance** - There is communication from a device with the specified ID, but the user doing the registration must still explicitly accept it so that the credentials are sent to the device

    **Accepted** - The user has allowed the credentials to be send to the device

    **Blocked** - The device registration has been blocked due to the exceeded limit of failed attempts.


    To register devices, you can select one of the following options:

    Single device registration - To manually connect one or more devices.

    Bulk device registration - To register larger amounts of devices in one step.


    Depending on the microservices subscribed to your tenant, you might see other device registration options for specific protocol types.


    To register a device, click **Register device** at the right of the top bar, select an option from the dropdown list and follow the instructions in the device registration wizard."
---

In the **Device registration** page all devices are displayed which are currently in the registration process.

<img src="/images/users-guide/DeviceManagement/devmgmt-device-registration.png" alt="Device registration page">

The following information is shown for each device:

* Device name specified in the registration process
* Status of the device (see below)
* Creation date
* Tenant from which the device was registered

The devices may have one of the following status:

* **Waiting for connection** - The device has been registered but no device with the specified ID has tried to connect.
* **Pending acceptance** - There is communication from a device with the specified ID, but the user doing the registration must still explicitly accept it so that the credentials are sent to the device.
* **Accepted** - The user has allowed the credentials to be send to the device.
* **Blocked** - The device registration has been blocked due to the exceeded limit of failed attempts.

{{< c8y-admon-info >}}
If a device registration is **blocked**, you will need to delete it first and then create it again.
{{< /c8y-admon-info >}}

Devices can be connected to your {{< product-c8y-iot >}} account in different ways.

To register devices, you can select one of the following options:

* **[Single device registration](#device-registration-manually)** - to manually connect one device or several devices one by one.
* **[Bulk device registration](#bulk-registration)** - to register larger amounts of devices in one step.

Microservice developers can also use the [Extensible device registration](/concepts/applications/#extensible-device-registration) and implement a custom registration form that blends seamlessly into the UI.

{{< c8y-admon-info >}}
The following descriptions apply to the general device registration processes. If you subscribe to specific protocol integrations, you will see additional protocol-specific options (for example, for LWM2M or OPC UA). A full list of supported protocols can be found in the [Protocol integration guide](/protocol-integration/overview/). It also contains descriptions for the protocol specific registration processes.
{{< /c8y-admon-info >}}