# Configuration

- [Configuration](#configuration)
  - [Configure PLC Connection](#configure-plc-connection)
  - [Configure Energy Manager](#configure-energy-manager)
    - [Create Sankey Diagram](#create-sankey-diagram)
    - [Create Duration Curve](#create-duration-curve)
    - [Create KPI](#create-kpi)
    - [Create Heatmap Diagram](#create-heatmap-diagram)
    - [Create Cost Calculation](#create-cost-calculation)
    - [Create Line Diagram](#create-line-diagram)
    - [Create Bulk Diagram](#create-bulk-diagram)
    - [Create Energy Media Analysis](#create-energy-media-analysis)
    - [Create Gantt Diagram](#create-gantt-diagram)

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

## Configure Energy Manager

Open the app Energy Manager on your Industrial Edge Device.

Within the Energy Manager you can create custom dashboards for data analysis. The input data comes from the previously configured app Data Service. The modelled data structure is then automatically displayed in the Energy Manager navigation tree.

At least one dashboard must be created on the dedicated asset. Depending on the needs, there are several widget types available:

![widgets](/docs/graphics/Widgets.png)

### Create Sankey Diagram

​Using the ​Sankey diagram​, energy flows can be displayed as arrows whose width is proportional to the flow rate. This makes it easy for you to recognize, for example, how energy is flowing through your plant.

First you need to create a dashboard, klick on "add dashboard"

Click "My Plant" at the top of the left side and create first widget:

![Energy_Manager_create_first_widget](graphics/Energy_Manager_create_first_widget.PNG)

Select the Sankey Diagram widget:

![Energy_Manager_Sankey_Diagram_widget](graphics/Energy_Manager_sankey_diagram_widget.PNG)

Create nodes which will be linked to the parameters. Select a colour for the respective nodes:

![Energy_Manager_Sankey_Diagram_define_display_options_nodes](graphics/Energy_Manager_sankey_diagram_define_display_options_nodes.PNG)

Link the nodes with the parameters of the respective parameters. Note the energy flow of the respective parameters:

![Energy_Manager_Sankey_Diagram_define_display_options_links](graphics/Energy_Manager_sankey_diagram_define_display_options_links.PNG)

Create Sankey diagram of combined energy and water consumption including single energy and water values:

![Energy_Manager_Sankey_Diagram](graphics/Energy_Manager_sankey_diagram.PNG)

### Create Duration Curve

​By using the ​duration curve​, you can display a chart sorted by size. ​In the ​duration curve​, the measured values of a specific time range are displayed collected and sorted. The highest value is displayed on the far left, and the lowest value on the far right.

Select the Duration Curve widget:

![Energy_Manager_Duration_Curve_widget](graphics/Energy_Manager_duration_curve_widget.PNG)

Create single Duration Curve diagrams for each energy and water consumption value:

![Energy_Manager_Duration_Curve](graphics/Energy_Manager_duration_curve.PNG)

### Create KPI

Click on "Configuration" on the left side and select "KPI types":

![Energy_Manager_select_KPI](graphics/Energy_Manager_select_KPI.PNG)

Create a new KPI type, klick on "New KPI type".

Create a calculation of the total energy consumption via KPI formula:

![Energy_Manager_total_energy_consumption](graphics/Energy_Manager_total_energy_consumption_KPI.PNG)

### Create Heatmap Diagram

​Using the ​Heatmap​, you can visualize the intensity of data values over time. You can, for example, display the energy consumption (red = high energy consumption; green = low energy consumption), temperatures or production quantities in a specific time range.

Select the Heatmap widget:

![Energy_Manager_Heatmap_widget](/docs/graphics/Energy_Manager_heatmap_widget.PNG)

Create Heatmap diagram of total energy consumption based on KPI:

![Energy_Manager_Heatmap_total_energy_consumption_KPI](/docs/graphics/Energy_Manager_Heatmap_KPI.PNG)

![Energy_Manager_Heatmap_total_energy_consumption_display](/docs/graphics/Energy_Manager_Heatmap_display.PNG)

### Create Cost Calculation

Calculation of the costs for energy and water via KPI formula. Calculation of total costs per bottle via KPI formula.

Created KPI type “KPI costs energy total” and “KPI costs total”:

![Energy_Manager_KPI_costs_energy_total](/docs/graphics/Energy_Manager_KPI_costs_energy_total.PNG)

![Energy_Manager_KPI_total_costs](/docs/graphics/Energy_Manager_KPI_total_costs.PNG)

### Create Line Diagram

Create line diagram of costs for energy and water and total costs per bottle based on KPI:

![Energy_Manager_line_diagram_parameter](/docs/graphics/Energy_Manager_line_diagram_parameter.PNG)

![Energy_Manager_line_diagram_costs](/docs/graphics/Energy_Manager_line_diagram_costs.PNG)

### Create Bulk Diagram

Calculation/Aggregation of energy consumption within 15 minutes:

![Energy_Manager_energy_consumption_15_minutes](/docs/graphics/Energy_Manager_energy_consumption_15_minutes.PNG)

Create Bulk diagram for aggregated energy consumption:

![Energy_Manager_energy_consumption_Bulk_diagram](/docs/graphics/Energy_Manager_energy_consumption_Bulk_diagram.PNG)

### Create Energy Media Analysis

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

### Create Gantt Diagram

​The Gantt widget shows you the status of a machine at a glance using different color codes. For example, the status can represent the current state or the state within a specific time range.

Select the Heatmap widget:

![Energy_Manager_Gantt_widget](/docs/graphics/Energy_Manager_gantt_widget.PNG)

Creating status mappings for the "Gantt" widget:

![Energy_Manager_Status_Mapping](/docs/graphics/Energy_Manager_gantt_status_mapping.PNG)

Click on the "Enable Zoom" button to zoom in on the Gantt Chart too see the Machine Status better:

![Energy_Manager_Gantt_chart](/docs/graphics/Energy_Manager_gantt_chart.PNG)

![Energy_Manager_Gantt_chart_Zoom](/docs/graphics/Energy_Manager_gantt_chart_zoom.PNG)
