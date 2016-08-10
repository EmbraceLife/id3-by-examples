# id3-by-examples
**Lessons learnt**    
1. the better I understand previous work, the more confident I am to tackle new problems
2. If there is no need to read or watch my work again and again, then I should not make them in the first place
3. notes and videos as specific and short as possible

[Line Charts](#line-charts)        
[Brush and Zoom](#brush-and-zoom)

## Line Charts


### Multi-line Chart

**Challenge**    
- Data: 3 cities' daily temperatures over a number of periods    
- Draw 3 lines with diff colors on the same chart    
- Label each line with a city name      

[Code Overview](http://bl.ocks.org/EmbraceLife/aa9155f9d0baaa3429e087b34980c929)    
[Full Demo](http://blockbuilder.org/EmbraceLife/aa9155f9d0baaa3429e087b34980c929)  


**Step 0**   
Set up a starting template    

[Video](https://youtu.be/CZZHkxJIja0)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/039276f3ae83f19a5e12a4e2d4c54af8)


**Step 1 -> Create svg canvas and g placeholder**   
Create a svg canvas
```html
<svg width="960" height="500"></svg>
```    
select and assign the canvas       
```javascript
svg = d3.select("svg")
```
g placeholder to Locate a tarting point for inner canvas    
```javascript
g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")")
```

[Video](https://youtu.be/MroiTmauDeg)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/d3bb1c7c3275ae84a5b8a12f28b1f2a5)


**Step 2 -> Create funcs to map data points to px**   
map date to px on x-axis => update px range     
```javascript
d3.scaleTime().range([0, width])
```
map temperature to px on y-axis => update px range    
```javascript
d3.scaleLinear().range([height, 0])
```
map city names to color, give 20 default colors         
```javascript
d3.scaleOrdinal(d3.schemeCategory10)
```
transform data points into (x, y) px position for drawing lines    
```javascript
d3.line().curve(d3.curveBasis).x(function(d) { return x(d.date); }).y(function(d) { return y(d.temperature); })
```

[Video](https://youtu.be/uiwh0EJPKr8)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/c675ec2a11d547ac62ab57c04f7a4e02)  


**Step 3 -> Load data and Process each row of data**   
row func to make use of column names
```javascript
function type(d, _, columns) {}
```
Format date for data file        
```javascript
var parseTime = d3.timeParse("%Y%m%d");
  d.date = parseTime(d.date);
```
access each column's value of each row, except Date/first column    
```javascript
for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
```
load data file and preprocess data for use    
```javascript
d3.tsv("data.tsv", type, function(error, data) {}
```
Reorganise dataset by columns    
```javascript
var cities = data.columns.slice(1).map(function(id) {
    return {id: id,
            values: data.map(function(d) {
                return {date: d.date,
                        temperature: d[id]};})
```


[Video1](https://youtu.be/NgjhKnoWGZg)    
[Video2](https://youtu.be/AnSUbBXXvnM)   
[Practice Demo](http://blockbuilder.org/EmbraceLife/3f7287859b3c582cb2a451a42a6faf58)


**Step 4 -> update domain-range for scale-map functions above**   
=> update date range for (func => map date to px on x-axis)    
```javascript
x.domain(d3.extent(data, function(d) { return d.date; }));
```
=> update temperature range for mapping temperature to px on y-axis)     
```javascript
y.domain([
    d3.min(cities, function(c) { return d3.min(c.values, function(d) { return d.temperature; }); }),
    d3.max(cities, function(c) { return d3.max(c.values, function(d) { return d.temperature; }); })
]);```
=> update city names for (func => map city names to color)    
```javascript
z.domain(cities.map(function(c) { return c.id; }))
```
=> create and display x-axis    
```javascript
g.append("g")
    .attr("class", "axis axis--x")
    .attr("transform", "translate(0," + height + ")")
    .call(d3.axisBottom(x));
```
=> create and display y-axis with a label    
```javascript
g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y))
    .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", 6)
      .attr("dy", "0.71em")
      .attr("fill", "#000")
      .text("Temperature, ºF");
```


[Video](https://youtu.be/7tz1dTPp7nc)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/dd839308a263c9423bd8e0957bdb332c)



**Step 5**    
=> update and create g placeholders by binding with data    
```javascript
var city = g.selectAll(".city")
  .data(cities)
  .enter().append("g")
    .attr("class", "city");
```    
=> for each placeholder, create path and draw line on it    
```javascript
city.append("path")
      .attr("class", "line")
      .attr("d", function(d) { return line(d.values); })
      .style("stroke", function(d) { return z(d.id); });
```
=> create a label at the end of each line     
```javascript
city.append("text")
      .datum(function(d) { return {id: d.id, value: d.values[d.values.length - 1]}; })
      .attr("transform", function(d) { return "translate(" + x(d.value.date) + "," + y(d.value.temperature) + ")"; })
      .attr("x", 3)
      .attr("dy", "0.35em")
      .style("font", "10px sans-serif")
      .text(function(d) { return d.id; });
```

[Video](https://youtu.be/j57aoJSsdHQ)
[Practice Demo](http://blockbuilder.org/EmbraceLife/9a73445e8527495bc5cf23b0447cb622)


##### Data format for d3
For simplicity:
* Column names can be strings
* Y,M,D has nothing in between
* Date can be in quote too

[Video](https://www.youtube.com/watch?v=pmQykZXiRcI&feature=youtu.be)    
[Demo](http://blockbuilder.org/EmbraceLife/9a73445e8527495bc5cf23b0447cb622)


##### d3 workflow  
* svg, g
* data extraction by row and by column
* scale-map: x, y, color
* draw: x-y-axis, lines, labels

[Video](https://youtu.be/8bJ85ig-C1k)    
[my-workflow-template](http://blockbuilder.org/EmbraceLife/d80d44aaef08328aee2fd80819fd62ac)


----
### Multi-line Chart Practices

#### 1-stock-return line chart
* no missing data
```html   

<!DOCTYPE html>
<meta charset="utf-8">
<style>

.axis--x path {
  display: none;
}

.line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

</style>

<svg width="960" height="500"></svg>

<script src="//d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg"),
    margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = svg.attr("width") - margin.left - margin.right,
    height = svg.attr("height") - margin.top - margin.bottom,
    g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")");


var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime().range([0, width]),
    y = d3.scaleLinear().range([height, 0]),
    z = d3.scaleOrdinal(d3.schemeCategory10);

var line = d3.line()
    .curve(d3.curveBasis)
    .x(function(d) { return x(d.date); })
    .y(function(d) { return y(d.return); });



function type(d, _, columns) {
  d.Date = parseTime(+d.Date);
//   i = 1 to skip date, c = columns[i] for +d[c]
  for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;
}


d3.csv("data.csv", type,  function(error, data) {
  if (error) throw error;  

  var returns = data.columns.slice(data.columns.length-1).map(function(id) {
    return {
      id: "hkws",
      values: data.map(function(d) {
        return {date: d.Date, return: d.return};
      })
    };
  });

  x.domain(d3.extent(returns[0].values, function(d) { return d.date; }));

  y.domain(
    d3.extent(returns[0].values, function(d) { return d.return;})
  );

  g.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));

  g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y))
    .append("text")
	  .attr("x",20)
      .attr("y", 6)
      .attr("dy", "0.71em")
  	  .attr("text-anchor", "start")
      .attr("fill", "#000")
      .text("return, 1-base");

  g.append("path").datum(returns[0].values)
    .attr("class", "line")
    .attr("d", function(d) { return line(d); })
    .style("stroke", "red" );

  g.append("text")
    .datum(returns[0].values)
    .attr("transform", function(d){return "translate(" + x(d[returns[0].values.length - 1].date) + "," + y(d[returns[0].values.length - 1].return) + ")";})
    .attr("x", 3)
    .attr("dy", "0.35em")
    .style("font", "10px sans-serif")
    .text(function(d) { return returns[0].id; });

});
</script>

```
[video: No need to use .data, but good to use .datum to bind column dataset](https://youtu.be/DKy2ClZWTDU)
[Practice Demo](http://blockbuilder.org/EmbraceLife/3c6ddf06851e61f9a915c5bc081c0c8e)



#### 3-stock-return data => multi-line chart

=> Following code is a cope, only change is data file
```html
<!DOCTYPE html>
<meta charset="utf-8">
<style>

.axis--x path {
  display: none;
}

.line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

</style>

<svg width="960" height="500"></svg>

<script src="//d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg"),
    margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = svg.attr("width") - margin.left - margin.right,
    height = svg.attr("height") - margin.top - margin.bottom,
    g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")");


var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime().range([0, width]),
    y = d3.scaleLinear().range([height, 0]),
    z = d3.scaleOrdinal(d3.schemeCategory10);

var line = d3.line()
    .curve(d3.curveBasis)
    .x(function(d) { return x(d.date); })
    .y(function(d) { return y(d.return); });

function type(d, _, columns) {
  d.date = parseTime(+d.date);
//   i = 1 to skip date, c = columns[i] for +d[c]
  for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;  
}


d3.csv("data.csv", type,  function(error, data) {
  if (error) throw error;  

  var returns = data.columns.slice(1).map(function(id) {
    return {
      id: id,
      values: data.map(function(d) {
        return {date: d.date, return: d[id]};
      })
    };
  });

  x.domain(d3.extent(returns[0].values, function(d) { return d.date; }));

  y.domain(
    [d3.min(returns, function(r){return d3.min(r.values, function(p){return p.return;});}),
    d3.max(returns, function(r){return d3.max(r.values, function(p){return p.return;});})]
  );

   z.domain(returns.map(function(c) { return c.id; }));

  g.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));

  g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y))
    .append("text")
			.attr("x",20)
      .attr("y", 6)
      .attr("dy", "0.71em")
  		.attr("text-anchor", "start")
      .attr("fill", "#000")
      .text("return, 1-base");

  var rr = g.selectAll(".return")
    .data(returns)
    .enter().append("g")
      .attr("class", ".return");

  rr.append("path")
      .attr("class", "line")
      .attr("d", function(d) { return line(d.values); })
      .style("stroke", function(d){return z(d.id)} );

  rr.append("text")
      .datum(function(d) { return {id: d.id, value: d.values[d.values.length - 1]}; })
      .attr("transform", function(d) { return "translate(" + x(d.value.date) + "," + y(d.value.return) + ")"; })
      .attr("x", 3)
      .attr("dy", "0.35em")
      .style("font", "10px sans-serif")
      .text(function(d) { return d.id; });
});


</script>

```

=> structure of data file: about missing dates and values, NA
* contains no NA
* there are missing dates along with missing values
* dataset is created by only inner merge among three stocks return rates
* **path-line will take on those missing dates and smooth out the missing values** on graph    
[video](https://youtu.be/ihTUo3cmozY)     

[Practice Demo](http://blockbuilder.org/EmbraceLife/04c7747f4f664d3cff48e0c730b417ae)



#### 3-stock-return data => multi-line chart
```html
<!DOCTYPE html>
<meta charset="utf-8">
<style>

.axis--x path {
  display: none;
}

.line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

</style>

<svg width="960" height="500"></svg>

<script src="//d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg"),
    margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = svg.attr("width") - margin.left - margin.right,
    height = svg.attr("height") - margin.top - margin.bottom,
    g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")");


var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime().range([0, width]),
    y = d3.scaleLinear().range([height, 0]),
    z = d3.scaleOrdinal(d3.schemeCategory10);

// .defined() remove all NaN or null
var line = d3.line()
    .curve(d3.curveBasis)
	.defined(function(d){return d})
    .x(function(d) { return x(d.date); })
    .y(function(d) {  return y(d.return); });



function type(d, _, columns) {
  d.date = parseTime(+d.date);
  for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;  
}

d3.csv("data.csv", type,  function(error, data) {
  if (error) throw error;  

  // NaN must be dealt as string
  var returns = data.columns.slice(1).map(function(id) {
    return {
      id: id,
      values: data.map(function(d) {
        if(d[id]+"" === "NaN") {
          return null;
        } else {
        return {date: d.date, return: d[id]};
        }
      })
    };
  });

  x.domain(d3.extent(returns[2].values, function(d) { return d.date; }));

// null is easier than NaN to handle
  y.domain(
    [d3.min(returns, function(r){return d3.min(r.values, function(p){ if(p !== null) return p.return;});}),
    d3.max(returns, function(r){return d3.max(r.values, function(p){if(p !== null) return p.return;});})]
  );

   z.domain(returns.map(function(c) { return c.id; }));

  g.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));

  g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y))
    .append("text")
			.attr("x",20)
      .attr("y", 6)
      .attr("dy", "0.71em")
  		.attr("text-anchor", "start")
      .attr("fill", "#000")
      .text("return, 1-base");

var rr = g.selectAll(".return")
    .data(returns)
    .enter().append("g")
      .attr("class", ".return");



var c =  rr.append("path")
      .attr("class", "line")
      .attr("d", function(d) { return line(d.values);})
      .style("stroke", function(d){return z(d.id)} );



  rr.append("text")
      .datum(function(d) { return {id: d.id, value: d.values[d.values.length - 4]}; })
      .attr("transform", function(d) { return "translate(" + x(d.value.date) + "," + y(d.value.return) + ")"; })
      .attr("x", 3)
      .attr("dy", "0.35em")
      .style("font", "10px sans-serif")
      .text(function(d) { return d.id; });
});


</script>

```

=> new struture of dataset
- 3 df merged fully, no date is missing
- but many NA created

=> path-line now will break and showing the empty spaces    
[video](https://youtu.be/Kqv7Ix1bHBs)    

=> NA of data.file read as NaN through d3.js     
[video](https://youtu.be/Xf3oZvBW8hQ)

=> Convert NaN to null, easier to handle     
[video](https://youtu.be/DSImln7Hekk)     

=> null is easier to handle       
[video](https://youtu.be/et27mSllXEM)     

=> path-line func use .defined() to reject null in the first place without applying .x(), .y()
[video](https://youtu.be/F5fmCJJS7KM)      

[Practice Demo](http://blockbuilder.org/EmbraceLife/c85ff2725cd17ca16371ae58689b9b15)


#### 3-stock-return data => Multi-line chart
* inner-merged data => path-line smooth on date and values
* union-merged data => path-line leave all the NA as spaces
* union-merged with na.locf data => path-line plot straight lines for spaces above
* switch data file from "data.csv" to "data_filled.csv"     
[video](https://youtu.be/8-GIzELqOak )     


##### Notes
* How to parse dateformat from data.file
* NaN must be dealt as string
* null is removed by d3.line().defined()

[Video](https://youtu.be/qJFme9KxtzQ)
[Practice Demo](http://blockbuilder.org/EmbraceLife/c85ff2725cd17ca16371ae58689b9b15)



----

## BarChart

### CandleBar chart

#### a basic candlebar chart
```html
<!DOCTYPE html>
<meta charset="utf-8">
<style>

.axis--x path {
  display: none;
}

.line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

</style>

<svg width="960" height="500"></svg>

<script src="//d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg");

var  
    margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = svg.attr("width") - margin.left - margin.right,
    height = svg.attr("height") - margin.top - margin.bottom;

var  
    g = svg.append("g")
				.attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime().rangeRound([0, width]),

    y = d3.scaleLinear().range([height, 0]);

function type(d, _, columns) {

  d.Date = parseTime(+d.Date);

  for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;  
}


d3.csv("data.csv", type,  function(error, data) {
  if (error) throw error;  

    x.domain(d3.extent(data, function(d){return d.Date;}));

  y.domain(
    [d3.min(data.map(function(d){return d.Low;})),
    d3.max(data.map(function(d){return d.High;}))]
  );

  g.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));

  g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y))
    .append("text")
			.attr("x",20)
      .attr("y", 6)
      .attr("dy", "0.71em")
  		.attr("text-anchor", "start")
      .attr("fill", "#000")
      .text("up-red, down-green");


  var barWidth = width/data.length;

  var candlebar = g.selectAll(".bar")
    .data(data)
    .enter().append("g")
      .attr("class", ".bar")
  		.attr("transform", function(d, i) { return "translate(" + i * barWidth + ",0)"; });
  ;

    candlebar.append("line")
			 .attr("x1", barWidth/2)
			.attr("x2", barWidth/2)
			.attr("y1", function(d){ return y(d.High);})
			.attr("y2", function(d){ return y(d.Low);})
			.attr("stroke-width", 0.01)
			.attr("stroke", "gray");


  candlebar.append("rect")
            .attr("y", function(d) {
    					if (d.Open > d.Close) {
                          return y(d.Open)
                        } else {
	                        return y(d.Close);   
                        }})

            .attr("height", function(d) {
    					if (d.Open > d.Close) {
                          return (height - y(d.Open)) - (height - y(d.Close));
                        } else {
                          if (d.Open < d.Close) {
                          return (height - y(d.Close)) - (height - y(d.Open));
                        }}})

			.attr("fill", function(d){
					if (d.Open > d.Close) {
                        return "green" ;
            } else {
                    if (d.Open < d.Close) {
                        return "red" ;
            }}})

            .attr("width", barWidth);

});


</script>

```

=> x-scale-map: use scaleTime not scaleBand     
[Video](https://youtu.be/0BYPUT7KPZQ)   

=> g->bar(transform-translate x position)->rect & line     
- rect fill color => d.Close vs d.Open    
[video](https://youtu.be/Z4zQ40tq1-4)    

=> row-data => create bars and line-stick    
[video](https://youtu.be/RWncr_E-Ag0)


[Demo](http://blockbuilder.org/EmbraceLife/77a920a331c0ed20adfe2bba6f4b28aa)





#### Multi-axis, return line, a candlebar chart

```html
<!DOCTYPE html>
<meta charset="utf-8">
<style>

.axis--x path {
  display: none;
}

.line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

</style>

<svg width="960" height="500"></svg>

<script src="//d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg");  

var  
    margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = svg.attr("width") - margin.left - margin.right,
    height = svg.attr("height") - margin.top - margin.bottom;

var  
    g = svg.append("g")
				.attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime().rangeRound([0, width]),

    y = d3.scaleLinear().range([height, 0]);

    y_return = d3.scaleLinear().range([height, 0]);

var line = d3.line()
				.curve(d3.curveBasis)
                .x(function(d) { return x(d.Date); })
                .y(function(d) {  return y_return(d.return); });

function type(d, _, columns) {

  d.Date = parseTime(+d.Date);

  for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;  
}


d3.csv("data.csv", type,  function(error, data) {
  if (error) throw error;  

		x.domain(d3.extent(data, function(d){return d.Date;}));

    y_return.domain(d3.extent(data, function(d){return d.return;}));

  y.domain(
    [d3.min(data.map(function(d){return d.Low;})),
    d3.max(data.map(function(d){return d.High;}))]
  );

  g.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));


  g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y_return))
    .append("text")
	   .attr("x",20)
      .attr("y", 6)
      .attr("dy", "0.71em")
  	   .attr("text-anchor", "start")
      .attr("fill", "#000")
      .text("up-red, down-green");


  var barWidth = width/data.length;

  var candlebar = g.selectAll(".bar")
    .data(data)
    .enter().append("g")
      .attr("class", ".bar")
  		.attr("transform", function(d, i) { return "translate(" + i * barWidth + ",0)"; });
  ;

    candlebar.append("line")
  				  .attr("x1", barWidth/2)
    				.attr("x2", barWidth/2)
    				.attr("y1", function(d){ return y(d.High);})
     				.attr("y2", function(d){ return y(d.Low);})
    				.attr("stroke-width", 0.01)
  					.attr("stroke", "gray");


  candlebar.append("rect")
            .attr("y", function(d) {
    					if (d.Open > d.Close) {
                          return y(d.Open)
                        } else {
	                        return y(d.Close);   
                        }})

            .attr("height", function(d) {
    				    if (d.Open > d.Close) {
                          return (height - y(d.Open)) - (height - y(d.Close));
                        } else {
                          if (d.Open < d.Close) {
                          return (height - y(d.Close)) - (height - y(d.Open));
                        }}})

  			.attr("fill", function(d){
    					if (d.Open > d.Close) {
                          return "green" ;
                        } else {
                          if (d.Open < d.Close) {
                          return "red" ;
                        }}})

            .attr("width", barWidth);



  var col_return = data.map(function(d){
    return {
        Date: d.Date,
        return: d.return
  }})

  var c =  g.append("path")
  		.datum(col_return)
      .attr("class", "line")
      .attr("d", function(d) { return line(d);})
      .style("stroke", "pink");

});


</script>

```


=> price & ror => 2 y-axis, display only ror    
[video](https://youtu.be/sbpwhaFXN0A)

=> async between candlebar and return line    
[video](https://youtu.be/KRPt-i96jbs)

[Demo](http://blockbuilder.org/EmbraceLife/22dfe256e8d9400c2dc8c4a5e39da695)





#### Solution to async between candlebar and return-line

```html
<!DOCTYPE html>
<meta charset="utf-8">
<style>

.axis--x path {
  display: none;
}

.line {
  fill: none;
  stroke: steelblue;
  stroke-width: 1.5px;
}

</style>

<svg width="960" height="500"></svg>

<script src="//d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg");  

var  
    margin = {top: 20, right: 80, bottom: 30, left: 50},
    width = svg.attr("width") - margin.left - margin.right,
    height = svg.attr("height") - margin.top - margin.bottom;

var  
    g = svg.append("g")
				.attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime().rangeRound([0, width]),

    y = d3.scaleLinear().range([height, 0]);

    y_return = d3.scaleLinear().range([height, 0]);

var line = d3.line()
			.curve(d3.curveBasis)
            .x(function(d) { return x(d.Date); })
            .y(function(d) {  return y_return(d.return); });

function type(d, _, columns) {

  d.Date = parseTime(+d.Date);

  for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;  
}


d3.csv("data_filled.csv", type,  function(error, data) {
  if (error) throw error;  

  x.domain(d3.extent(data, function(d){return d.Date;}));

  y_return.domain(d3.extent(data, function(d){return d.return;}));

  y.domain(
    [d3.min(data.map(function(d){return d.Low;})),
    d3.max(data.map(function(d){return d.High;}))]
  );

  g.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x));

var rightAxis = g.append("g")
      .attr("class", "axis axis--y")
      .attr("transform", "translate("+width+","+0+")")
      .call(d3.axisRight(y_return))

	rightAxis
    	.append("text")
  		.attr("x",-10)
      .attr("y", 6)
      .attr("dy", "0.71em")
  	  .attr("text-anchor", "end")
      .attr("fill", "#000")
      .text("ROR");

  rightAxis
  		.append("rect")
  		.attr("x", -30)
  		.attr("y", 20)
  		.attr("width", 15)
  		.attr("height", 5)
  		.attr("fill", "steelblue")

var leftAxis = g.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y))

// legend price
leftAxis
    .append("text")
			.attr("x",10)
      .attr("y", 6)
      .attr("dy", "0.71em")
  		.attr("text-anchor", "start")
      .attr("fill", "#000")
      .text("Price");

//   legend red
leftAxis
    .append("rect")
			.attr("x",10)
      .attr("y", 26)
      .attr("width", 15)
  		.attr("height", 5)
      .attr("fill", "red")
leftAxis
		.append("text")
			.attr("x", 30)
			.attr("y", 36)
			.attr("dy", "-0.45em")
			.attr("stroke", "red")
			.attr("text-anchor", "start")
      .text("up");

//  legend green
leftAxis
    .append("rect")
			.attr("x",10)
      .attr("y", 36)
      .attr("width", 15)
  		.attr("height", 5)
      .attr("fill", "green")
leftAxis
		.append("text")
			.attr("x", 30)
			.attr("y", 46)
			.attr("dy", "-0.45em")
			.attr("stroke", "green")
			.attr("text-anchor", "start")
      .text("down");  

  var barWidth = width/data.length;

  var candlebar = g.selectAll(".bar")
    .data(data)
    .enter().append("g")
      .attr("class", ".bar")
  		.attr("transform", function(d, i) { return "translate(" + i * barWidth + ",0)"; });
  ;

    candlebar.append("line")
  				  .attr("x1", barWidth/2)
    				.attr("x2", barWidth/2)
    				.attr("y1", function(d){ return y(d.High);})
     				.attr("y2", function(d){ return y(d.Low);})
    				.attr("stroke-width", 0.01)
  					.attr("stroke", "gray");


  candlebar.append("rect")
            .attr("y", function(d) {
    					if (d.Open > d.Close) {
                          return y(d.Open)
                        } else {
	                        return y(d.Close);   
                        }})

            .attr("height", function(d) {
    				    if (d.Open > d.Close) {
                          return (height - y(d.Open)) - (height - y(d.Close));
                        } else {
                          if (d.Open < d.Close) {
                          return (height - y(d.Close)) - (height - y(d.Open));
                        }}})

  		   .attr("fill", function(d){
    										if (d.Open > d.Close) {
                          return "green" ;
                        } else {
                          if (d.Open < d.Close) {
                          return "red" ;
                        }}})
						.attr("opacity", 0.2)
            .attr("width", barWidth);

  var col_return = data.map(function(d){
    return {

        Date: d.Date,
        return: d.return

  }})

  g.append("path")
  		.datum(col_return)
      .attr("class", "line")
      .attr("d", function(d) { return line(d);})
      .style("stroke", "steelblue");

});


</script>

```

- rect and line (barChart) will ignore missing data (even though there is No NA, therefore, not included in data.file, see data.csv)
- path-line will not ignore missing data (even though there is No NA, therefore, not included in data.file, see data_filled.csv)
- provide data_filled.csv (missing data is filled with previous data and date)    
[video](https://youtu.be/VVA11yeTA3Y)      
- 2-y-axis created with .axisRight()    
[video](https://youtu.be/MVYSLBoYiuI)     
- legends on both sides => rects and texts     
[video](https://youtu.be/RTO5B8Xv958)     
- fade candle-bar chart => opacity attr for rect and line   

[Demo](http://blockbuilder.org/EmbraceLife/acfe4bad38dc546e6917b914e5933016)


----

### Brush and Zoom     

#### mbostock brush and zoom example

```html
<!DOCTYPE html>
<meta charset="utf-8">
<style>

.area {
  fill: steelblue;
  clip-path: url(#clip);
}

.zoom {
  cursor: move;
  fill: none;
  pointer-events: all;
}

/*-------- step1: svg canvas, g for inner canvas ----   */

</style>
<svg width="960" height="500"></svg>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg"),
    margin = {top: 20, right: 20, bottom: 110, left: 40},
    margin2 = {top: 430, right: 20, bottom: 30, left: 40},
    width = +svg.attr("width") - margin.left - margin.right,
    height = +svg.attr("height") - margin.top - margin.bottom,
    height2 = +svg.attr("height") - margin2.top - margin2.bottom;


svg.append("defs").append("clipPath")
    .attr("id", "clip")
  .append("rect")
    .attr("width", width)
    .attr("height", height);


var focus = svg.append("g")
    .attr("class", "focus")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var context = svg.append("g")
    .attr("class", "context")
    .attr("transform", "translate(" + margin2.left + "," + margin2.top + ")");





  // ---- step2: funcs: x-y-axis, area, brush, zoom -------


var parseDate = d3.timeParse("%b %Y");


var x = d3.scaleTime().range([0, width]),
    x2 = d3.scaleTime().range([0, width]),
    y = d3.scaleLinear().range([height, 0]),
    y2 = d3.scaleLinear().range([height2, 0]);


var xAxis = d3.axisBottom(x),
    xAxis2 = d3.axisBottom(x2),
    yAxis = d3.axisLeft(y);


var brush = d3.brushX()

    .extent([[0, 0], [width, height2]])
    .on("brush end", brushed);

var zoom = d3.zoom()

    .scaleExtent([1, Infinity])

    .translateExtent([[0, 0], [width, height]])

    .extent([[0, 0], [width, height]])
    .on("zoom", zoomed);


var area = d3.area()
    .curve(d3.curveMonotoneX)
    .x(function(d) { return x(d.date); })
    .y0(height)
    .y1(function(d) { return y(d.price); });

var area2 = d3.area()
    .curve(d3.curveMonotoneX)
    .x(function(d) { return x2(d.date); })
    .y0(height2)
    .y1(function(d) { return y2(d.price); });



// ---- step3: update x-y.domain values; draw zoom box area, x-y-axis, draw brush box area, x-axis; draw zoom box and brush box behaviour


d3.csv("sp500.csv", type, function(error, data) {
  if (error) throw error;

  x.domain(d3.extent(data, function(d) { return d.date; }));
  y.domain([0, d3.max(data, function(d) { return d.price; })]);
  x2.domain(x.domain());
  y2.domain(y.domain());



focus.append("path")
      .datum(data)
      .attr("class", "area")
      .attr("d", area);

  focus.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(xAxis);

  focus.append("g")
      .attr("class", "axis axis--y")
      .call(yAxis);


  context.append("path")
      .datum(data)
      .attr("class", "area")
      .attr("d", area2);

  context.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height2 + ")")
      .call(xAxis2);

  context.append("g")
      .attr("class", "brush")
      .call(brush)
      .call(brush.move, x.range());

  svg.append("rect")
      .attr("class", "zoom")
      .attr("width", width)
      .attr("height", height)
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")")
      .call(zoom);



});


// ---- step 4: define zoom box and brush box behaviour  


function brushed() {
  if (d3.event.sourceEvent && d3.event.sourceEvent.type === "zoom") return;

  var s = d3.event.selection || x2.range();

  x.domain(s.map(x2.invert, x2));


  focus.select(".area").attr("d", area);

  focus.select(".axis--x").call(xAxis);


  svg.select(".zoom")
    	.call(zoom.transform, d3.zoomIdentity
      .scale(width / (s[1] - s[0]))
      .translate(-s[0], 0))
  ;
}

function zoomed() {
  if (d3.event.sourceEvent && d3.event.sourceEvent.type === "brush") return;

  var t = d3.event.transform;

  x.domain(t.rescaleX(x2).domain());
  focus.select(".area").attr("d", area);
  focus.select(".axis--x").call(xAxis);
  context.select(".brush").call(brush.move, x.range().map(t.invertX, t));
}

function type(d) {
  d.date = parseDate(d.date);
  d.price = +d.price;
  return d;
}

</script>

```


Set styles:
- .area {clip-path: url(#clip)}
[video: prevent things display](https://youtu.be/rbkN0hnodEs)
- .zoom {cursor: move; pointer-events: all;}
[video: change a sign on movable object](https://youtu.be/jsEMpHbGy8Q)   
[video: mouse-event control](https://youtu.be/-xY-ZNjEpZk)



Define variables:
- set height and width for 2 view panels  
[video](https://youtu.be/dlxRFf5tmiI )  

Create a date-format function:    
- Nov 2016 => .timeParse("%d %Y")    
- 2 panels => 2 heights + 2 .range([height, 0]) => 2 g with own transform-translate origin     
[video](https://youtu.be/pZHTpAHqJ48)

=> create a brush func
```javascript
var brush = d3.brushX()

    .extent([[0, 0], [width, height2]])
    .on("brush end", brushed);

```
- make a brush generator => set size => where action begin     
[video](https://www.youtube.com/watch?v=EyW7uND_t44)   

=> create a zoom func
```javascript
var zoom = d3.zoom()

    .scaleExtent([1, Infinity])

    .translateExtent([[0, 0], [width, height]])

    .extent([[0, 0], [width, height]])
    .on("zoom", zoomed);
```
- make a zoom generator => set scale range: 1 to infinite => set scale-screen size => set viewport size => where action begin     
[video](https://youtu.be/HV_K5o1tMY4)   

=> Create a area function:   
```javascript
var area = d3.area()
    .curve(d3.curveMonotoneX)
    .x(function(d) { return x(d.date); })
    .y0(height)
    .y1(function(d) { return y(d.price); });
```
- make a area generator => set curve style => set x0 value by function, x1 as null => set y0 at bottom of viewport => set y1 as area topEdge     
[video](https://youtu.be/SPTesThh0eE)

=> Create A clip-path Rect here:
```javascript
svg.append("defs").append("clipPath")
    .attr("id", "clip")
  .append("rect")
    .attr("width", width)
    .attr("height", height);
```
- svg => defs:render,reuse elements => clip-path: not display portion of elements => a visual element like rect     
[video](https://youtu.be/XfVMkZYHkeA)  


=> draw areas, x-y-axis
```javascript
focus.append("path")
      .datum(data)
      .attr("class", "area")
      .attr("d", area);

  focus.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(xAxis);

  focus.append("g")
      .attr("class", "axis axis--y")
      .call(yAxis);

  context.append("path")
      .datum(data)
      .attr("class", "area")
      .attr("d", area2);

  context.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height2 + ")")
      .call(xAxis2);

```
- g placeholder => path => datum(data) => attr("d", area);
- datum vs data => enter, exit or not     
[video](https://youtu.be/HoZYskbULYM)     

=> Draw with path or with g:
- path-datum-attr-d-area
- g-call(xAxis)    
[video](https://youtu.be/Qdt4NT0od8g)     


=> draw brush: call => brush.move
```javascript
context.append("g")
    .attr("class", "brush")
    .call(brush)
    // how far can brush move?
    .call(brush.move, x.range());
```  
[video](https://youtu.be/kxolPUl4IEA)

=> Set the range of gray movable control-box on context viewbox
```javascript
.call(brush.move, x.range());
```
[video](https://youtu.be/3vt3Lf7SaUk)

=> logic flow from drawing focus-brush-box to understand brush-zoom-funcs
```javascript
context.append("g")
    .attr("class", "brush")
    .call(brush)
    .call(brush.move, x.range());

svg.append("rect")
    .attr("class", "zoom")
    .attr("width", width)
    .attr("height", height)
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")")
    .call(zoom);

    var brush = d3.brushX()

        .extent([[0, 0], [width, height2]])
        .on("brush end", brushed);

    var zoom = d3.zoom()

        .scaleExtent([1, Infinity])

        .translateExtent([[0, 0], [width, height]])

        .extent([[0, 0], [width, height]])
        .on("zoom", zoomed);    
```
[video](uploading)


##### Brushed Function:
```javascript
function brushed() {
  if (d3.event.sourceEvent && d3.event.sourceEvent.type === "zoom") return;
  // 1. ignore brush-by-zoom

// 2. s is brush range px selection  
  var s = d3.event.selection || x2.range();

// 3. convert s from px to date
  x.domain(s.map(x2.invert, x2));  

  focus.select(".area").attr("d", area);
  focus.select(".axis--x").call(xAxis);

//   control zoom viewbox transformation k, x, y
  svg.select(".zoom")
    	.call(zoom.transform, d3.zoomIdentity
      .scale(width / (s[1] - s[0]))
      .translate(-s[0], 0));}
```
=> 1. Brushed-event-sourceEvent: why ignore brush-by-zoom???    
[video](https://youtu.be/PJ7Y7PfTL6g)

=> 2. s is a range of px on x-axis on context box selected by brush
[video](https://youtu.be/XY1HCaTTyvs)    

=> 3. convert px range to date range, and set it to x.domain()
```javascript
x.domain(s.map(x2.invert, x2));  
```
[video](https://youtu.be/GV61bQtwfHQ)   

=> 4. update to draw area and x-axis; then update k, x, y to scale up-down and move focus viewbox left-right
```javascript
svg.select(".zoom")
      .call(zoom.transform, d3.zoomIdentity // default 1,0,0
    .scale(width / (s[1] - s[0])) // set k
    .translate(-s[0], 0)); // set x, y
```     
[video](https://youtu.be/-KJh4ZG5tl8)

=> 5. Brushed: zoom rect move left & clip-path's power    
[video](https://youtu.be/KBPhIy7fDz8)

=> conversion between px and dates and between k-x-y and dates
```javascript
// from bushed side: convert px range to date range
var s = d3.event.selection || x2.range();
x.domain(s.map(x2.invert, x2));

// from zoomed side; convert from k-x-y to dates range
var t = d3.event.transform;
x.domain(t.rescaleX(x2).domain());
```
[video: px for context box and k-x-y for focus box to convert to date range](https://youtu.be/q4mKNSubfQg)

=> sync brush-box change with zoom-box change     
```javascript  
// inside brush-box change, use px change to update k,x,y, to transform zoom box
svg.select(".zoom")
    .call(zoom.transform, d3.zoomIdentity
    .scale(width / (s[1] - s[0]))
    .translate(-s[0], 0));}

// inside zoom-box change, use k,x,y change to update px
context.select(".brush").call(brush.move, x.range().map(t.invertX, t));

// convert k-x-y to px range
x.range().map(t.invertX, t)
```
[video: sync brush-px change to zoom-kxy change and vice verse](https://youtu.be/h5Hp9tCUKa8)





##### Zoomed Function:
```javascript
function zoomed() {
  if (d3.event.sourceEvent && d3.event.sourceEvent.type === "brush") return;
  // t capture changing k,x,y
  var t = d3.event.transform;
  x.domain(t.rescaleX(x2).domain());

  focus.select(".area").attr("d", area);
  focus.select(".axis--x").call(xAxis);
  // set brush movement [px, px]
  context.select(".brush").call(brush.move, x.range().map(t.invertX, t));
}
```
- Zoomed: update-x.domain-px-date    
[video](https://youtu.be/yUXsqmwU42s)
- Zoomed: update area and xAxis, and update brushed area range     
[video](https://youtu.be/yuFs9Z50QJQ)    

Brush and Zoom workflow:
1. create svg canvas, svg-clip-path, margin-width-height
* create funcs: dateformat func, 2x-scale funcs, 2y-scale funcs, 2x-axis func, y-axis func, 2area-func, brush func, zoom func
* load data: load data func, type func
* update and draw: update x-domain, y-domain; draw zoom area, zoom x-axis, zoom y-axis; draw brush area, brush-x-axis; draw zoom box, brush box
* zoomed and brushed funcs for control zoom box and brush box behaviour     
[video](https://youtu.be/K0iG0Vk516I)

[Demo](http://blockbuilder.org/EmbraceLife/7efd1f9031beecb5252e57e944e1a440)
[Cleaner Demo](http://bl.ocks.org/EmbraceLife/21cc0f29827dacf30a658ef7763c19e7)

----


##### brush-zoom-candle-return

[demo](http://bl.ocks.org/EmbraceLife/d66394e7abd5ee805eeb82284db3106f)

### Hover to check

[Demo](http://blockbuilder.org/EmbraceLife/9dc7507eab115461527848925270e81a)   

### stock example by [arnauddri/d3-stock](https://github.com/arnauddri/d3-stock)  
How to Update to version 4
- update v3 to v4
```html
<script src='http://d3js.org/d3.v4.min.js' charset="utf-8"></script>
```
- Check error on console view     
- Click on the error link to see the problematic code    
[video](https://youtu.be/GhlrzcDc014)  




[Demo v3](http://blockbuilder.org/EmbraceLife/8d5f72013244fb92fc4fe03279a14ebf)
[Demo v4](http://blockbuilder.org/EmbraceLife/14ba2eadaeba1767591e96102a7471a2)


### Project
#### Questions
- M2 4 times in 10 years from today backward
- HS300 performance during same period   
- Stocks up 4 times during same period
- stocks with less volatility
- stocks with huge volatility

#### Performance
- Zoom in and hover to display names
