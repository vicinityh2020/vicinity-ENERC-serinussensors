# Vicinity-ENERC-serinussensors

The adapter bridges communication with the Serinus Sensors installed at Enercoutim's SolarLab and Municipal Cluster (school, nursing home, swimming pool and sports pavilion) of Martim Longo. This adapter will get data from the sensors (Temperature, Humidity, CO2, Noise, Luminance and Movement) and make it available to Vicinity. This data will be used by the "Smart School" and Dynamic Audit Value-Added Service (VAS).

# 1. Infrastructure Overview
This is a Vicinity Adapter for ENERC Pilot Infrastructure. It is used to describe the Interior Environmental Quality (IEQ) sensors from Serinus which are already deployed at the mentioned facilities and connected to Serinus Cloud Service.

# 2 - Configuration and deployment

## Requirements
- JDK 1.8 or higher
- Node Red v0.18

## Device Specific Information
The Serinus sensors collect data every 30 minutes and send it to the Serinus Cloud Platform. Then there may be two options: (a) Serinus will build the adapter and include it on their cloud service, or (b) the Serinus REST API can be used to retrieve data from the Serinus Cloud platform to a Raspberry Pi that will act as a Vicinity Gateway and make the adapter to run locally.

For option (b) a Raspberry Pi located in the SolarLab and/or School and running Raspbian with Node-Red will perform the following actions:
####
1. Every X seconds a Node Red trigger node triggers an HTTP Request node which gets data from the Serinus Cloud platform 
2. Gathered information is parsed and made available to Vicinity
3. A function node takes values and performs Smart School and Dynamic Audit VAS Logic
4. Dashboard nodes will be used to build an initial version of the VAS UI.

This same Raspberry Pi will be running Vicinity Gateway and Agent. An HTTP Request Node on NodeRed will be able to make GET and POST Requests to Vicinity.

# 3 - Functionality and API

## Endpoints
- GET /objects (optional): Retrieve all devices Thing Descriptions (TDs) for registration to VICINITY. This functionality is optional since auto-registration of devices will be performed.
- GET /objects/{oid}/properties/{pid} - Returns last known value and time the value was received by the device. {oid} is UUID of device and {pid} is a property identifier.

## Functions
- Send device TD to the Vicinity Agent at Start Up
- Publish every new measurement to a specific Vicinity event topic.

