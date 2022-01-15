# YL-800T LoRa Radio Module Configuration Library

Library for building AT commands to set configuration parameters of the YL-800T module.

YL-800T is a LoRa radio module with a TTL UART interface.

This device is available from China or from DFRobot. It is simple to use in the standard configuration, but requires specific commands to set parameters for other configurations, which can be difficult since the manufacturer's website and documentation is in Chinese.

## Configuring module

Commands can be sent via the UART interface to configure parameters of the module. The manufacturer provides Windows software for configuring the module. This library supports building the messages to perform this same configuration and parsing the response. It does not cover serial device communication.

## Module operation

In normal operation, data received via the UART interface is transmitted over radio. The data is received by other modules, and transmitted via UART.

The EN pin must be pulled low in order to enable communication.

### Standard

In standard mode, the data is received by all modules in the network. All modules communicate transparently.

### Star

In star network mode, the central module transmits a node id in the first two bytes of a message. The module in node mode with matching node id will receive the message and transmit the remaining data via UART (excluding the node id). A node with id 0x0000 will receive all messages. The central module can use id 0xFFFF to broadcast to all nodes.

To save power, the EN pin of a node module can be pulled high to enter a low power state. The UART will be down, but radio data can still be received. When data is received, the AUX pin will be pulled low by the module. The EN pin should then be pulled low to enable UART and receive the data.
