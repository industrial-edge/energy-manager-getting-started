# Configuration

- [Configuration](#configuration)
  - [Configure PLC Connection](#configure-plc-connection)
    - [Databus](#ie-databus)
    - [OPC UA Connector](#simatic-s7-connector)
    - [Data Service](#data-service)

## Configure PLC Connection

To read data from the PLC and provide the data, we will use the app S7 Connector to establish a connection to the PLC via OPC UA. The S7 Connector publishes the data on the Databus, where the app Data Service can model and collect the energy data, that is needed. In order to build this infrastructure, these apps must be configured properly:

- Databus
- OPC UA Connector
- Data Service

Please refer to [using the Data Service](https://github.com/industrial-edge/data-service) for detailed instructions.

Finally the configurations should look like this:

### Databus

![ie_databus](/docs/graphics/IE_Databus.PNG)

### OPC UA Connector

![S7_connector_data_source](/docs/graphics/S7_Connector_Data_Source.PNG)

![s7_connector_config](/docs/graphics/S7_Connector_Configuration.PNG)

### Data Service

![Data_Service_Aspects](/docs/graphics/Data_Service_Data_Service_Variable.PNG)
