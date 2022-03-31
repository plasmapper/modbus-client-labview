# Modbus Client Library for LabVIEW
Yet another Modbus client library for LabVIEW.

## Requirements
LabVIEW 2015 and higher.

## Features
1. RTU, ASCII and TCP protocols via serial or network connection.
2. Implemented read/write functions (Modbus function codes):
   - Read Coils / Discrete Inputs / Holding Registers / Input Registers (1/2/3/4)
   - Write Single Coil / Holding Register (5/6)
   - Write Multiple Coils / Holding Registers (15/16)
3. Splitting single read/write requests into multiple requests with valid number of memory elements. 
4. Automatic reconnection to device.
5. Support of multiple devices on the same serial port (VISA Lock/Unlock).
6. Possibility of other Modbus function code (including user-defined) implementation.

## Serial Port Settings
Modbus Serial Line Protocol and Implementation Guide states that:
1. 8 data bits should be used for Modbus RTU and 7 data bits - for Modbus ASCII.
2. 1 stop bit should be used if there is parity bit and 2 stop bits - if there is no parity bit.  

However there is a number of devices that do not follow these rules. So `Initialize Serial.vi` allows to set the same parameters as basic `VISA Configure Serial Port.vi`. Limitations on serial parameters can be implemented in higher level specific device library.

## Not implemented and user-defined Modbus function codes
All implemented Read/Write VIs internally use `Command.vi` with **function code** and **data in** as inputs and **data out** as output.
For Modbus TCP and Modbus ASCII this VI can be used with any function code, since these protocols allow to receive responce data without knowing its size beforehand. For Modbus RTU descendant class should be created with overriden `Read RTU Data.vi`.

## Examples
### Modbus Client.vi
Simple Modbus client application.
### Speed Test.vi
Tests client-server connection and measures transaction rate.
### Memory Test.vi
Tests Modbus server by writing to random memory locations, reading back and comparing data.

## Documentation
[Modbus (Wikipedia)](https://en.wikipedia.org/wiki/Modbus)  
[Modbus Protocol Specification](https://modbus.org/docs/Modbus_Application_Protocol_V1_1b3.pdf)  
[Modbus Serial Line Protocol and Implementation Guide](https://modbus.org/docs/Modbus_over_serial_line_V1_02.pdf)
