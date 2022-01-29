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
you will see that there are 2 bars as seen below in which the 2nd has a greater color span. The first is limited because of the floor divission, but you can see a slight
shift in color if you look closely. Here is what you would call to show the second colormapped output along with the color slide:
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




