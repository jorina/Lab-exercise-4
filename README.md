# Lab-exercise-4

## Sources
This tutorial is based on a MATLAB exercise from [Prof. Todd Ehlers (Uni Tübingen)](http://www.geo.uni-tuebingen.de/?id=2183) and [Prof. Brian Yanites (Uni Idaho)](https://www.uidaho.edu/sci/geology/people/faculty/byanites).

## Overview
For the exercises this week, we will be applying the advection equation to bedrock river erosion with a spatially variable advection coefficient (stream-power erosion). You are asked to modify an starter Python script to produce plots and to answer questions related to the plots. As before, we will be using **Spyder** for these exercises.

## Getting started
1. You can start by making a folder to store files for this week's exercises in a Terminal.

    ```bash
    $ cd Desktop
    $ mkdir Lab-4
    $ cd Lab-4
    ```
**Reminder**: the `$` symbol above represents the command prompt in the Terminal window.
2. Now you can open **Spyder**.

    ```bash
    $ spyder
    ```

Now we are ready to start.

## Problem 1 - Introduction to river profile evolution
For this exercise we will be using the Python script [`river_profiles.py`](river_profiles.py) to plot river profiles. The script performs all of the basic calculations needed to answer the questions below, but you will need to make some changes to the script to complete the exercise. To begin, download a copy the [`river_profiles.py`](river_profiles.py) file to your `Lab-4` directory and open it in **Spyder**.

### Part 1 - Examining the code
The program simulates river incision into a 100-km-wide landscape with an initial flat surface elevation of 1500 m. River incision is calculated using the stream-power erosion equations described in [Lecture 7](https://github.com/Intro-Quantitative-Geology/Lecture-slides/blob/master/07-Advection-of-the-Earths-surface/07-Advection-of-the-Earths-surface.pdf). For this part you should do the following:

1. Carefully read over the Python source code and comments. There are some new features in this code, so pay attention to where the variables are defined and used, how the initial topography is defined, how the upstream drainage basin area is calculated, how surface elevation is calculated and how the results are plotted.
2. Without making any changes, run the program and save a copy of the plot it produces. The program will take about 1 minute to run. **Add your plot at the end of your version of this document and include a figure caption explaining what the plot shows**.
3. Look again through the Python code and the plot it produces. Answer the following questions in the space beneath the plot and caption you've inserted.
  - **How long is the time step in the calculation?**
  - **What is the rock uplift rate in the model? Is it constant or does it vary with space in the model?**
  - **What is the maximum elevation of the topography at the end of the simulation? Is this higher or lower than the original maximum elevation? Why?**
  - **Does the maximum elevation continually increase with time, or does it also decrease? Why might this be? Does the river profile appear to reach a steady state?**
  - **How fast (at what velocity) does the drainage divide (highest point in the topography) migrate across the model?** To calculate this value, you should run the model several times for shorter simulation times, note the position of the divide at the completion of the simulation and then calculate the velocity (distance travelled divided by time).

### Part 2 - Subplots and erosion rates
This program calculates erosion rates across the length of the channel as a function of time in order to update the topography at the end of each time step. Currently, the program only plots the topography. For this part of the exercise, your goal is to plot both the topography and erosion rates on separate plots. This can be done using the `plt.subplot()` function to add a second plot beneath the existing plot. Currently, the first plot is created in the Python script using the commands

```python
# Format subplot 1
axis1 = plt.subplot(1,1,1)                  # Set axis1 as the first plot
axis1.set_xlim([0.0, max(xkm)])             # Set the x-axis limits for plot 1
axis1.set_ylim([0.0, max_elevation*1.1])    # Set the y-axis limits for plot 1
plot1, = plt.plot(xkm, topography)          # Define plot1 as the first plot
plt.xlabel("Distance from drainage divide [km]")
plt.ylabel("River channel elevation [m]")
plt.title("River channel profile evolution model")
```

This is slightly different than past plots for two reasons. First, we would like to have multiple plots in one window. Second, to update the plot in an animation in the plot window, we need to define a variable to refer to the plot frame (`axis1`) and the line that will be plotted (`plot1`). Here, by using `plt.subplot()` function, we have allowed ourselves to potentially have several plots in one window, but it is set to only have one plot. The syntax for the `plt.subplot()` command is `plt.subplot(nrows, ncols, plot number)`, where `nrows` is the number of rows of plots, `ncols` is the number of columns of plots and `plot number` is the number of the plot in the list. Currently, we have 1 row, 1 column and 1 plot to display. Note that we have also defined the axis limits separately so they can be updated in the animation. For this part, you should:

1. First increase the number of rows to two for the first plot, then add the code necessary to generate a second plot similar to the example for plot 1. The second plot should be below the first plot and show the erosion rate **in mm/a** across the river profile with proper axis labels.

    :heavy_exclamation_mark: **NOTE**: Because the coordinate system for elevation is positive upwards, you should multiply the erosion rates that are calculated by -1 so that they are positive values.<br/><br/>
If you run your simulation for 100,000 years, you should see something like the following plot:

    ![Subplot example](Images/subplot_example_100ka.png)<br/>
    *Figure 1. An example of using the `plt.subplot()` function. Your plot should look like this.*

2. **Add your plot at the end of your version of this document and include a figure caption**.
3. Run the program with a rock uplift rate of 1 mm/a and answer the following questions below the plot you've just inserted:
  - **What are the fastest erosion rates your see in your river profile?**
  - **Do the fastest erosion rates always occur in the same place, or does the location of fastest erosion change?** Explain why this occurs, based on the equations for stream-power erosion presented in Lecture 7.
4. Rerun the program with a rock uplift rate of 3 mm/a and answer the following questions at the end of your version of this document:
    - **What is the maximum elevation you observe in the model after 100,000 years now?**
    - **What is the maximum erosion rate in the model after 100,000 and 2,000,000 years? Does the river profile reach an equilibrium elevation?**

### Part 3 - Sloping initial topography
Modify the program so that it now uses an initial topography that is sloping rather than flat. This feature is already available in the code, but you will need to locate it and change the corresponding variable in order to use sloping initial topography. Rerun the program and perform the following steps:

1. **Save the plot that is generated after 2,000,000 years with a rock uplift rate of 1 mm/a, insert a copy at the end of your version of this document and include a figure caption**.
2. **Explain how fast (at what velocity) the drainage divide migrates back into the initial topographic surface**. As before, you may want to run several shorter simulations to calculate the position of the divide at various times in order to find a velocity (distance over time). **How fast is this velocity compared to that calculated in question 1?**
3. Look at the erosion rates across the profile. **Are the majority of the erosion rates greater than, less than or equal to the rock uplift rate? Based on this answer, is the topography in a steady state (i.e., not changing)?**

### Part 4 - The stream-power erosion law exponents
Change the initial topography back to a flat surface. In the stream-power erosion law, there are two important exponents (*m* and *n*) that will alter the efficiency of river erosion when varied. Change the values of *m* and *n* to the different values listed in the comments in the code and rerun the program for each pair of *m* and *n* values.

1. **Save a copy of each of the three plots that are generated and add them to the end of your version of this document including a figure caption**.
2. **Is the river channel profile sensitive to variations in *m* and *n*?**

### Part 5 - Non-uniform channel uplift
Change the values of *m* and *n* back to the original values (*m* = 1.0, *n* = 2.0). Currently, the program uses a constant rock uplift rate across the river profile. Modify the program to have a rock uplift rate of 5 mm/a when *x* ≤ 50 km, and an uplift rate of 1 mm/a when *x* > 50 km. This discontinuity is equivalent to placing an active fault along the river profile. Rerun the program and perform the following tasks:

1. **Save a copy of the plot that is generated and add it to the end of your version of this document along with a figure caption**.
2. Answer the following questions:
  - **Is the maximum topography higher or lower in this simulation compared to that in part 1 of this problem?**
  - **Does the river profile after 2 million years clearly show where the change in uplift rate occurs?**
  - **Does the plot of erosion rates clearly show where the change in uplift rate occurs as the profile evolves?**


## What to submit
**For this exercise, your modifications to the end of this document should include**

1. One plot each for Parts 1-3 and Part 5.
2. One plot for **each** combination of *m* and *n* values for Part 4.
3. A figure caption beneath **each** plot explaining what it shows as if it was in a scientific publication.
4. Answers to the questions in bold for Parts 1-5 inserted beneath the associated plots and captions in each Part.

# Answers
## Problem 1
### Part 1
![Text shown if image does not load](Images/figure_1-1.png)<br/>
*Fig.1: River channel profile after 2,000,000 yr. The initial conditions include a flat initial topography, a constant uplift rate of 0.001 m/a and area (m) and slope (n) exponents equal to 1.00 and 2.00 respectively. The maximum elevation resulting from this model at the specified time is 2334.1 m, and we can see a gradual slope that is more abrupt or steep in the top section of the river profile (x < 20km).*

**How long is the time step in the calculation?**

The time step is 2.0 yr for profile calculations, and 2000.0 yr for displaying the plots.

**What is the rock uplift rate in the model? Is it constant or does it vary with space in the model?**

The rock uplift rate is equal to 0.001 m/a (1 mm/a), and is constant.

**What is the maximum elevation of the topography at the end of the simulation? Is this higher or lower than the original maximum elevation? Why?**

The maximum elevation at the end is 2334.1 m, that is higher than at first, because the change in topography is based on uplift and river erosion, and migrates from the minimum elevation area to the higher, as a result of an increase in the drainage basin area (higher stream power), so in the higher area, the effect of erosion is minimum during most of the experiment, in comparison to lower areas, therefore only the uplift is taking place at that point (or at least, dominates over the erosion) and so the maximum elevation increases. 

**Does the maximum elevation continually increase with time, or does it also decrease? Why might this be? Does the river profile appear to reach a steady state?**

The maximum elevation does not increase linearly during the whole simulation, but at some point (around 2330-2340) the river achieves the steady state, and the maximum topography stabilize, even decreasing a little bit until it totally stabilize at 2334.1 m.

**How fast (at what velocity) does the drainage divide (highest point in the topography) migrate across the model?**

T0=0 ->        X0= 80 km

T1= 2000 ->    X1= 73km       ΔX01= 7000m/2000yr= 3.500 m/yr

T2= 10000 ->   X2= 60 km      ΔX12= 13000m/8000yr = 1.625 m/yr

T3= 20000 ->   X3= 50 km      ΔX23= 1.00 m/yr

T4= 30000 ->   X4= 45km       ΔX34= 0.5 m/yr

T5= 100000 ->  X5= 22km       Δx45= 0.33 m/yr

T6= 1000000 -> X6= 100km      Δx06= 0.087 m/yr

The migration velocity varies across the model, with faster velocities in the early years (3.5 m/yr), and slowing down with time (e.g. 0.33m/yr).

:cow: 4.5/4.5pts

### Part 2

![Text shown if image does not load](Images/figure_2.png)<br/>
*Fig.2: The upper subplot shows the river channel profile at t= 100,000 yr, with the same initial conditions as in Fig.1 The maximum elevation at that time is 1604.0 m. The bottom subplot shows the fluvial erosion rate of the river channel profile of the upper subplot, at equal time than this one. At 100,000 yr the maximum erosion is 12.7 mm/a, and is located at x= 25km.*

###### Run the program with a rock uplift rate of 1 mm/a:

**What are the fastest erosion rates your see in your river profile?**

The fastest erosion rate is 293.4 mm/a at t= 0.  

**Do the fastest erosion rates always occur in the same place, or does the location of fastest erosion change?**

The fastest erosion rate always occurs at time 0, in the lowest part of the river, but the maximum erosion rate at every time migrates from the lowest part of the river towards the upper part, and that is because the stream power increases downstream as the discharge grows, but as a result of this, the slope decreases and the fastest erosion rate migrates upstream, where the equation –K*Am * Sn is maximized. 

###### Rerun the program with a rock uplift rate of 3 mm/a:

**What is the maximum elevation you observe in the model after 100,000 years now?**

1812 m.

**What is the maximum erosion rate in the model after 100,000 and 2,000,000 years? Does the river profile reach an equilibrium elevation?**

After 100,000 years, the max erosion rate is 12.8 mm/a. And after 2,000,000 yr, 3.1 mm/a. Yes, the river profile reached an equilibrium elevation, and also the erosion rate (when erosion rate = uplift rate).

:cow: 4/4pts

### Part 3

![Text shown if image does not load](Images/figure_3.png)<br/>
*Fig.3: There are the same two subplots as in Fig.2, but for that figure, the initial topography has been changed to sloping (constant slope).The figure shows the river profile and erosion rate at time equal to 2,000,000 yr. The resulting maximum elevation at that time is the same as in fig.1, but with the main difference that the higher elevation point, or dividing drainage, is always in the same point (x=0).*

**Explain how fast (at what velocity) the drainage divide migrates back into the initial topographic surface. How fast is this velocity compared to that calculated in question 1?**

The drainage divide does not migrate, so the velocity is 0, and so, it is smaller than the calculated in question 1.

**Are the majority of the erosion rates greater than, less than or equal to the rock uplift rate? Based on this answer, is the topography in a steady state (i.e., not changing)?**

They are higher until the steady state is achieved (erosion rate = uplift rate), so the topography is  changing until the steady state is achieved, and then becomes stable.


:cow: 4/4pts
### Part 4

![Text shown if image does not load](Images/figure_4-1_bed_shearstress.png)<br/>
*Fig.4: This figure is displayed using the same initial conditions as in fig.1, but changing the exponents m and n to 0.3 and 0.7 respectively, representing bed shear stress conditions. The resulting river profile is totally different, with incision (erosion) only in the bottom part of the river, close to x= 100km, but with the maximum erosion being 0.01mm/yr, so almost nonexistent. As a result of this so focused erosion, the rest of the river profile shows a kind of plateau topography, beeing totally flat and having an elevation of 3504.0m, more than 1000m higher than in previous figures. In that model, the profile is still changing with time, due to the focused erosion, so in theory there is no steady state, but being the erosion so small, the profile is almost steady.* 

![Text shown if image does not load](Images/figure_4-2_stream_power_channel_length.png)<br/>
*Fig.5: The initial conditions are the same as in fig.4, but the exponents are changed again, being both equal to 1. These exponents represent the stream power per unit channel length. The effects are dramatically different than in fig.4, with a maximum topography of 239.6m, but with a totally different profile, displaying a low topography (light slope) almost all over the profile, and with a really abrupt change in slope at x < 10km. In that model we can conclude that the steady state has been achieved, because the erosion is the same, 1mm/a, all over the profile, and there is no change in topography with time anymore.*

![Text shown if image does not load](Images/figure_4-3_stream_power_bed_area.png)<br/>
*Fig.6: The exponents has been changed to 0.5 and 1.0 for m and n respectively, to represent the conditions of stream power per unit bed area. The resulting profile is similar to the one in fig.4, due to the bed (rock) conditions that both displayed, with the same maximum topography, but in this figure the erosion is more important, and even if it is localized in the same place as in fig.4, here the maximum erosion in that area is about 1mm/a, so there is a much deeper incision, beeing 0 the minimum topography in that area. Like in fig.4, there is no steady state, and the profile grows at a velocity rate of 1mm/a all over the profile but where the erosion acts.*

**Is the river channel profile sensitive to variations in m and n?**

Yes, it is sensitive to variations in m and n, because the fig.4-1, fig.4-2 and fig.4-3 show different river profiles, and only the m and n exponents has been changed. Is also possible to notice it in the stream power equation, because even a small change in the exponents can have a large effect on the result.

:cow: 4/4pts

### Part 5

![Text shown if image does not load](Images/figure_5.png)<br/>
*Fig.7: This model displays the same initial conditions as in fig.1, but for the rock uplift, that is modified to 5 mm/a when x ≤ 50km, and remains at 1mm/a rate for the rest of the x length. The result after 2,000,000 yr is the same as in fig.1, but not during the whole evolution of this model, because the profile showed at certain moments in early stages obeys these differences in uplift rates, with a higher topographies in the upper parts of the river, and also higher erosion rates at the same point as a result of those first ones. Because of that, the differences of uplift rate are finally counterbalanced, and the final topograpy shows no difference with the one displayed in fig.1.*

**Is the maximum topography higher or lower in this simulation compared to that in part 1 of this problem?**

The maximum topography is the same for both plots.

**Does the river profile after 2 million years clearly show where the change in uplift rate occurs?**

No, it does not; there is a gradient slope that is quite similar to the one showed in fig.1.

**Does the plot of erosion rates clearly show where the change in uplift rate occurs as the profile evolves?**

Not clearly, because even if the maximum uplift rate is situated in the x < 50km half of the plot for most of the time, that can also be observed in the previous plot evolutions.

:cow: 2/3.5 pts your plots are not correct. with the correct plot you would have answered correct: Q1: it is higher; Q3: yes, clear change

:cow: total 18.5/20pts
