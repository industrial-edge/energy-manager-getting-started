# Configuration and Usage

- [Configuration and Usage](#configuration-and-usage)
  - [Configure PLC Connection](#configure-plc-connection)
  - [Energy Manager: KPI calculation](#energy-manager-kpi-calculation)
    - [Create KPI type](#create-kpi-type)
    - [Create KPI instance](#create-kpi-instance)
  - [Energy Manager: Data analysis with widgets](#energy-manager-data-analysis-with-widgets)
    - [Create heatmap diagram](#create-heatmap-diagram)
    - [Create diagram](#create-diagram)
    - [Create sankey](#create-sankey)
    - [Create duration curve](#create-duration-curve)
  - [Energy Manager: Energy media analysis](#energy-manager-energy-media-analysis)

## Configure PLC Connection

To read data from the PLC and provide the data, we will use the app S7 Connector to establish a connection to the PLC via OPC UA. The S7 Connector publishes the data on the Databus, where the app Data Service can model and collect the energy data, that is needed. In order to build this infrastructure, these apps must be configured properly:

- IE Databus
- SIMATIC S7 Connector
- Data Service

Please refer to [using the Data Service](https://github.com/industrial-edge/data-service) for detailed instructions.

Finally the configurations should look like this:

**IE Databus**

![ie_databus](/docs/graphics/IE_Databus.PNG)

**S7 Connector**

![S7_connector_data_source](/docs/graphics/S7_Connector_Data_Source.PNG)

![s7_connector_config](/docs/graphics/S7_Connector_Configuration.PNG)

**Data Service**

![Data_Service_Aspects](/docs/graphics/Data_Service_Data_Service_Variable.PNG)

## Energy Manager: KPI calculation

KPI stands for **Key Performance Indicator**. KPI types are formulas made up of operands, constants, and operators. A KPI instance can be created either during the widget configuration or in the parameter list on the asset. KPI types can be instantiated multiple times. When you make changes to the KPI type, these changes are also implemented in all KPI instances.

Open the app Energy Manager on your Industrial Edge Device.

### Create KPI type

In this example a KPI type could be:

```
Total energy = Energy filling tank + Energy heating tank + Energy filling bottles
```

Follow these steps to create a new KPI type:

- select the tab "Configuration"
- choose "KPI types"
- click "New KPI type"
- enter a unique name and a unit
- in the formula editor, use operants and operators to create this formula:

![Energy_Manager_KPI_Type](/docs/graphics/Energy_Manager_KPI_Type.png)

- save the KPI type

It is also possible to create a **cost calculation** via KPI formulas. In this example we calculate the energy costs as well as the water costs.

Create two further KPI types:
```
Costs energy = Total energy * 0.35
```

![Energy_Manager_KPI_Type_2](/docs/graphics/Energy_Manager_KPI_Type_2.png)

```
Costs water = Water consumption * 0.21
```

![Energy_Manager_KPI_Type_3](/docs/graphics/Energy_Manager_KPI_Type_3.png)

### Create KPI instance

KPI instances can be created either in the parameter list of an asset or in the "Parameter" step when a widget is created. They can be derived from a KPI type or can be created typeless. Automatic KPI instances are created additionally when you create energy media and assign contract information. New KPI instances cause costs. The number of currently used KPI instances is displayed in the tab "Settings" under "Usage information".

Follow these steps to create a KPI instance in the parameter list based on our KPI type 'Total energy':

- select the tab "My Plant"
- go to the dedicated asset "Energy" and open the parameter view

![Energy_Manager_Parameter_View](/docs/graphics/Energy_Manager_Parameter_View.png)

- click "New KPI instance" to add an instance
- enter a unique instance name
- select "On the basis of a KPI type"
- select the KPI type for 'Total energy'
- link all operands to a variable coming from Data Service and set the aggregation to "Last"

![Energy_Manager_KPI_Instance](/docs/graphics/Energy_Manager_KPI_Instance.png)

- save the KPI instance

## Energy Manager: Data analysis with widgets

Within the Energy Manager you can create custom dashboards for data analysis. The input data comes from the previously configured app Data Service. The modelled data structure is then automatically displayed in the Energy Manager navigation tree.

At least one dashboard must be created on the dedicated asset:

- select the tab "My Plant"
- go to the dedicated asset "Energy"
- click "Create first dashboard"
- enter a name for the dashboard and save

![entry](/docs/graphics/Energy_Manager_Entry.png)

Depending on the needs, there are several widget types available:

![widgets](/docs/graphics/Widgets.png)

Below it is described how to create some characteristic widgets for energy data.

### Create heatmap diagram

Using the Heatmap, you can visualize the intensity of data values over time.

You can, for example, display the energy consumption (red = high energy consumption; green = low energy consumption) in a specific time range. Here we create the Heatmap based on the previously generated KPI instance 'Total energy':

- select the tab "My Plant"
- go to the newly created dashboard
- select "Create first widget" to start the wizard

1) choose the Heatmap widget type > Continue
2) enter a widget name and set the KPI calculation period to 1 Minute > Continue
3) click "Select parameter" and choose the KPI instance for 'Total energy' > Continue
4) no need to change anything in the general display options > Continue
5) no need to change anyting in the Heatmap dispaly options > Finish

This Heatmap now shows the total energy consumption over one day:

![Energy_Manager_Heatmap](/docs/graphics/Energy_Manager_Heatmap.png)

### Create diagram

Using the Diagram widget, you can display parameter values or calculated KPI values over time. There are several diagram types available. Also different aggregation functions can be selected for the values.

**Bulk diagram**

Here we want to display the KPI value for 'Total energy' for every 15 minutes as bulk diagram:

- go to the dashboard
- click the settings button and choose "New widget" to start the wizard

1) choose the Diagram widget type > Continue
2) enter a widget name and set the KPI calculation period to 15 Minutes > Continue
3) click "Select parameter" and choose the KPI instance for 'Total energy' > Continue
4) no need to change anything in the general display options > Continue
5) choose "Bar" in the dropdown field for the chart type > Finish

![Energy_Manager_Bulk_Diagram](/docs/graphics/Energy_Manager_Bulk_Diagram.png)

**Line diagram**

Here we want to display the consumption costs for energy and water as line diagram. The diagram is based on the predefined KPI types 'Costs energy' and 'Costs water', but the KPI instances must be defined within the wizard:

- go to the dashboard
- click the settings button and choose "New widget" to start the wizard

1) choose the Diagram widget type > Continue
2) enter a widget name and set the KPI calculation period to 15 Minutes > Continue
3) click "New KPI instance" to create an instance based on the KPI type 'Costs energy', enter a name, select the KPI type and link the parameter 'TotalEnergy' to the already existing instance of 'Total Energy'

![Energy_Manager_Line_KPI_Instance_1](/docs/graphics/Energy_Manager_Line_KPI_Instance_1.png)

3) Again click "New KPI instance" to create an instance based on the KPI type 'Costs water', enter a name, selectthe KPI type and link the parameter 'WaterConsumption' to the signal 'waterConsumptionFillingTank' with aggregation 'Last' > Continue

![Energy_Manager_Line_KPI_Instance_2](/docs/graphics/Energy_Manager_Line_KPI_Instance_2.png)

4) no need to change anything in the general display options > Continue
5) no need to change anyting in the Chart dispaly options > Finish

![Energy_Manager_Line_Diagram](/docs/graphics/Energy_Manager_Line_Diagram.png)

### Create sankey

Using the Sankey diagram, energy flows can be visualized. The energy flows are displayed as arrows whose width is proportional to the flow rate.

Here we want to display the water and energy consumption as Sankey:

- go to the dashboard
- click the settings button and choose "New widget" to start the wizard

1) choose the Sankey widget type > Continue
2) enter a widget name and set the KPI calculation period to 1 Minute > Continue
3) click "Select parameter" and choose the energy and water parameter (hint: choose them in the order you would like to see them in the diagram), for all set aggregation to 'Last' > Continue

![Energy_Manager_Sankey_Parameter](/docs/graphics/Energy_Manager_Sankey_Parameter.png)

4) no need to change anything in the general display options > Continue
5) in the tab 'Nodes' you need to create nodes with proper colours, that are later linked to the parameter:

![Energy_Manager_Sankey_Nodes](/docs/graphics/Energy_Manager_Sankey_Nodes.png)

5) go to the tab 'Links' and specify the links for each parameter from source node to destination node (you can also scale a link to show the proportions right):

![Energy_Manager_Sankey_Links](/docs/graphics/Energy_Manager_Sankey_Links.png)

7)  > Finish

![Energy_Manager_Sankey](/docs/graphics/Energy_Manager_Sankey.png)

### Create duration curve

​By using the ​duration curve​, you can display a chart sorted by size. ​In the ​duration curve​, the measured values of a specific time range are displayed collected and sorted. The highest value is displayed on the far left, and the lowest value on the far right.

Select the Duration Curve widget:

![Energy_Manager_Duration_Curve_widget](graphics/Energy_Manager_duration_curve_widget.PNG)

Create single Duration Curve diagrams for each energy and water consumption value:

![Energy_Manager_Duration_Curve](graphics/Energy_Manager_duration_curve.PNG)

## Energy Manager: Energy media analysis

​You use the energy media analysis to manage and calculate energy data, such as power and gas from the machines and plants. In the configuration, you create all required energy media and can then define for each asset which energy data it requires. Using the stored contract information, you can then convert the consumption of the individual energy media directly into the resulting costs and CO2 emissions.

Select your dashboard and click on the name of the dashboard. Click on the "Asset Configuration":

![Energy_Manager_asset_configuration_for_energy_data](/docs/graphics/Energy_Manager_asset_configuration_for_energy_data.PNG)

Click on "Assignment of energy medium":

![Energy_Manager_asset_configuration_menu_contract_information](/docs/graphics/Energy_Manager_asset_configuration_menu_contract_information.PNG)

Click on "New row" to select the Energy Medium, for configure the Energy Media click on "Energy medium":

![Energy_Manager_asset_configuration_energy_media_assignment](/docs/graphics/Energy_Manager_asset_configuration_energy_media_assignment.PNG)

![Energy_Manager_asset_configuration_energy_media](/docs/graphics/Energy_Manager_asset_configuration_energy_media.PNG)

Go back to "Asset Configuration" and click on "Contract Information".

Click on "Add energy medium" to select your energy medium.

Configure the contract information for your energy medium and the currency:

![Energy_Manager_asset_configuration_contract_information](/docs/graphics/Energy_Manager_asset_configuration_contract_information.PNG)

​Next, you can display the energy media analysis directly in the energy media dashboard. The dashboard is displayed automatically:

![Energy_Manager_Energy_media_display](/docs/graphics/Energy_Manager_Energy_media_display.PNG)
