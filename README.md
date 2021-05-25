
# Specification of Pebble Data Format

# Contents

[1. Introduction](#1-introduction)

[1.1 Definition](#11-definition)

[1.2 Example](#12-example)

[2. Pebble JSON Object](#2-pebble-json-object)

[2.1 Sensor Data Object](#21-sensor-data-object)

[2.2 Digital Signature Object](#22-digital-signature-object)

[3 pebble-simulator](#3-pebble-simulator)


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
```
  "message": {
    "snr": 19,
    "vbat": 4167,
    "latitude": 20000,
    "longitude": 20000,
    "gasResistance": 7745665,
    "temperature": 24.389999389648438,
    "pressure": 1003,
    "humidity": 67.24214935302734,
    "light": 0,
    "temperature2": 29.3176326751709,
    "gyroscope": [
      -2,
      3,
      1
    ],
    "accelerometer": [
      -35,
      110,
      8226
    ],
    "timestamp": "1621943329",
    "random": "E1915DBE2ACCC9F3",
    "eccPubkey": "E1B955AEDF34D18921E3DC2133F2B785BA4C40DBC1502A8BF6ECE674B80E25D8822C4686723BBC3CB4A58D881DE053A1444EE1873E5916907D2F8819ECC7A1B6"
  },
  "signature": {
    "r": "597E7BF0F5C85D7A84C3C409CA358DE3C27A072587C884AE0452BD93D8F72F39",
    "s": "ACF44E758925A2454DB1880B31A3B1B11EEAE9BCEE67C423DADF8510B1A244CC"
  }
```
# 2. Pebble JSON Object

Pebble JSON Object consists of sensor data object,digital signature data object and configure object.

## 2.1 Sensor Data Object

The sensor data object includes the following sensor data collected by a Pebble tracker.

| Sensor Data | Data Type | Description |
| ----------- | --------- | ----------- |
| SNR             | Number  | Signal-to-noise ratio of NB-IoT/LET-M|
| VBAT            | Number  | Votage of battery|
| latitude        | Number  | gps latitude|
| longitude       | Number  | gps longitude|
| gasResistance | Number  | Air quality |
| temperature     | Number  | Environmental temperature |
| pressure        | Number  | Air pressure |
| humidity        | Number  | Environmental humidity |
| light           | Number  | Ambient light |
| gyroscope       | Array   | Angular velocity around the X-axis, Y-axis and Z-axis |
| accelerometer   | Array   | Acceleration along the X-axis, Y-axis and Z-axis |
| timestamp       | String  | Timestamp of sensor data sampling |
| random          | String  | Random number (16 numbers) |

## 2.2 Digital Signature Object

The Pebble tracker utilizes ECDSA over the elliptic curve sepc256r1 to sign the collected sensor data (i.e., the &quot;message&quot sub-object in the Pebble data format) and the digital signature data object contains the following signature data. 

| Digital Signature | Data Type | Description |
| ----------------- | --------- | ----------- |
| r                 | Number    | r value of an ECDSA signature |
| s                 | Number    | s value of an ECDSA signature |


# 3. [pebble-simulator](https://github.com/iotexproject/pebble-simulator)
 A simulator for producing pebble data, write it to a local file and publish to AWS MQTT, interact with a local or remote iotex block chain node to get a MQTT endpoint and generate RSA key pair which used to decrypt the endpoint .
