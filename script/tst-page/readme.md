# Telstra IoT prototype


This example of IoT device reports current
Temperature and responds to the status requests and simulates the on/off command. This prototype utilises the AWS IoT cloud based platform to ingest the data.
A client application subscribes and display the data.
http:/orgsensor.com 


## Prerequisites

- Hardware: ESP8266 NodeMCU
- Amazon AWS account
- Amazon's `aws` management tool (see https://aws.amazon.com/cli)
- `mos` management tool installed
  (see [mos installation guide](https://mongoose-os.com/software.html))

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


