# Using Color Schemes, and Polar Coordinates, to Create Discrete and Continuous Visuals in MatPlotLib

MatPlotlib offers you a nice selection of graphics packages in order to display your data with different schemes. This write up is a good representation 
of some great practice activities to just get comfortable with colormaps, different line styles, discrete blocks of data, continuous graphics spreads, and 
how to achieve those with a variety of MatPlotLib functionality. I explore those options with this dataset. 

Here are the packages that will need to be used in order to accomplish the different graphs here:
  
|Library|Note|
|:-------------|:--------------|
|import matplotlib as mpl| The matplotlib library|
|import matplotlib.pyplot as plt| Basic plotting from library|
|import matplotlib.colors as col| For basic named colors|
|import pandas as pnd| General manipulations in Python for plotting, data selection, and more|
|import numpy as np| General formulaic manipulations|
|import proplot as plot| Package that allows for continuous colormaps in Python|

## Discrete and Less Discrete Data Creation

A good place to start is to just create a range of numbers (*here we sampled 1-51*) and append those to a list. Then, run through that same number and floor divide 
by some modulus value (*like 5 `i//5`*) creating a second list. Then set up a list of the two lists which will allow you to plot both lists against each other. Place the 
more discrete list first (*the list with the floor division*). 

Now, set up a few different colormaps in Python noting the second method allows you to divide the map into shades which the first doesn't so much:
`cm = col.ListedColormap(['lime','red'])`

`cm2 = plot.Colormap(('lime','red'), name='Contrast')`

Set up a third colormap for later use:
`cm3 = plot.Colormap(('honeydew','peachpuff','firebrick','mediumblue'))`

Now if you try graphing with the first colormap (*cm*), you will notice that it sets up 3 lime green big blocks and 1 red big box. However if you try graphing with cm2
you will see that there are 2 bars as seen below in which the 2nd has a greater color span. The first is limited because of the floor division, but you can see a slight
shift in color if you look closely. Here is what you would call to show the second color mapped output along with the color slide:
`fig, ax =plt.subplots()`

`ax.imshow(data,cmap=cm2,aspect = 'auto',extent=[0,52,0,52],vmin=1,vmax=51)`

**Scaled display of 2 different ranges (notice the first only goes 1/5th as far as the second)**
<img src="https://github.com/AxisMeetsWorld/Color-Schemes-and-Polar-Coordinates/blob/main/Two%20arrays%20graphed.png" width=60% height=60%>

Here are a few other basic chart graphing basics: 
- Line Graph code

`inp=[1,2,3,4,5,6,7]`

`outp=[]`

`for i in inp:`

` outp.append(i**2)`

`plt.plot(inp,outp,color='aqua',marker='o',markerfacecolor='blue')`

![Output](https://github.com/AxisMeetsWorld/Color-Schemes-and-Polar-Coordinates/blob/main/line-dot.png)


- Pie Chart example

`budget=[450,300,950,1025]`

`costs=['groceries','travel','leasure','rent']`

`cols=['red','green','yellow','purple']`

`plt.pie(budget,labels=costs,colors=cols,shadow=True,startangle=180,radius=2.5)`

![Pie Output](https://github.com/AxisMeetsWorld/Color-Schemes-and-Polar-Coordinates/blob/main/Basic%20pie.png)

- 3 color slide graphs in one from the color schemes we created earlier. 

The real trick here is to simply set up 3 color graphs in 3 columns with the MatPlotLib.subplots function and then use different color maps with the 
**pcolormesh()** function. This only shows one of the called pcolormeshes.

`fig, (ax1, ax2, ax3)= plt.subplots(nrows= 1, ncols=3, figsize=(10,4))`

`ax1.pcolormesh(data,cmap=cm3)`

`ax1.set_title('Beach to Night Color')`

![Three different color slide graphs](https://github.com/AxisMeetsWorld/Color-Schemes-and-Polar-Coordinates/blob/main/three_slides.png)

## Advancing Into Polar Coordinate Graphs

*Note there is more in the code attached that shows different discrete vs continuous breakdown, but for the purposes of efficiency this guide skips onto the next conceptually
different implementation; polar coordinates.*

Moving this along to a more "centered" and artistically based approach, let's introduce polar coordinates and how to switch from Cartesian coordinates in Python.
You can see in the code that when you are setting up the subplots. Without getting into all the chart building details, here are the lines of code that are the most 
imperative to setting up your polar coordinates:

-Set up the two graph spaces that will be oriented towards polar coordinates
`ax2 = fig2.add_subplot(111,projection='polar')`

`ax3 = fig2.add_subplot(111,projection='polar')`

-Set up your radius and theta arrays noting the order they must be set up in based on dependency
`r = np.arange(0,5,0.01)`

for a spiral graph `theta = 2*np.pi*r`

**Note to set up a pedal graph there is more of an integral relationship between the radius and the angle (theta). You need to establish the angle first and account for the 
area in a circle formula. Here the radius has to be dependent upon the angle, so considering the span across the graph area is 2(pi)(r), you double the amount.**
`theta2 = np.arange(0,np.pi*10,0.02)`  
*You won't see all of the pedal graph if you don't make sure the range here goes through the same amount of ticks as the previous graph since they are being blended.
The range of angles above was 2np.pi\*5 so that is where you get the np.pi\*10 here.*

Now r is  `r2 = 4*np.cos(6*theta2)` where the 4 determines the magnitude of the pedals, and the 6 here determined the number of pedals. 

**Here is your graph**

<img src="https://github.com/AxisMeetsWorld/Color-Schemes-and-Polar-Coordinates/blob/3429ad3f66ff1f699d2fb958433efb0ab3731191/SPIEral%20Graph.png" width=60% height=60%>)

## Adding a background to demonstrate distance

One last concept is trying to fill in the background with a constant pattern to sort of create a "heatmap" feel to where the plot points/lines are. One example of how that might be used is to show how long a marathon runner who is running in an ever expanding circular motion has distanced from the start. Perhaps this color code could represent the lactic acid build up.
To implement this: 

-Again start out with adding a subplot with a polar projection

`ax2 = fig2.add_subplot(111,projection='polar')`

-Set up variable ranges for angle and radius with respect to the line drawn, and the area of the chart

`rline = np.linspace(0,2*np.pi,150)`

`rthet = 2*np.pi*rline`

`r = np.linspace(0,2*np.pi,150)`

`theta = np.linspace(0,2*np.pi,300)`

-Now, the trick here to get the polar coordinates into your background is to use the pcolormesh() function along with the meshgrid() function from the MatPlotLib and Numpy libraries respectively.

`rad, thet = np.meshgrid(r,theta)`

*Set up z to align the color shading with the angle as the pcolormesh needs that 3rd variant to shade*
`z = thet`

`acol2=ax2.pcolormesh(rad,thet,z,cmap=cm2)`

-You can add a colorbar, and some tick marks, but the last step is to add the spiral line to the plot which has the background shading

`ax2.plot(rthet,rline,color='b')`

**⭐ Here is your plot which shows a sort of measure of how far you have spiraled away from the center ⭐**

<img src="https://github.com/AxisMeetsWorld/Color-Schemes-and-Polar-Coordinates/blob/main/SpiralFade.png" width=60% height=60%>)

There are other representations here and you don't necessarily have to have the fade start from center, but this gives an idea of how you would build a radial chart, and how you might implement different color schemes to convey what you have found in your analysis! Happy coding 🙂



