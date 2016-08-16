# id3-by-examples
**Lessons learnt**    
1. the better I understand previous work, the more confident I am to tackle new problems    
2. If there is no need to read or watch my work again and again, then I should not make them in the first place    
3. notes and videos as specific and short as possible     

# **Table of Conent**     

## dc.js examples 


### flight-crossfilter example    

** Step 1 ==> elements structures **    
** Step 2 ==> investigate variables in console **




### Nasdaq 100 index example   

** Step 1 ==> elements structures **    
[Get to know the basic elements layouts](#elements-layouts)    

** Step 2 ==> investigate variables in console **     
[Get to know variables by log them in console](#variable-investigate)     

### variable investigate    
=> Get to know variables by log them in console    
[video: data loaded and processed](https://youtu.be/kUya1Xk_4tw)    
[video: crossfilter() and groupAll()](https://youtu.be/BC1jtPBQZWk)    
[video: crossfilter and groupAll API](https://youtu.be/fLKRsHRxFWU)         
[video: understanding dimension,group,reduce,order,all,top](https://youtu.be/fGd9RYgLxOw)     
[video: all vs top, order vs orderNatural](https://youtu.be/uTAi5F6kphU)     
[video: dimension.group().all() to access content](https://youtu.be/eppiaFcWiKA)      
[video: dimension.group.reduceSum.all-top](https://youtu.be/FVTsm4p9hzU)      
[video: any columns can be used by dimension.group.reduceSum](https://youtu.be/8nq4ZKtzfnk)    
[video: p.columnName and v.columnName for reduce() and order-custom-func](https://youtu.be/HIa-tX7wpi0)    
[video: dimension on category, return category and their counts](uplohttps://youtu.be/ptx3b4Ort7Qading)    
[video: histogram-dimension-percentageChange-key=>unique percentage, change-value=>count](https://youtu.be/1lAc8MyyYgA)     
[video: quarter name and count, sum of volume for all Q1 to Q4](https://youtu.be/pHgQu1DlPsw)     
[video: weekday, numberName, stringName, count](https://youtu.be/PR0rQZv_74U)    
[video: bubbleChart, colorDomain() not sure](https://youtu.be/7OQuRl5Uc2o)     
[video: bubblechart, set domain-range for x,y,r, trial-error for best range](https://youtu.be/hur1-F6aVps)    





### elements layouts    
=> How to get to know all the visual and non-visual elements (the skeleton)?    
[video: container, image, h2, p](https://youtu.be/VD-J9gl9czQ)     
[video: more h2-4, p, unordered list, and a-links](https://youtu.be/3CdXcyrllGo)    
[video: all of them are on immediate level of child from div .container](https://youtu.be/gbw8y21w4fM)    
[video: div rows contains texts, div graphs, reset hidden](https://youtu.be/qwMW-M5cCNA)       
[video: div rows inside -> more text, svg, div](https://youtu.be/pvSZ69Qt2tY)    
[video: div rows inside -> tick lines horizontal and vertical, circle with texts, x-y-axis and labels](https://youtu.be/Hauy4Vf2A9A)    
[video: reset and range selected](https://youtu.be/VbVj3qYpuKY)      
[video: line and area chart](https://youtu.be/iXefhFxHwK0)



## line-bar-brush-mouse-tooltip

### stock price volume brush tooltip      

[`ticks()` calc num of tick lines smartly rather than taking number constant](#ticks-smart)    
[no clip-path transform-translate and width-height as big as possible](#clip-path-no-translate)    
[How to make margin-height-width cleaner?](#margin-clean)    
[source v4](#asc-src)    
[update to version4](#update-to-4)    
[How to use axis.tickSize](#ticksize)    
[How to clean margins, width, height for 3 panels](#margins)    
[How to convert date to string](#date-to-string)    
[How to contrain index](#bisector-left)     
[Index left out by constraint](#left-out)     
[How to mouse around tooltip display](#mouse-tooltip)     
[How to choose display options](#css-display)    
[How to brush to update](#brush-update)     
[How to update by click a date-range-Name, like 3m or 1y](#click-rangeName)     
[How to update the gray selection box](#update-selection-box)     
[The key of code for updating](#key-code-update)       
[How to understand multi-file such as css script etc, exampe](#script-css)     



[Line Charts](#line-charts)        
[Brush and Zoom](#brush-and-zoom)    


----

## Other Basic Skills
[video: How to create a TOC in Markdown](https://youtu.be/S_jGcqajV9o)

----   

### advanced stock example
by [arnauddri/d3-stock](https://github.com/arnauddri/d3-stock)  


### g height width    
=> g can have not only transform-translate and also width and height attributes    
[video](https://youtu.be/hAwRSsViW14)     
[Back](#stock-price-volume-brush-tooltip)    


### ticks smart    
=> calc tick number of lines smartly rather than taking num for sure or constant    
[video](https://youtu.be/NZhmoebRU9I)    
[Back](#stock-price-volume-brush-tooltip)    


### clip path no translate    
=> no clip-path transform-translate and width-height as big as possible    
- purpose: to avoid part of visual elements lose its visibility    

```javascript 
svg.append('defs').append('clipPath')
     .attr('id', 'clip')
//      	 .attr("transform", "translate(" + margin.left + "," + margin.top +")" )
  .append('rect')
    .attr('width', 960) // width
    .attr('height', 500); // height_big
```
[video](https://youtu.be/ggCmpyHo7Zg)    
[Back](#stock-price-volume-brush-tooltip)    



### margin clean    
=> How to make margin-height-width cleaner?    
- svg width and height to be set first     
- margin top, bottom, right, left, one set is enough    
- draw a graph on paper to find out their relationship   
 
[video](https://youtu.be/AMZe1YH14jo)    
```javascript
  var svg = d3.select('body').append('svg')
    .attr('class', 'chart')
    .attr('width', 960)
    .attr('height', 500);
      
  var margin = {top: 20, bottom:20, left:30, right:30}, 
      height_big = (500 - 4*margin.top)/6*4, 
      height_small = (500 - 4*margin.top)/6,
  		width = 960 - margin.left*2;
```
[Back](#stock-price-volume-brush-tooltip)    


#### asc-src
=> script.js has updated to version 4
```javascript
/* global d3, _ */

(function() {
  var margin = {top: 30, right: 20, bottom: 100, left: 50},
    margin2  = {top: 210, right: 20, bottom: 20, left: 50},
    width    = 764 - margin.left - margin.right,
    height   = 483 - margin.top - margin.bottom -60,
    height2  = 283 - margin2.top - margin2.bottom;

  var parseDate = d3.timeParse('%d/%m/%Y'),
    bisectDate = d3.bisector(function(d) { return d.date; }).left;

  var x = d3.scaleTime().range([0, width]),
    x2  = d3.scaleTime().range([0, width]),
    y   = d3.scaleLinear().range([height, 0]),
    y1  = d3.scaleLinear().range([height, 0]),
    y2  = d3.scaleLinear().range([height2, 0]),
    y3  = d3.scaleLinear().range([60, 0]);

  var xAxis = d3.axisBottom(x),
    xAxis2  = d3.axisBottom(x2),
    yAxis   = d3.axisLeft(y);

  var priceLine = d3.line()
  // check out line.curve and curve factor or curves
    .curve(d3.curveMonotoneX)
    .x(function(d) { return x(d.date); })
    .y(function(d) { return y(d.price); });

  var avgLine = d3.line()
    .curve(d3.curveMonotoneX)
    .x(function(d) { return x(d.date); })
    .y(function(d) { return y(d.average); });

  var area2 = d3.area()
    .curve(d3.curveMonotoneX)
    .x(function(d) { return x2(d.date); })
    .y0(height2)
    .y1(function(d) { return y2(d.price); });

  var svg = d3.select('body').append('svg')
    .attr('class', 'chart')
    .attr('width', width + margin.left + margin.right)
    .attr('height', height + margin.top + margin.bottom + 60);

  svg.append('defs').append('clipPath')
     .attr('id', 'clip')
  .append('rect')
    .attr('width', width)
    .attr('height', height);

  var make_y_axis = function () {
    return d3.axisLeft(y)
      .ticks(3);
  };

  var focus = svg.append('g')
    .attr('class', 'focus')
    .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')');

  var barsGroup = svg.append('g')
    .attr('class', 'volume')
    .attr('clip-path', 'url(#clip)') // added clip-path css
    .attr('transform', 'translate(' + margin.left + ',' + (margin.top + 60 + 20 + 150) + ')');

  var context = svg.append('g')
    .attr('class', 'context')
    .attr('transform', 'translate(' + margin2.left + ',' + (margin2.top + 60 + 150) + ')');

  var legend = svg.append('g')
    .attr('class', 'chart__legend')
    .attr('width', width)
    .attr('height', 30)
    .attr('transform', 'translate(' + margin2.left + ', 10)');

  legend.append('text')
    .attr('class', 'chart__symbol')
    .text('NASDAQ: AAPL')

  var rangeSelection =  legend
    .append('g')
    .attr('class', 'chart__range-selection')
    .attr('transform', 'translate(110, 0)');

   d3.csv('aapl.csv', type, function(err, data) {
    var brush = d3.brushX()

    .extent([[0, 0], [width, height2]])
    .on("brush", brushed);
//     console.log(brush.extent()());

    var xRange = d3.extent(data.map(function(d) { return d.date; }));
// console.log(xRange)

    x.domain(xRange);
    y.domain(d3.extent(data.map(function(d) { return d.price; })));
    y3.domain(d3.extent(data.map(function(d) { return d.volume; })));
    x2.domain(x.domain());
    y2.domain(y.domain());

    var min = d3.min(data.map(function(d) { return d.price; }));
    var max = d3.max(data.map(function(d) { return d.price; }));

    var range = legend.append('text')
      .text((new Date(xRange[0])).toDateString() + ' - ' + (new Date(xRange[1]).toDateString()))
      .style('text-anchor', 'end')
      .attr('transform', 'translate(' + width + ', 0)');

    focus.append('g')
        .attr('class', 'y chart__grid')
        .call(make_y_axis()
//         .tickSizeInner(-width)
//         .tickSizeOuter(-width)
         .tickSize(-width)
        .tickFormat(''));


    var averageChart = focus.append('path')
        .datum(data)
        .attr('class', 'chart__line chart__average--focus line')
        .attr('d', avgLine);

    var priceChart = focus.append('path')
        .datum(data)
        .attr('class', 'chart__line chart__price--focus line')
        .attr('d', priceLine);

    focus.append('g')
        .attr('class', 'x axis')
        .attr('transform', 'translate(0 ,' + height + ')')
        .call(xAxis);

    focus.append('g')
        .attr('class', 'y axis')
        .attr('transform', 'translate(12, 0)')
        .call(yAxis);

// volume bars, no x-axis for bars
    var focusGraph = barsGroup.selectAll('rect')
        .data(data)
      .enter().append('rect')
        .attr('class', 'chart__bars')
        .attr('x', function(d, i) { return x(d.date); })
        .attr('y', function(d) { return 155 - y3(d.volume); })
        .attr('width', 1)
        .attr('height', function(d) { return y3(d.volume); });

    var helper = focus.append('g')
      .attr('class', 'chart__helper')
      .style('text-anchor', 'end')
      .attr('transform', 'translate(' + width + ', 0)');

    var helperText = helper.append('text')

    var priceTooltip = focus.append('g')
      .attr('class', 'chart__tooltip--price')
      .append('circle')
      .style('display', 'none') // null to display, none to hide
      .attr('r', 2.5);

    var averageTooltip = focus.append('g')
      .attr('class', 'chart__tooltip--average')
      .append('circle')
      .style('display', 'none')
      .attr('r', 2.5);

    var mouseArea = svg.append('g')
      .attr('class', 'chart__mouse')
      .append('rect')
      .attr('class', 'chart__overlay')
      .attr('width', width)
      .attr('height', height)
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
      .on('mouseover', function() {
        helper.style('display', null);
        priceTooltip.style('display', null);
        averageTooltip.style('display', null);
      })     
      .on('mouseout', function() {
        helper.style('display', 'none');
        priceTooltip.style('display', 'none');
        averageTooltip.style('display', 'none');
      })
      .on('mousemove', mousemove);

    context.append('path')
        .datum(data)
        .attr('class', 'chart__area area')
        .attr('d', area2);

    context.append('g')
        .attr('class', 'x axis chart__axis--context')
        .attr('y', 0)
        .attr('transform', 'translate(0,' + (height2 - 22) + ')')
        .call(xAxis2);

    context.append('g')
        .attr('class', 'x-brush')
        .call(brush)
    .call(brush.move, x2.range())
      .selectAll('rect')
        .attr('y', -6)
        .attr('height', height2 + 7);

    function mousemove() {
//       convert mouse (x,y)'s x to date
      var x0 = x.invert(d3.mouse(this)[0]);

      var i = bisectDate(data, x0, 1);
// var i = bisectDate(data, data[2].date, 1);
//       console.log(i);

      var d0 = data[i - 1];
      var d1 = data[i];

// if mouse is at the first date, let d be d0; if mouse is beyond the first date, let d be d1
      var d = x0 - d0.date > d1.date - x0 ? d1 : d0;

      helperText.text((new Date(d.date)).toDateString() + ' - Price: ' + d.price + ' Avg: ' + d.average);

      priceTooltip.attr('transform', 'translate(' + x(d.date) + ',' + y(d.price) + ')');

      averageTooltip.attr('transform', 'translate(' + x(d.date) + ',' + y(d.average) + ')');
    }

    function brushed() {

//       if (d3.event.sourceEvent && d3.event.sourceEvent.type === "zoom") return;       

      var s = d3.event.selection || x2.range();  

      x.domain(s.map(x2.invert, x2));    

        y.domain([

          d3.min(data.map(function(d) { return (d.date >= x.domain()[0] && d.date <= x.domain()[1]) ? d.price : min; })), // min here is minimum price of data

          d3.max(data.map(function(d) { return (d.date >= x.domain()[0] && d.date <= x.domain()[1]) ? d.price : max; }))  // max here is maximum price of data
        ]);

        range.text((new Date(x.domain()[0])).toDateString() + ' - ' + (new Date(x.domain()[1])).toDateString())

//   focusGraph has many rects, binding data, but x is updated with new domain
//  therefore, x(d.date) will only reflect brushed dataset         
        focusGraph.attr('x', function(d, i) { return x(d.date); });

        var days = Math.ceil((x.domain()[1] - x.domain()[0]) / (24 * 3600 * 1000))

//   if zoom in on period of less 40 days, set barwidth to be (40-days)*5/6
//   if zoom in n period over 40 days, set barwidth to be 5px
        focusGraph.attr('width', (40 > days) ? (40 - days) * 5 / 6 : 5)


      priceChart.attr('d', priceLine);
      averageChart.attr('d', avgLine);
      focus.select('.x.axis').call(xAxis);
      focus.select('.y.axis').call(yAxis);

    }

    var dateRange = ['1w', '1m', '3m', '6m', '1y', '5y'],
        rangeName;//added

    for (var i = 0, l = dateRange.length; i < l; i ++) {

      var v = dateRange[i];
      rangeSelection
        .append('text')
        .attr('class', 'chart__range-selection')
        .text(v)
        .attr('transform', 'translate(' + (18 * i) + ', 0)')
        .on('click', function(d) {
        rangeName = this.textContent
        focusOnRange(rangeName);
      });

    }

    function focusOnRange(rangeName) {

      var today = new Date(data[data.length - 1].date)
      var ext = new Date(data[data.length - 1].date)

      if (rangeName === '1m')
        ext.setMonth(ext.getMonth() - 1)

      if (rangeName === '1w')
        ext.setDate(ext.getDate() - 7)

      if (rangeName === '3m')
        ext.setMonth(ext.getMonth() - 3)

      if (rangeName === '6m')
        ext.setMonth(ext.getMonth() - 6)

      if (rangeName === '1y')
        ext.setFullYear(ext.getFullYear() - 1)

      if (rangeName === '5y')
        ext.setFullYear(ext.getFullYear() - 5)

      x.domain([ext, today]);

      context.select(".x-brush").call(brush.move, [x2(x.domain()[0]), x2(x.domain()[1])]);

    }

  })// end Data

  function type(d) {
    return {
      date    : parseDate(d.Date),
      price   : +d.Close,
      average : +d.Average,
      volume : +d.Volume, // scale volume smaller
    }
  }
}());
```
[Back](#stock-price-volume-brush-tooltip)    


### update to 4
=> How to Update to version 4    

```html
<script src='http://d3js.org/d3.v4.min.js' charset="utf-8"></script>
```
- Check error on console view     
- Click on the error link to see the problematic code     

[video](https://youtu.be/GhlrzcDc014)      
[Back](#stock-price-volume-brush-tooltip)    

### tickSize    
=> use of axis.tickSize  
```javascript
focus.append('g')
    .attr('class', 'y chart__grid')
    .call(make_y_axis()
    // .tickSize(-width, 0, 0)
    .tickSize(-width)
    // .tickSizeInner(-width)
    // .tickSizeOuter(-width)
    .tickFormat(''));
```
- the correct code should be `tickSize(-width)`    
[video: tickSize src](https://youtu.be/-wThViyYVzY)    
- `.tickSize()` = `.tickSizeInner()` + `.tickSizeOuter()`   
- they all have just one argument   
[video: their effects](https://youtu.be/TKkruCsOKkw)    
[Back](#stock-price-volume-brush-tooltip)    


### margins
=> set three panels starting points and heights and widths
```javascript
var margin = {top: 30, right: 20, bottom: 100, left: 50},
  margin2  = {top: 210, right: 20, bottom: 20, left: 50},
  width    = 764 - margin.left - margin.right,
  height   = 483 - margin.top - margin.bottom -60,
  height2  = 283 - margin2.top - margin2.bottom;

  var svg = d3.select('body').append('svg')
    .attr('class', 'chart')
    .attr('width', width + margin.left + margin.right)
    .attr('height', height + margin.top + margin.bottom + 60);

  svg.append('defs').append('clipPath')
    .attr('id', 'clip')
  .append('rect')
    .attr('width', width)
    .attr('height', height);

    var focus = svg.append('g')
      .attr('class', 'focus')
      .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')');

    var barsGroup = svg.append('g')
      .attr('class', 'volume')
      .attr('clip-path', 'url(#clip)') // added clip-path css
      .attr('transform', 'translate(' + margin.left + ',' + (margin.top + 60 + 20 + 150) + ')');

    var context = svg.append('g')
      .attr('class', 'context')
      .attr('transform', 'translate(' + margin2.left + ',' + (margin2.top + 60 + 150) + ')');
```
- current starting position for 3 panels are a mess, needs a clean way to define them    
[video](https://youtu.be/11OIGzA_Lp8)    
[Back](#stock-price-volume-brush-tooltip)    


### date to string
=> convert a date object to a string in the format we need     
```javascript
var range = legend.append('text')
  .text((new Date(xRange[0])).toDateString() + ' - ' + (new Date(xRange[1]).toDateString()))
  .style('text-anchor', 'end')
  .attr('transform', 'translate(' + width + ', 0)');
```
[video](https://youtu.be/Zz86atOrWx0)    
[Back](#stock-price-volume-brush-tooltip)    


### bisector left    
=> how to use d3.bisector(func).left     
```javascript
var bisectDate = d3.bisector(function(d) { return d.date; }).left;
// only date column are extracted from data
var i = bisectDate(data, data[2].date, 1);
console.log(i)
```
- i is index which is set to be equal or greater than 1       

[video](https://youtu.be/5GpeKc8POqY)    
[Back](#stock-price-volume-brush-tooltip)    


### left out
=> when mouse is at the very first date, use d0; otherwise use d1    
```javascript
      var d0 = data[i - 1];
      var d1 = data[i];
      var d = x0 - d0.date > d1.date - x0 ? d1 : d0;
```
[video](https://youtu.be/KyPG3H36mws)

[Back](#stock-price-volume-brush-tooltip)    



### mouse tooltip
=> mouse-tooltip-two-lines-text-label-updating
```javascript
var mouseArea = svg.append('g')
  .attr('class', 'chart__mouse')
  .append('rect')
  .attr('class', 'chart__overlay')
  .attr('width', width)
  .attr('height', height)
  .attr('transform', 'translate(' + margin.left + ',' + margin.top + ')')
  .on('mouseover', function() {
    helper.style('display', null);
    priceTooltip.style('display', null);
    averageTooltip.style('display', null);
  })     
  .on('mouseout', function() {
    helper.style('display', 'none');
    priceTooltip.style('display', 'none');
    averageTooltip.style('display', 'none');
  })
  .on('mousemove', mousemove);

function mousemove() {
//       convert mouse (x,y)'s x to date
  var x0 = x.invert(d3.mouse(this)[0]);

  var i = bisectDate(data, x0, 1);
// var i = bisectDate(data, data[2].date, 1);
//       console.log(i);

  var d0 = data[i - 1];
  var d1 = data[i];

// if mouse is at the first date, let d be d0; if mouse is beyond the first date, let d be d1
  var d = x0 - d0.date > d1.date - x0 ? d1 : d0;

  helperText.text((new Date(d.date)).toDateString() + ' - Price: ' + d.price + ' Avg: ' + d.average);

  priceTooltip.attr('transform', 'translate(' + x(d.date) + ',' + y(d.price) + ')');

  averageTooltip.attr('transform', 'translate(' + x(d.date) + ',' + y(d.average) + ')');
}

```
[video](https://youtu.be/KyYhNCB7F3o)

[Back](#stock-price-volume-brush-tooltip)    



### css display
=> `.style("display", "none"/null)`: null to display, none to hide     
[video](https://youtu.be/RJz_EEfyzhk)    

[Back](#stock-price-volume-brush-tooltip)  



### brush update
=> How brush func select a range at context and change focus graph at the same time
```javascript

function brushed() {

//       if (d3.event.sourceEvent && d3.event.sourceEvent.type === "zoom") return;       
  var s;

  if(rangeName == undefined) {
      s = d3.event.selection || x2.range();  

    // convert brushed px range to date range and update it to x.domain
    x.domain(s.map(x2.invert, x2));    
  }

    rangeName = undefined;

    y.domain([

      d3.min(data.map(function(d) { return (d.date >= x.domain()[0] && d.date <= x.domain()[1]) ? d.price : min; })), // min here is minimum price of data

      d3.max(data.map(function(d) { return (d.date >= x.domain()[0] && d.date <= x.domain()[1]) ? d.price : max; }))  // max here is maximum price of data
    ]);

    range.text((new Date(x.domain()[0])).toDateString() + ' - ' + (new Date(x.domain()[1])).toDateString())

//   focusGraph has many rects, binding data, but x is updated with new domain
//  therefore, x(d.date) will only reflect brushed dates corresponding px position          
    focusGraph.attr('x', function(d, i) { return x(d.date); });

    var days = Math.ceil((x.domain()[1] - x.domain()[0]) / (24 * 3600 * 1000))

//   if zoom in on period of less 40 days, set barwidth to be (40-days)*5/6
//   if zoom in n period over 40 days, set barwidth to be 5px
    focusGraph.attr('width', (40 > days) ? (40 - days) * 5 / 6 : 5)

  priceChart.attr('d', priceLine);
  averageChart.attr('d', avgLine);
  focus.select('.x.axis').call(xAxis);
  focus.select('.y.axis').call(yAxis);
}
```
[video](https://youtu.be/9rUvRcBd5dI)

[Back](#stock-price-volume-brush-tooltip)    


### click rangeName
=> How to click rangeName and update focus graph and volume bars     
```javascript
var dateRange = ['1w', '1m', '3m', '6m', '1y', '5y'],
    rangeName;//added

for (var i = 0, l = dateRange.length; i < l; i ++) {

  var v = dateRange[i];

  // draw all range options on focus graph top  
  rangeSelection
    .append('text')
    .attr('class', 'chart__range-selection')
    .text(v)
    .attr('transform', 'translate(' + (18 * i) + ', 0)')

    // click any one of rangeName to update rangeName and x.domain date-range
    .on('click', function(d) {

    rangeName = this.textContent
    focusOnRange(rangeName);

  });

}

function focusOnRange(rangeName) {

  // define the dateRange [ext, today] by click rangeName
  var today = new Date(data[data.length - 1].date)
  var ext = new Date(data[data.length - 1].date)

  if (rangeName === '1m')
    ext.setMonth(ext.getMonth() - 1)

  if (rangeName === '1w')
    ext.setDate(ext.getDate() - 7)

  if (rangeName === '3m')
    ext.setMonth(ext.getMonth() - 3)

  if (rangeName === '6m')
    ext.setMonth(ext.getMonth() - 6)

  if (rangeName === '1y')
    ext.setFullYear(ext.getFullYear() - 1)

  if (rangeName === '5y')
    ext.setFullYear(ext.getFullYear() - 5)

// update x.domain() with this new dateRange by click-rangeName
  x.domain([ext, today]);

// run brushed function
  brushed();
}

function brushed() {

//       if (d3.event.sourceEvent && d3.event.sourceEvent.type === "zoom") return;       

  var s;
// if rangeName is not selected, graph updated will be based on brush event
  if(rangeName == undefined) {
      s = d3.event.selection || x2.range();  

    // convert brushed px range to date range and update it to x.domain
    x.domain(s.map(x2.invert, x2));    
  }
// if rangeName is selected, brush event will be ignored, and x.   
    rangeName = undefined;

    y.domain([... ]}

```
[video](https://youtu.be/NmHVUzE19pE)    

[Back](#stock-price-volume-brush-tooltip)  



### update selection box
=> How to update the gray selection rect when click rangeName and drag it smoothly    
```javascript
var brush = d3.brushX()
.extent([[0, 0], [width, height2]])
.on("brush", brushed);

context.append('g')
        .attr('class', 'x-brush')
        .call(brush)
    .call(brush.move, x2.range())
      .selectAll('rect')
        .attr('y', -6)
        .attr('height', height2 + 7);

var v = dateRange[i];
    rangeSelection
      .append('text')
      .attr('class', 'chart__range-selection')
      .text(v)
      .attr('transform', 'translate(' + (18 * i) + ', 0)')
      .on('click', function(d) {
      rangeName = this.textContent
      focusOnRange(rangeName);
    });

  }

  function focusOnRange(rangeName) {
      ...
      x.domain([ext, today]);
    //  x2(x.domain()[0]), x2(x.domain()[1]) update size of gray box .selection
      context.select(".x-brush").call(brush.move, [x2(x.domain()[0]), x2(x.domain()[1])]);
    //  as select the whole brush, so it is dragable
  }
```
[video](https://youtu.be/ZpGyaiQ1Xq0)

[Back](#stock-price-volume-brush-tooltip)  


### Key code update    
=> Key is to understand the updating effect of the following code
```javascript
...
context.select(".x-brush").call(brush.move, [x2(x.domain()[0]), x2(x.domain()[1])]);
...
```
[video](https://youtu.be/OcD7QKh5Brc)

[Back](#stock-price-volume-brush-tooltip)  

### script css
=> How to understand a multiple files example: 
- need more familiar with styles or css      

[video](https://youtu.be/JrU2xhnJmhY)

[Back](#stock-price-volume-brush-tooltip)  



[Demo v3](http://blockbuilder.org/EmbraceLife/8d5f72013244fb92fc4fe03279a14ebf)    
[Demo v4](http://blockbuilder.org/EmbraceLife/14ba2eadaeba1767591e96102a7471a2)    

[Back](#stock-price-volume-brush-tooltip)  


----

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

[Back to TOC](#toc)

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

[Back to TOC](#toc)    


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

[Back to TOC](#toc)    

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

[Back to TOC](#toc)



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


[Back to TOC](#toc)


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


[Back to TOC](#toc)


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

[Back to TOC](#toc)
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
[video](https://youtu.be/FHcqroGTJp4)


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

[Back to TOC](#toc)

----


##### brush-zoom-candle-return

[demo](http://bl.ocks.org/EmbraceLife/d66394e7abd5ee805eeb82284db3106f)

----

### Hover to check

[Demo](http://blockbuilder.org/EmbraceLife/9dc7507eab115461527848925270e81a)   

----



----



### Project
#### Questions
- M2 4 times in 10 years from today backward
- HS300 performance during same period   
- Stocks up 4 times during same period
- stocks with less volatility
- stocks with huge volatility

#### Performance
- Zoom in and hover to display names


[Back to TOC](#toc)
-----
