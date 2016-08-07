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



----
### Multi-line Chart

#### 1-stock-return => line chart
* no missing data

[Practice Demo](http://blockbuilder.org/EmbraceLife/3c6ddf06851e61f9a915c5bc081c0c8e)

#### 3-stock-return data => multi-line chart
* no missing data


[Practice Demo](http://blockbuilder.org/EmbraceLife/04c7747f4f664d3cff48e0c730b417ae)



#### 3-stock-return data => multi-line chart
* with missing data handled     

[Practice Demo](http://blockbuilder.org/EmbraceLife/c85ff2725cd17ca16371ae58689b9b15)


#### 3-stock-return data => Multi-line chart
* missing data bridged by previous data
* switch the demo below data file to "data_filled.csv"

[Practice Demo](http://blockbuilder.org/EmbraceLife/c85ff2725cd17ca16371ae58689b9b15)

##### Notes
* How to parse dateformat from data.file
* How to handle NaN inside data-row-object
* How to handle null data on d3.line().defined()

[Video]()




----

## BarChart

###
