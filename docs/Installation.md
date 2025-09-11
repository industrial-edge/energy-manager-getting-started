# Configuration

- [Configuration](#configuration)
  - [Configure PLC Connection](#configure-plc-connection)
    - [Databus](#databus)
    - [OPC UA Connector](#opc-ua-connector)
    - [Data Service](#data-service)

## Configure PLC Connection

To read data from the PLC and provide the data, we will configure the app OPC UA Connector with the Common Configurator to establish a connection to the PLC via OPC UA. The OPC UA Connector Connector publishes the data on the Databus, where the app Data Service can model and collect the energy data, that is needed. In order to build this infrastructure, these apps must be configured properly:

- Databus
- OPC UA Connector
- Common Configurator
- Data Service

Please refer to [using the IIH](https://github.com/industrial-edge/data-service) for detailed instructions.

Finally the configurations should look like this:

### Databus

![ie_databus](/docs/graphics/IE_Databus.PNG)

### OPC UA Connector configured with the Common Configurator

![OPC_UA Connector Source](/docs/graphics/OPCUA_Connector_Data_Source.PNG)

![OCUA Connector Tags](/docs/graphics/OPCUA_Connector_Configuration.PNG)

![Common Configurator Databus](/docs/graphics/OPCUA_Connector_Configuration_2.PNG)

### IIH Essentials

![IIH Atrributes](/docs/graphics/Data_Service_Data_Service_Variable.PNG)

![IIH Connectors](/docs/graphics/IIH_Connectors.PNG)

![IIH Databus](/docs/graphics/IIH_Databus.PNG)
