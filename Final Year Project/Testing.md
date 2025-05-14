I think building an example manufacturing company with plenty of edge cases to test out Summerville would be best. I think for final deployment, it should be deployed along side the final app to see it running live.

For data sources that I want it to be able to work with:

- Postgres (both the main database used for the app but also example data from there)
- Microsoft SQL Server Management
- Kafka
- Excel

I want to at least for charts, visuals and components have
Output:

- Card Container
- Line Chart
- Donut Chart
- 2d d3js MAP
- 3d three js graph with particle effects to demonstrate live data

Input:

- Date Input
- Text Input
- Select List
- Choice Box
- Select Map
- Filter by Legends or selected Nodes.

----

For my prototype, we will have analytics dashboard page that will be for 1 section of my CPU.

It will  gave 3 statitons, 9 machines.

2 data sources and 1 live data sensor.

These machines are cutting machines operated by machinists. Production data for the machine is directly uploaded to a mssql database, stating the part produced, time it was made, what machine it's going to next any faults with it being made.. It also uses live sensor data to monitor the quality of the parts produced, checking for blemishes or faults, and applies a score to the fault. As well as monitoring the heat of the finished product.

There  is also a shift handover excel that documents the shift range, as well as who was responsible for a given shift at a given time range.

2 Charts, 2 Kpi's, 2 inputs.

KPI's Per machine:
- Total output
- Parts Per Hour
In general:
- total amount produced.

inputs include:
- A select list for the given time and time span
- Select list (meant to be the chart but for now we'll use a list) of the different machines to filter by that too

Charts include:0o
- A bar chart showing amount produced against each machine, with the legend being the shift produced.
- A table with a filter showing the list of all parts that are outside the given accepted range.

Intial look for finished app:
- Image of the final analytics display board
  ![[IMG_20241220_121115.webp|436]]
  
Intial look for app as it's being made:
- Image of connecting to those data


![[Pasted image 20241220123652.webp]]

connection-name: Server=localhost\SQLEXPRESS;Database=master;Trusted_Connection=True;
System Name	LAPTOP-R4L4TEJT

Administrators: C:\Program Files\Microsoft SQL Server\160\Setup Bootstrap\Log\20241220_122718

Features: C:\SQL2022\Express_ENU

Version: C:\Program Files\Microsoft SQL Server\160\SSEI\Resources