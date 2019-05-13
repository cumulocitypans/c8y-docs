---
weight: 40
title: Upgrading the system
layout: redirect
---

Follow the steps below to upgrade the system. 

1. Power off the VM. To do so, access the VM and run the following command in the terminal:<br>
```shell
`sudo shutdown`
```

2. Navigate to the VM directory. For VirtualBox it is *[USER-DIRECTORY]\VirtualBox VMs*. Move the entire VM folder (e.g. EDGE-server) to a safe location.
<img src="/guides/images/edge/edge-update-move.jpg" name="Move folder" style="width:75%;"/> 

3. In the VirtualBox Manager, right-click on the VM and then click **Remove**. In the upcoming window, select **Remove Only** so that the VM will not be deleted. 
<img src="/guides/images/edge/edge-update-remove.jpg" name="Remove VM" style="width:75%;"/> 

4. Import the new version of EDGE server. To do so, click **File** and then **Import Appliance** in the VirtualBox Manager. Select the new OVA file (upgraded one supplied by Cumulocity) and click **Open** to import it. 
<img src="/guides/images/edge/edge-update-import.jpg" name="Import VM" style="width:75%;"/> 
<br>The new Edge version should now be visible in the VirtualBox Manager in powered-off state. 

5. Right-click on the VM and select **Settings**. In the upcoming window, select **Storage**. Two disks should be visible called "disk001.vmdk" and "disk002.vmdk". 

6. Right-click on the second disk i.e. disk002.vmdk, and select **Remove attachment**. 
<img src="/guides/images/edge/edge-update-storage.jpg" name="Storage" style="width:75%;"/> 

7. Right-click on the second controller i.e. SATA controller and select **Add Hard Disk**. In the upcoming window, select **Choose existing disk**. 
<img src="/guides/images/edge/edge-update-harddisk.jpg" name="Add hard disk" style="width:75%;"/> 

8. In the explorer, navigate to the previously backed-up EDGE folder as per step 2. Select the secondary disk, i.e. disk002.vmdk, and click **OK**.<br>
<img src="/guides/images/edge/edge-update-choose-disk.JPG" name="Choose disk" style="width:75%;"/> 

9. Power on the VM by clicking the **Start** button. 

10. Invoke the post-installer by running the script *post-installation.sh* located in the directory */opt/c8y/utilities*.<br>
```shell
sudo ./post_installation.sh
```

11. Choose the post-upgrade task (option 4). Provide inputs if prompted and complete the post-upgrade task. For details see [Configuration](/guides/edge/installation/configuration).

10. Verify, whether DB and property files are intact and unchanged.