---
weight: 20
title: Configuring columns
layout: redirect
---

The columns shown in the device list may be configured to your needs.

### To show/hide standard columns

1. In the table header, click **Configure columns**.
2. In the resulting dropdown, select/clear the checkboxes for all columns as required.

The device list will reflect your changes and only show the selected columns.

### To add custom columns

Moreover, you can add custom columns to show additional device properties.

1. In the **Configure columns** dropdown, click **Add custom column**.<br>
   ![Configure columns](/images/users-guide/DeviceManagement/devmgmt-device-list-custom-column.png)<br>
2. In the **Header** field, enter a header for the new custom column.
3. In the **Fragment path** field, enter the property of the device to be shown. Nested properties will be accepted. However, for nested properties its only possible to select {{< product-c8y-iot >}} standard fragments like `c8y_Mobile.mcc`.
4. Switch the **Add another column after saving this one** toggle to active to create another custom column right after saving the current one without leaving the dialog.
5. Click **Save**.

The new column will be added and displayed in the device list.

{{< c8y-admon-info >}}
While standard columns can only be shown/hidden as required, custom columns may be deleted permanently.
{{< /c8y-admon-info >}}

### To delete a device from the list

1. Hover over the row of the device you want to delete.
2. Click the delete icon at the right of the row.
3. Confirm the device removal. Optionally, select whether to delete child devices of the device or to delete the associated device owner. Note that it is not possible to select both options.

The device will be permanently deleted from the platform.

{{< c8y-admon-important >}}
Deleting a device means to remove the device from the {{< product-c8y-iot >}} database including all its generated data. Alternatively, you can arrange all retired devices in one group, see [Grouping devices](#grouping-devices)). This ensures that all reports remain correct. To prevent alarms from being raised for the retired devices, disable [connection monitoring](#connection-monitoring). Deleting a device does not delete the data of its child devices.
{{< /c8y-admon-important >}}

<a name="filtering-devices"></a>

### To filter devices

The device list offers a filtering functionality to filter devices in the list for specific criteria.

Filtering is available on every column. Click the filter icon next to the name of the column you want to set a filter for.

Specify your filter options in the dropdown list.

Most columns represent text fields. You can filter these columns by simply entering an arbitrary text into the textbox as in the search field. Click **+ Add next** to add another textbox if you want to filter for more than one term.

Apart from filtering for text there are several other options:

- In case of date fields (for example **Registration date**), you specify a date range to filter for.
- In the **Status** column you can filter for various criteria representing the send, push or maintenance status of the device.
- In the **Alarm** column the filtering options you may select correspond to the alarm types (critical, major, minor, warning, no alarms).
- For custom columns, select **Only rows where value is defined** to filter based on whether the fragment exists, or specify one or more filter terms the entry must match.

Finally, click **Apply** to carry out the filtering.

The devices list will now only display devices matching the filtering options.

Sorting is available on every column. Click the sort icon in the respective column header once to sort the entries in ascending order and twice to sort the entries in descending order. Click the sort icon once more to remove sorting for this column.

Click **Clear filters** in the table header if you want to clear all filters and view all devices.

{{< c8y-admon-info >}}
If you select to sort a text field, for example, device name, in ascending or descending order, keep in mind that the resulting alphabetical sorting is based on ASCII/UTF: A < B < ... < Z < ... < a < b ... < z. Names starting with lower case letters will be sorted below all names with uppercase letters or vice versa.
{{< /c8y-admon-info >}}