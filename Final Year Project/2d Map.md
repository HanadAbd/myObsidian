Honestly might be easier and more challenging to just make it with canvas elements, instead of d3.js.

Reason being just limiting the amount of package dependecies, more learning and more control. Especially when it comes portraying live data, heat maps, 3d dimensional graphs.

Could follow the structure of graph with nodes and edges.

Main goal should be, being able to translate a graph with the relevant data and schema and settings, and produce it as a useable, moveable, zoom able, and editable canvas element.

And then limit to UI wouldn't be too much of an issue.'

Different options are:

- Heat maps (density gradient of different data at different points or areas)
- Choropleth maps (Similar to heat maps, but logarithmic)
- Pinging nodes where live data is added to it.
- Flow maps (To show the flow of data being added)
- Selecting a node zooms in on it and slightly greys out the other nodes.
- Hovering over a node displays it's tooltip with the corresponding data for it
![[Pasted image 20241025191124.png]]