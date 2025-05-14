chartjs is just a manipulation of a canvas element.

Shouldn't be too hard.

Has a type configuration
Composed of array of labels and data and optional array of background colours.

Each column, bar, point etc. is based on index.

data[0] corresponds to label[0]

input for type of chart

data could just be array of a tuple with n dimensions, with n being how labels, data and other optional elements we may one to consider.

Make the chart upon initialisation, and use update functionality to replace it's data when updates are made in the page.

So passing the query to this chart, we'll have a rest API call to rest API service.

Maybe each query should be it's own endpoint to for that query, after passing it's requirements, it returns the configurations for the json of that graph.
