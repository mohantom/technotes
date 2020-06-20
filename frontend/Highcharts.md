Highcharts
--------------

Course: Realtime web dashboard highcharts
Colorbrewer2.org
Highcharts
Code.jquery.com/jquery-1.11.3.min.js
Code.highcharts.com/highcharts.js
Bar chart
Compare distinct values
Use color to highlight a single bar (use 4 colors at most)
Do not change Y axis to not start at zero
Avoid stacked bar chart
Line chart
	Compare values over time
	Show trend lines
	Do not shrink x axis to show steeper +/-
	Do not label every data point, use tooltips
Scatter plot
	Disaggregate results
	Use distinct measurements
	Do not aggregate highly
	Use less colors
Map
	Use bubbles with size
	Color by another measurement
	Do not fill entire area
	Do not use pies
Chart types to avoid
	Radial, donut chart, stacked, 3D, decorative (gauge)
Funnel
Code.highcharts.com/modules/funnel.js
 
Heat map
Code.highcharts.com/modules/heatmap.js
Code.highcharts.com /modules/exporting.js
 

Scatter plot
 
Tree map
	/heatmap.js, /treemap.js
 

Box plot
	Code.highcharts.com/highchart-more.js
 

Stock plot
	/stock/highstock.js
 
Map
	/maps/highmaps.js
	/maps/modules/data.js
	/mapdata/countries/us/us-all.js
 

Data
/modules/data.js
$.get(‘top-users.csv’, function(csvData) {
Data: {
	Csv: csvData
}
Google spreadsheet: 
 

Data from API
Same origin policy
	Get data from another domain
	JSONP callback
 

Live Data
	Node.js with socket.io
 
Recursive calling itself, every 1 second. -> poll data (not push)

Solid, semi-transparent, linear gradient, radial gradient

Dashboard
Audience: Exploratory vs explainatory
Color: college course
Layout: 
 
	Events: { load: requestData() } // load live data from ajax
