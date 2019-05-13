---
weight: 50
title: Device availability
layout: redirect
---

#### c8y\_RequiredAvailability

Devices can be monitored for availability by adding a "c8y\_RequiredAvailability" fragment to the device:

    "c8y_RequiredAvailability": { "responseInterval": <<time in minutes>> }

Devices that have not sent any message in the response interval are considered unavailable. Response interval can have value between -32768 and 32767 and any values out of range will be shrink to range borders. Such devices are marked as unavailable (see below) and an unavailability alarm is raised. Devices with a response interval of zero minutes are considered to be under maintenance. No alarm is raised while a device is under maintenance. Devices that do not contain "c8y\_RequiredAvailability" are not monitored.

#### c8y\_Availability

The availability information computed by Cumulocity is stored in fragments: "c8y\_Availability" and "c8y\_Connection" of the device.

    "c8y_Availability": { "lastMessage": "2013-05-21...", "status": "AVAILABLE" },
    "c8y_Connection": {"status":"CONNECTED"}

|Name|Type|Description|
|:---|:---|:----------|
|lastMessage|Date|The time when the device sent the last message to Cumulocity.|
|status|String|The current status, one of AVAILABLE, MAINTENANCE, UNAVAILABLE.|

The following messages update the last message timestamp of a device:

-   Create an event, measurement or alarm (for given device as source)
-   Update the device itself (with given id) sending empty PUT request or request with id only, ie. {} or {"id":...}

A monitored device has one of following statuses:

|Name|Description|
|:---|:----------|
|CONNECTED|A device push connection is established.|
|AVAILABLE|The device is not connected through device push, but a message was sent within the required response interval.|
|MAINTENANCE|"responseInterval" is set to 0; the device is under maintenance.|
|UNAVAILABLE|"responseInterval" is larger than 0 and the device is neither AVAILABLE nor CONNECTED.|

#### c8y\_UnavailabilityAlarm

The alarm sent when a device becomes unavailable is of type "c8y\_UnavailabilityAlarm":

    {
        ...
        "type" : "c8y_UnavailabilityAlarm",
        "text" : "No communication with device since <<last activity time>>",
        "status" : "active",
        "severity" : "major",
        "source" : <<device id>>
        ...
    }

Updates to the availability status may occur with a delay.

![Availability](/guides/images/reference-guide/availability.png)

To flag a device as available without updating any data, a "ping" can be sent. The "ping" can be carried out by simply sending an empty update message to the device (i.e., a PUT request to the managed object with empty content).

#### c8y\_ActiveAlarmsStatus

The number of currently active and acknowledged alarms is stored in a fragment "c8y\_ActiveAlarmsStatus".

    "c8y_ActiveAlarmsStatus": {
        "minor": 1,
        "major": 3
    }

![Alarm status](/guides/images/reference-guide/alarmstatus.png)