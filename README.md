# pebble-spec
Specifications of Pebble


**PebbleJson**  **格式介绍**

# 目录

[1. 简介 1](#_Toc46150598)

[1.1 定义 1](#_Toc46150599)

[1.2 例子 2](#_Toc46150600)

[2. PebbleJson Object 2](#_Toc46150601)

[2.1 Sensor数据对象 2](#_Toc46150602)

[2.2 签名数据对象 3](#_Toc46150603)

1.
# 简介

PebbleJson 使用JavaScript Object Notation (JSON)格式编码Pebble设备的传感器数据，以及传感器数据的数字签名。PebbleJson中包含传感器数据和对传感器数据的ECDSA数字签名，数据类型包括: Number、String、Array。

  1.
## 定义

PebbleJson中使用的数据类型定义:

●Array类型数据, 位宽16bit, 数值范围 -32768 ~ +32768

●Number类型数据, 位宽 64bit, 数值范围 -1.79E+308 ~ +1.79E+308

●String类型数据，null-terminated string

  1.
## 例子

PebbleJson数据实例

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

1.
# PebbleJson Object

PebbleJson Object包含Sensor数据object和签名数据object

  1.
## Sensor数据对象

● message ：sub Object保存sensor数据

● SNR： Number类型数据，指示NBIOT的信噪比

●VBAT： Number 类型浮点数据, 指示电池电压

●gas\_resistance： Number 类型数据，指示空气质量

●temperature： Number 类型数据，指示环境温度

●pressure： Number类型数据，指示大气压

●humidity： Number类型数据，指示环境温度

●gyroscope： Array类型数据，3 个数据分别表示陀螺仪的X，Y和Z轴角速率

●accelerometer: Array 类型数据，3 个数据分别表示陀螺仪的X，Y和Z轴加速度

●timestamp：String 类型数据，记录对sensot采样的时间

  1.
## 签名数据对象

●signature\_r： ECDSA secp256r1 算法对 &quot;message&quot; 字段做的数字签名 r 值

●signature\_s： ECDSA secp256r1 算法对 &quot;message&quot; 字段做的数字签名 s 值
