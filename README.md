# id3-by-examples
Learning D3.js by examples


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


----
### Multi-line Chart Exercies

#### 1-stock-return => line chart

[Practice Demo](http://blockbuilder.org/EmbraceLife/3c6ddf06851e61f9a915c5bc081c0c8e)

#### 3-stock-return data => line chart

[Practice Demo](http://blockbuilder.org/EmbraceLife/04c7747f4f664d3cff48e0c730b417ae)


##### data by column vs path vs line

##### missing data
