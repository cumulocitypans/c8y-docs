---
title: Anomaly detection using a demo device
layout: redirect
weight: 50
---

A fully functional demo can be prepared with the help of a demo device. For this, use the artefacts provided as part of the *AnomalyDetectionDemo.zip* file.

#### Register a demo device in Cumulocity

Instead of registering a real phone for anomaly detection use case, a demo device can be registered. This device can be used as a replica of an actual mobile phone.

We have added a script *DemoDeviceCreator.sh* which registers a demo device in Cumulocity. Run the script using the following command:

	sh DemoDeviceCreator.sh 

Use this script to add a device named "DemoDevice" to Cumulocity.

	DemoDeviceCreator.sh
	c_url=$(awk -F "=" '/c_url/ {print $2}' ./CONFIG.INI)
	c_user=$(awk -F "=" '/c_user/ {print $2}' ./CONFIG.INI)
	c_pass=$(awk -F "=" '/c_pass/ {print $2}' ./CONFIG.INI)
	echo
	echo "#####################################"
	echo "#    Registering new demo device    #"
	echo "#####################################"
	curl --user $c_user:$c_pass -X POST $c_url"/inventory/managedObjects" -H "accept: application/json" -H "Content-Type: application/json" \
	--data '{"name": "DemoDevice", "c8y_IsDevice": {}, "myDemoDevice":{}, "c8y_SupportedMeasurements": ["c8y_SignalStrengthWifi","c8y_Acceleration", "c8y_Barometer", "c8y_Gyroscope", "c8y_Luxometer", "c8y_Compass"]}'
	echo
	echo
	echo "#########################################################"
	echo "#  Registered a demo device with the name 'DemoDevice'  #"
	echo "#########################################################"

Once registered, try to get the device ID by looking up your device on the **All Devices** page of your tenant's Device Management application. Now, update the `c_device_source` of the *CONFIG.INI* file with the device ID of this demo device.

#### Upload the model and Apama monitor to Cumulocity

1. Upload the attached model *iforest_demo.pmml* to Cumulocity. To upload the model to Cumulocity, follow the steps described in [Predictive Analytics application > Managing models](/guides/predictive-analytics/web-app/#managing-models).
2. Download the attached *DetectAnomalies.mon* file, open it in a text editor and replace the `deviceId` variable with the ID of your registered device, same as c_device_source in the CONFIG.INI file mentioned above.
3. Save your changes and upload this monitor file to your tenant. See [Deploying Apama applications as a single *.mon file with the Apama-epl application] (/guides/apama/analytics-introduction/#single-mon-file) in the Analytics guide for details on uploading Apama monitor files.


#### Trigger an Anomaly Alert

A script *AnomalySimulatorForDemoDevice.sh* has been attached which simulates sending of alternate anomalous and non-anomalous readings to Cumulocity from our demo device. This script can be used to depict the generation of anomalies.

All you need to do is run it as `sh AnomalySimulatorForDemoDevice.sh`.

	AnomalySimulatorForDemoDevice.sh
	c_url=$(awk -F "=" '/c_url/ {print $2}' ./CONFIG.INI)
	c_user=$(awk -F "=" '/c_user/ {print $2}' ./CONFIG.INI)
	c_pass=$(awk -F "=" '/c_pass/ {print $2}' ./CONFIG.INI)
	c_device_source=$(awk -F "=" '/c_device_source/ {print $2}' ./CONFIG.INI)
	end=$((SECONDS+30))
	COUNTER=0
	DIV=2
	while [ $SECONDS -lt $end ]; do
	    result=`expr $COUNTER % $DIV`
	    if [ $result == 0 ]
	    then
	        echo
	        echo "##########################################"
	        echo "#  Simulating Non-Anamolous Measurement  #"
	        echo "##########################################"
	        echo
	        curl --user $c_user:$c_pass -X POST $c_url"/measurement/measurements" -H "accept: application/vnd.com.nsn.cumulocity.measurementCollection+json" -H "Content-Type: application/json" \
	        --data '{"measurements":[{"time":"2019-03-29T17:26:14.000+02:00","source":{"id":"'$c_device_source'"},"type":"c8ydemoAndroid","c8y_SignalStrengthWifi":{"rssi":{"unit":"dBm","value":-46}},"c8y_Acceleration":{"accelerationY":{"unit":"G","value": 9.347839355},"accelerationX":{"unit":"G","value":7.12612915},"accelerationZ":{"unit":"G","value":7.345794678}},"c8y_Barometer":{"Air pressure":{"unit":"mBar","value":10.00928101}},"c8y_Gyroscope":{"gyroX":{"unit":"°/s","value":-1.415344238},"gyroY":{"unit":"°/s","value": 5.859771729},"gyroZ":{"unit":"°/s","value":0.934921265}},"c8y_Luxometer":{"lux":{"unit":"lux","value":240.7909851}},"c8y_Compass":{"compassX":{"unit":"uT","value":-72.02148438},"compassY":{"unit":"uT","value":-24.59411621},"compassZ":{"unit":"uT","value":-15.24505615}}}]}'
	        sleep 2
	    fi
	    if [ $result -eq 1 ]
	    then
	        echo
	        echo "##########################################"
	        echo "#    Simulating Anamolous Measurement    #"
	        echo "##########################################"
	        echo
	        curl --user $c_user:$c_pass -X POST $c_url"/measurement/measurements" -H "accept: application/vnd.com.nsn.cumulocity.measurementCollection+json" -H "Content-Type: application/json" \
	        --data '{"measurements":[{"time":"2019-03-29T17:26:14.000+02:00","source":{"id":"'$c_device_source'"},"type":"c8ydemoAndroid","c8y_SignalStrengthWifi":{"rssi":{"unit":"dBm","value":-46}},"c8y_Acceleration":{"accelerationY":{"unit":"G","value":9.347839355},"accelerationX":{"unit":"G","value":7.12612915},"accelerationZ":{"unit":"G","value":7.345794678}},"c8y_Barometer":{"Air pressure":{"unit": "mBar","value":10.00928101}},"c8y_Gyroscope":{"gyroX":{"unit":"°/s","value":5.288024902},"gyroY":{"unit":"°/s","value":-9.42755127},"gyroZ":{"unit":"°/s","value":-4.908660889}},"c8y_Luxometer":{"lux":{"unit":"lux","value":240.7909851}},"c8y_Compass":{"compassX":{"unit":"uT","value":-72.02148438},"compassY":{"unit":"uT","value":-24.59411621},"compassZ":{"unit":"uT","value":-15.24505615}}}]}'
	        sleep 2
	    fi
	    COUNTER=`expr $COUNTER + 1`
	done

This should now start sending alternate anomalous and non-anomalous measurements to Cumulocity on behalf of your demo device for a total duration of 30 seconds.

You should notice anomaly detection alarms for every anomalous measurement that it sends. These alarms generated from your device will be visible under the **Alarms** page of the Device Management application.