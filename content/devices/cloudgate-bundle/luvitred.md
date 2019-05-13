---
title: LuvitRED
layout: redirect
weight: 30
---


### Overview

LuvitRED is a browser-based application which allows you to write applications without any programming language. With the help of an editor, you can easily create workflows by utilizing a set of nodes which perform certain tasks respectively.

To view the LuvitRED editor, go to the "Plugin" tab in the CloudGate web interface and select "LuvitRED". Click on "Advanced Editor" and the editor will appear.

![LuvitRED user interface](/guides/images/devices/cloudgate/luvitred.png)

On the left side of the user interface, you can see a list of nodes which are ready to use. To see which purpose the node serves, click on a node and see the description on the right side. Drag a node into the middle area to add it to your current workflow. Before creating a workflow, you have make sure that your device is connected to the CloudGate, otherwise the workflow will not work. In a similar manner, you have to include at least one "c8y" node in your workflow in order to connect to Cumulocity. Type "c8y" into the search bar to view all the nodes which are related to Cumulocity. Adding one of the following "c8y" nodes brings the following features:

* [c8y measurement](#measurement): Sends a measurement to the Cumulocity server
* [c8y alarm](#alarm): Sends an alarm to the Cumulocity server
* [c8y event](#event): Sends an event to the Cumulocity server
* [c8y command](#command): Receives a command sent by the Cumulocity server
* [c8y config](#config): Receives a configuration update sent by the Cumulocity server
* [c8y response](#response): Sends a response to commands to the Cumulocity server

> Note that nodes in LuvitRED which require the user to write code (e.g. the "function" node) use Lua as a programming language.

### Using LuvitRED with Cumulocity: An Example

#### Basic workflow

In general, a node can have an input and/or output depending on the functionality. Two nodes can be connected by linking the output of one node with the input of another node. A dialog for configuring the node will appear when double-clicking it. After configuring the nodes, the workflow is ready to be deployed. Click on the "Deploy" button in the top right corner to start the workflow. If there are changes in the configuration which have not been deployed yet, a blue dot will appear above the node. If there is at least one parameter in the configuration which has to be specified but is not, a red triangle will appear above the node.

In the following example, the "inject" and "debug" node will be used. Drag both nodes into the middle area and connect them by clicking on the output of the "inject" node", holding the mouse and releasing it above the input of the "debug" node.

![LuvitRED user interface](/guides/images/devices/cloudgate/basicflow.png)

The "debug" node is used for displaying the input it gets on the console (the "debug" tab on the right side of the editor) while the "inject" node is used for sending a customizable value as output. In this case, the "debug" node will just display the value we will configure in the "inject" node. To configure the "inject" node, double-click it.

![LuvitRED user interface](/guides/images/devices/cloudgate/injectdialog.png)

- Payload: Defines what will be sent as output.
  - Select "string" as the type of the payload in the drop-down menu.
  - Enter "test" as payload.
- Repeat: Specifies when the payload will be sent.
  - Check "Fire once at start".
- Name: Defines the name of the node which will be displayed in the user interface.
  - Enter an arbitrary name.

After deploying the changes, you should be able to see the specified value in the "debug" tab.

![LuvitRED user interface](/guides/images/devices/cloudgate/debug.png)

#### Basic workflow with Cumulocity

In the following example, we will simulate a periodic temperature measurement and send it to Cumulocity. To do so, replace the "debug" node with a "c8y measurement" node.

![LuvitRED user interface](/guides/images/devices/cloudgate/basiccumulocityflow.png)

To send random numeric values perdiodically, change the configuration of the "inject" node. First, select "random integer" as payload type and choose a range of possible values. Second, select "interval" in the "repeat" field and specify an interval.

![LuvitRED user interface](/guides/images/devices/cloudgate/basiccumulocityflowinjectdialog.png)

Next, the "c8y measurement" node needs to be configured.

![LuvitRED user interface](/guides/images/devices/cloudgate/basiccumulocityflowmeasurement.png)

- Type: Type of the measurement.
  - Enter "c8y_Temperature" as type.
  - Select "Temperature" in the drop-down menu. A predefined fragment will be created depending on the selection.
  - Click on the "add" button.

- Platform: Defines the platform the node will use.
  - Click on the "pencil" icon. Another dialog which represents the "c8y platform" node will appear.

![LuvitRED user interface](/guides/images/devices/cloudgate/basiccumulocityflowplatform.png)

- Provision: Defines if the credentials will be set manually or autoprovisioned.
  - Select "Manually" in the drop-down menu.
- Tenant: The tenant you want to register your device at.
  - Enter the tenant name.
- Username: The username which will be used for authentication.
  - Enter your username.
- Password: The password which will be used for authentication.
  - Enter your password.
- Name: Defines the name of the node which will be displayed in the user interface.
  - Enter an arbitrary name.

For more information on the "[c8y measurement](#measurement)" and "[platform](#platform)" node, see below.

After configurating the "c8y measurement", the workflow is ready to be deployed. You should be able to see the measurements sent by the device in the "Measurement" tab of your device in the "Device Management" application of Cumulocity. You can also see the amount of measurements which were sent in the status under the node.

![LuvitRED user interface](/guides/images/devices/cloudgate/temperaturemeasurements.png)