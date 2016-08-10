# id3-by-examples
**Lessons learnt**    
1. the better I understand previous work, the more confident I am to tackle new problems
2. If there is no need to read or watch my work again and again, then I should not make them in the first place
3. notes and videos as specific and short as possible



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

- `d3.scaleTime().range([0, width])` => map date to px on x-axis => update px range     
- `d3.scaleLinear().range([height, 0])` => map temperature to px on y-axis, update px range    
- `d3.scaleOrdinal(d3.schemeCategory10)` => map city names to color, give 20 default colors         
- `d3.line().curve(d3.curveBasis).x(function(d) { return x(d.date); }).y(function(d) { return y(d.temperature); })` => tranform data points into (x, y) px position for drawing lines    

[Video](https://youtu.be/uiwh0EJPKr8)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/c675ec2a11d547ac62ab57c04f7a4e02)  


**Step 3 -> Load data and Process each row of data**   
- `function type(d, _, columns) {}` => row func to make use of column names
- `d3.timeParse("%Y%m%d")` => Format date for data file        
- `for (var i = 1, n = columns.length, c; i < n; ++i) d[c = columns[i]] = +d[c];
  return d;` => access each column's value of each row, except Date/first column
- `d3.tsv("data.tsv", type, function(error, data) {}` => load data file and preprocess data
- `var cities = data.columns.slice(1).map(function(id) {return {id: id, values: data.map(function(d) {return {date: d.date, temperature: d[id]};})` => reorganise dataset by columns


[Video1](https://youtu.be/NgjhKnoWGZg)    
[Video2](https://youtu.be/AnSUbBXXvnM)   
[Practice Demo](http://blockbuilder.org/EmbraceLife/3f7287859b3c582cb2a451a42a6faf58)


**Step 4 -> update domain-range for scale-map functions above**   
`x.domain(d3.extent(data, function(d) { return d.date; }));` => update date range for (func => map date to px on x-axis)    
`y.domain([
    d3.min(cities, function(c) { return d3.min(c.values, function(d) { return d.temperature; }); }),
    d3.max(cities, function(c) { return d3.max(c.values, function(d) { return d.temperature; }); })
  ]);` => update temperature range for mapping temperature to px on y-axis)    
`z.domain(cities.map(function(c) { return c.id; }))` => update city names for (func => map city names to color)
- create and display x-axis
- create and display y-axis with a label


[Video](https://youtu.be/7tz1dTPp7nc)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/dd839308a263c9423bd8e0957bdb332c)



**Step 5**
- update and create g placeholders by binding with data      
- for each placeholder, create path and draw line on it    
- create a label at the end of each line     

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

#### 1-stock-return => line chart
* no missing data

[Practice Demo](http://blockbuilder.org/EmbraceLife/3c6ddf06851e61f9a915c5bc081c0c8e)

#### 3-stock-return data => multi-line chart
* there is no values as NA, only inner data among three stocks return rates
* there are missing dates
* path-line will take on those missing dates and smooth out the missing values on graph    
[video](https://youtu.be/ihTUo3cmozY)     

[Practice Demo](http://blockbuilder.org/EmbraceLife/04c7747f4f664d3cff48e0c730b417ae)



#### 3-stock-return data => multi-line chart
* 3 df merged fully, no date is missing, but many NA created for other 2 stocks
* path-line now will break and showing the empty spaces    
[video](https://youtu.be/Kqv7Ix1bHBs)     
- NA of data.file read as NaN through d3.js     
[video](https://youtu.be/Xf3oZvBW8hQ)      
- Convert NaN to null, easier to handle     
[video](https://youtu.be/DSImln7Hekk)     
- null is easier to handle       
[video](https://youtu.be/et27mSllXEM)     
- path-line func use .defined() to reject null in the first place without applying .x(), .y()
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
* How to handle NaN inside data-row-object
* How to handle null data on d3.line().defined()

[Video](https://youtu.be/qJFme9KxtzQ)
[Practice Demo](http://blockbuilder.org/EmbraceLife/c85ff2725cd17ca16371ae58689b9b15)



----

## BarChart

### CandleBar chart

#### a basic candlebar chart
- x-scale-map: use scaleTime not scaleBand  
[Video](https://youtu.be/0BYPUT7KPZQ)   
- g->bar(transform-translate x position)->rect & line    
- rect fill color => d.Close vs d.Open    
[video](https://youtu.be/Z4zQ40tq1-4)    
- row-data => create bars and line-stick
[video](https://youtu.be/RWncr_E-Ag0)


[Demo](http://blockbuilder.org/EmbraceLife/77a920a331c0ed20adfe2bba6f4b28aa)

#### Multi-axis, return line, a candlebar chart
- price & ror => 2 y-axis, display only ror    
[video](https://youtu.be/sbpwhaFXN0A)
- async between candlebar and return line    
[video](https://youtu.be/KRPt-i96jbs)

[Demo](http://blockbuilder.org/EmbraceLife/22dfe256e8d9400c2dc8c4a5e39da695)

#### Solution to async between candlebar and return-line
* rect and line (barChart) will ignore missing data (even though there is No NA, therefore, not included in data.file, see data.csv)
* path-line will not ignore missing data (even though there is No NA, therefore, not included in data.file, see data_filled.csv)
* provide data_filled.csv (missing data is filled with previous data and date)    
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

Set styles:
- .area {clip-path: url(#clip)} ????
- .zoom {cursor: move; pointer-events: all;} ????

Define variables:
- set height and width for 2 view panels  
[video](https://youtu.be/dlxRFf5tmiI )  

Create a date-format function:    
- Nov 2016 => .timeParse("%d %Y")    
- 2 panels => 2 heights + 2 .range([height, 0]) => 2 g with own transform-translate origin     
[video](https://youtu.be/pZHTpAHqJ48)

create a brush func
- make a brush generator => set size => where action begin     
[video](https://www.youtube.com/watch?v=EyW7uND_t44)   

create a zoom func
- make a zoom generator => set scale range: 1 to infinite => set scale-screen size => set viewport size => where action begin     
[video](https://youtu.be/HV_K5o1tMY4)   

Create a area function:   
- make a area generator => set curve style => set x0 value by function, x1 as null => set y0 at bottom of viewport => set y1 as area topEdge     
[video](https://youtu.be/SPTesThh0eE)

Create A clip-path Rect here:
- svg => defs:render,reuse elements => clip-path: not display portion of elements => a visual element like rect     
[video](https://youtu.be/XfVMkZYHkeA)  


draw area with area func defined:
- g placeholder => path => datum(data) => attr("d", area);
- datum vs data => enter, exit or not     
[video](https://youtu.be/HoZYskbULYM)     

Draw with path or with g:
- path-datum-attr-d-area
- g-call(xAxis)    
[video](https://youtu.be/Qdt4NT0od8g)     


draw brush: call => brush.move ????  
```javascript
context.append("g")
    .attr("class", "brush")
    .call(brush)
    // how far can brush move?
    .call(brush.move, x.range());
```  
[video](https://youtu.be/kxolPUl4IEA)


understand brushed and zoomed functions:
- but not sure following code adds anything meaningful
```javascript
.call(brush.move, x.range());
```
[video](https://youtu.be/SFYkLwZWKPc)

Brushed Function:
```javascript
function brushed() {
  if (d3.event.sourceEvent && d3.event.sourceEvent.type === "zoom") return; // ignore brush-by-zoom

// s is brush range px selection  
  var s = d3.event.selection || x2.range();

// convert s from px to date
  x.domain(s.map(x2.invert, x2));  

  focus.select(".area").attr("d", area);
  focus.select(".axis--x").call(xAxis);

//   control zoom viewbox transformation k, x, y
  svg.select(".zoom")
    	.call(zoom.transform, d3.zoomIdentity
      .scale(width / (s[1] - s[0]))
      .translate(-s[0], 0));}
```
- Brushed-event-sourceEvent: why ignore brush-by-zoom???    
[video](https://youtu.be/PJ7Y7PfTL6g)
- Brushed-update-x.domain: change brush area => record the change of px range of brush     
[video](https://youtu.be/XY1HCaTTyvs)    
- Brushed-update-x.domain: convert px range to date range to update x.domain()    
[video](https://youtu.be/GV61bQtwfHQ)    
- Brushed-control-tranform-k,x,y for zoom view box    
[video](https://youtu.be/-KJh4ZG5tl8)
- Brushed: zoom rect move left & clip-path's power    
[video](https://youtu.be/KBPhIy7fDz8)

Zoomed Function:
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
##### brush-zoom-candle-return

[demo](http://bl.ocks.org/EmbraceLife/d66394e7abd5ee805eeb82284db3106f)

### Hover to check

[Demo](http://blockbuilder.org/EmbraceLife/9dc7507eab115461527848925270e81a)   

### stock example by [arnauddri/d3-stock](https://github.com/arnauddri/d3-stock)  

[Demo](http://blockbuilder.org/EmbraceLife/8d5f72013244fb92fc4fe03279a14ebf)


### Project
#### Questions
- M2 4 times in 10 years from today backward
- HS300 performance during same period   
- Stocks up 4 times during same period
- stocks with less volatility
- stocks with huge volatility

#### Performance
- Zoom in and hover to display names
