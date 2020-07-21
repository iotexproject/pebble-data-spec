
# Specification of Pebble Data Format

# Contents

[1. Introduction](#introduction)

[1.1 Definition](#definition)

[1.2 Example](#example)

[2. Pebble JSON Object](#pebble-json-object)

[2.1 Sensor Data Object](#sensor-data-object)

[2.2 Digital Signature Data Object](#digital-signature-data-object)

# 1. Introduction

JavaScript Object Notation (JSON) is utilized to represent the sensor data collected by a Pebble tracker as well as the corresponding ECDSA digital signature. The data type includes *Number*, *String* and *Array*.   

## 1.1 Definition

The data types used in the Pebble data format are defined as follows:  

| Data Type | Data Size | Data Range |
| ----------| --------- | ---------- |
| Array     | 16-bit    | -32768 ~ +32768 |
| Number    | 64-bit    | -1.79E+308 ~ +1.79E+308|
| String    | null-terminated string | 

## 1.2 Example

An example of the Pebble data format is shown below:

{

&quot;message&quot;: {

&quot;SNR&quot;: 3,

&quot;VBAT&quot;: 0.14076246321201324,

&quot;gas\_resistance&quot;: 1166811,

&quot;temperature&quot;: 33.33333206176758,

&quot;pressure&quot;: 996.3800048828125,

&quot;humidity&quot;: 78.01000213623047,

&quot;gyroscope&quot;: [-18, -3, 18],

&quot;accelerometer&quot;: [166, 132, 8395],

&quot;timestamp&quot;: &quot;1630575085&quot;

},

&quot;signature\_r&quot;: &quot;1EE739A0297D3D85&quot;,

&quot;signature\_s&quot;: &quot;2771F48356B03101DE25FB2511485C0E8EC118020908DC727EF8C34A461818E4&quot;

}

# 2. Pebble JSON Object

Pebble JSON Object consists of sensor data object and digital signature data object.

## 2.1 Sensor Data Object

The sensor data object includes the following sensor data collected by a Pebble tracker.

| Sensor Data | Data Type | Description |
| ----------- | --------- | ----------- |
| SNR             | Number  | Signal-to-noise ratio of NB-IoT/LET-M|
| VBAT            | Number  | Votage of battery|
| gas\_resistance | Number  | Air quality |
| temperature     | Number  | Environmental temperature |
| pressure        | Number  | Air pressure |
| humidity        | Number  | Environmental humidity |
| gyroscope       | Array   | Angular velocity around the X-axis, Y-axis and Z-axis |
| accelerometer   | Array   | Acceleration along the X-axis, Y-axis and Z-axis |
| timestamp       | String  | Timestamp of sensor data sampling |

## 2.2 Digital Signature Object

The Pebble tracker utilizes ECDSA over the elliptic curve sepc256r1 to sign the collected sensor data (i.e., the &quot;message&quot sub-object in the Pebble data format) and the digital signature data object contains the following signature data. 

| Digital Signature | Data Type | Description |
| ----------------- | --------- | ----------- |
| r                 | Number    | r value of an ECDSA signature |
| s                 | Number    | s value of an ECDSA signature |
