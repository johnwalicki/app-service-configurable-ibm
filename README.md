# app-service-configurable-ibm
EdgeX **app-service-configurable** Profile for IBM Watson IoT Platform

The [configuration.toml](/res/ibm-mqtt-export/configuration.toml) provided in this repository defines the [EdgeX app-service-configurable](https://github.com/edgexfoundry/app-service-configurable) **PROFILE** required to send MQTT data to [IBM Watson IoT Platform](https://cloud.ibm.com/catalog/services/internet-of-things-platform#about)

## Prerequisites

This tutorial can be completed using an IBM Cloud Lite account.

* Create an [IBM Cloud account](https://ibm.biz/BdzgKN)
* Log into [IBM Cloud](https://cloud.ibm.com/login)

## Install EdgeX

You can build the EdgeX Foundry services using the open source code on [Github](https://github.com/edgexfoundry), but more often than now you just need to get these services running so that you can connect your own services to them. To support that, the project publishes Docker images based on the latest stable release of the open source code, as well as docker-compose.yml files that will run all the necessary services together on your development machine. Learn more at https://www.edgexfoundry.org/get-started/

## Send MQTT Data to IBM Watson IoT platform

If you have an Edge device generating MQTT data, you might want to send the IoT data to the Cloud for Analytics, storage, Real Time alerts and modeling. IBM Cloud provides an IoT ingestion service, Watson AI services, Watson Studio data science portal that can help developers manage their IoT data and find insights.

EdgeX provides an [App-Service-Configurable](https://github.com/edgexfoundry/app-service-configurable/README.md) service as an easy way to get started with processing data flowing through EdgeX. This service leverages the App Functions SDK and provides a way for developers to use configuration instead of having to compile standalone services to utilize built in functions in the SDK. For a full list of supported/built-in functions view the README located in the App Functions SDK repository.

** Watson IoT Configuration Example:**

* Create a [Watson IoT Service instance](https://cloud.ibm.com/catalog/services/internet-of-things-platform)
* Create a Devicetype, Device ID and a secure Authentication token.
* Download this [configuration.toml](/res/ibm-mqtt-export/configuration.toml) and edit the **[Writable.Pipeline.Functions.MQTTSend.Addressable]** section.
* Enter your Watson IoT Organization (6 character <orgid>), <DeviceType>, <Device ID> and <Authentication token>.

```
[Writable.Pipeline.Functions.MQTTSend.Addressable]
  Address=   "<orgid>.messaging.internetofthings.ibmcloud.com"
  Port=      1883
  Protocol=  "tcp"
  Publisher= "d:<orgid>:<devicetype>:<deviceid>"
  User=      "use-token-auth"
  Password=  "<Authentication-Token>"
  Topic=     "iot-2/evt/status/fmt/json"
```  

* Save this file
* Restart docker-compose
