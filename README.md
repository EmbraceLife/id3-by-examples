# id3-by-examples
**Lessons learnt**    
1. the better I understand previous work, the more confident I am to tackle new problems
2. If there is no need to read or watch my work again and again, then I should not make them in the first place



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


**Step 1**   
- Create a canvas     
- Locate a tarting point for drawing   

[Video](https://youtu.be/MroiTmauDeg)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/d3bb1c7c3275ae84a5b8a12f28b1f2a5)


**Step 2**   
- func => format date for data file       
- func => map date to px on x-axis, update px range        
- func => map temperature to px on y-axis, update px range       
- func => map city names to color, give 20 default colors     
- func => tranform data points into points of lines    

[Video](https://youtu.be/uiwh0EJPKr8)    
[Practice Demo](http://blockbuilder.org/EmbraceLife/c675ec2a11d547ac62ab57c04f7a4e02)  


**Step 3**   
- func => tranform each row of data from data file     
 + apply date format func
 + convert string to number   
- load data file and preprocess data
- reorganise dataset by columns


[Video1](https://youtu.be/NgjhKnoWGZg)    
[Video2](https://youtu.be/AnSUbBXXvnM)   
[Practice Demo](http://blockbuilder.org/EmbraceLife/3f7287859b3c582cb2a451a42a6faf58)


**Step 4**   
- update date range for (func => map date to px on x-axis)
- update temperature range for (func => map temperature to px on y-axis)
- update city names for (func => map city names to color)
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
- .area {clip-path: url(#clip)} ????
- .zoom {cursor: move; pointer-events: all;} ????
- set height and width for 2 view panels  
[video](https://youtu.be/dlxRFf5tmiI )     
[Demo](http://blockbuilder.org/EmbraceLife/7efd1f9031beecb5252e57e944e1a440)

### Hover to check

[Demo](http://blockbuilder.org/EmbraceLife/9dc7507eab115461527848925270e81a)
