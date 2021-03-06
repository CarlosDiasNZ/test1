# Telstra IoT prototype


This example of IoT device reports current
Temperature and responds to the status requests and simulates the on/off command.<br>
This prototype utilises the AWS IoT cloud based platform to ingest the data.<br>
A client application subscribes and display the data.<br> see:(http://orgsensor.com) 

<p align="center">
  <img src="aws_heater.png" width="75%">
</p>

## Prerequisites

- Hardware: ESP8266 NodeMCU or any device with credentials
- Amazon AWS account
- Amazon's `aws` management tool (see https://aws.amazon.com/cli)


## Architecture

<p align="center">
  <img src="aws_heater.png" width="75%">
</p>

The data flow is as follows:

- A device uses I2C temperature sensor and sends data to the AWS IoT periodically
- An AWS IoT rule intercepts temperature data and stores it into the DynamoDB table
- A device gets synchronised with its AWS IoT shadow
- A frontend is running on AWS S3, talking to the device shadow to get the device state.


## Design and Implementation Process 

The application was designed to be platform agnostic and deployable in any modern architecture via scripts.   


