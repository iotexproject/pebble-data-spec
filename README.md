
# Specification of Pebble Data Format

# Contents

[1. Introduction](#1-introduction)

[1.1 Definition](#11-definition)

[1.2 Example](#12-example)

[2. Pebble JSON Object](#2-pebble-json-object)

[2.1 Sensor Data Object](#21-sensor-data-object)

[2.2 Digital Signature Data Object](#22-digital-signature-data-object)

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

&quot;SNR&quot;: 2,

&quot;VBAT&quot;: 4.0750732421875,

&quot;latitude&quot;: 3050.69225,

&quot;longitude&quot;: 11448.65815,

&quot;gas\_resistance&quot;: 1166811,

&quot;temperature&quot;: 36.23188400268555,

&quot;pressure&quot;: 1003.82000732421885,

&quot;humidity&quot;: 55.755001068115234,

&quot;gyroscope&quot;: [-12, 11, 14],

&quot;accelerometer&quot;: [-711, -231, 8260],

&quot;timestamp&quot;: &quot;3443547577&quot;

},

&quot;signature&quot;: &quot;D7797968EAA3FFE5F8057C9D97F707A4A96CBFC250115FE6293EBA5E90327174643A8CB823110376A5D30201463CF69CDF8CBF1C050EB85B023CABFB589C3222&quot;,

}

# 2. Pebble JSON Object

Pebble JSON Object consists of sensor data object and digital signature data object.

## 2.1 Sensor Data Object

The sensor data object includes the following sensor data collected by a Pebble tracker.

| Sensor Data | Data Type | Description |
| ----------- | --------- | ----------- |
| SNR             | Number  | Signal-to-noise ratio of NB-IoT/LET-M|
| VBAT            | Number  | Votage of battery|
| latitude        | Number  | gps latitude|
| longitude       | Number  | gps longitude|
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
| signature         | Number    | (r,s) value of an ECDSA signature |
