# Lab-exercise-4

## Sources
This tutorial is based on a MATLAB exercise from [Prof. Todd Ehlers (Uni Tübingen)](http://www.geo.uni-tuebingen.de/?id=2183) and [Prof. Brian Yanites (Uni Idaho)](https://www.uidaho.edu/sci/geology/people/faculty/byanites)].

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

## Problem 1 -Introduction to river profile evolution
For this exercise we will be using the Python script [`river_profiles.py`](river_profiles.py) to plot river profiles. The script performs all of the basic calculations needed to answer the questions below, but you will need to make some changes to the script to complete the exercise. To begin, download a copy the [`river_profiles.py`](river_profiles.py) file to your `Lab-4` directory and open it in **Spyder**.

1. The program simulates river incision into a 100-km-wide landscape with an initial flat surface elevation of 1500 m. River incision is calculated using the stream-power erosion equations described in [Lecture 7](https://github.com/Intro-Quantitative-Geology/Lecture-slides/blob/master/07-Advection-of-the-Earths-surface/07-Advection-of-the-Earths-surface.pdf). For this part you should do the following:
  1. Carefully read over the Python source code and comments. There are some new features in this code, so pay attention to where the variables are defined and used, how the initial topography is defined, how the upstream drainage basin area is calculated, how surface elevation is calculated and how the results are plotted.
  2. Without making any changes, run the program and save a copy of the plot it produces. The program will take about 1 minute to run. **Insert the plot into your write-up for this week's exercises and add a figure caption explaining what the plot shows**.
  3. Look again through the Python code and the plot it produces. **Answer the following questions in the space below the plot and caption you've inserted previously**.
    - How long is the time step in the calculation?
    - What is the rock uplift rate in the model? Is it constant or does it vary with space in the model?
    - What is the maximum elevation of the topography at the end of the simulation? Is this higher or lower than the original maximum elevation? Why?
    - Does the maximum elevation continually increase with time, or does it also decrease? Why might this be? Does the river profile appear to reach a steady state?
    - How fast (at what velocity) does the drainage divide (highest point in the topography) migrate across the model? To calculate this value, you should run the model several times for shorter simulation times, note the position of the divide at the completion of the simulation and then calculate the velocity (distance travelled divided by time).
2. This program calculated erosion rates across the length of the channel as a function of time in order to update the topography at the end of each time step. Currently, the program only plots the topography. For this part of the exercise, your goal is to plot both the topography and erosion rates on separate plots. This can be done using the `plt.subplot()` function to add a second plot beneath the existing plot. Currently, the first plot is created in the Python script using the commands

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
This is slightly different than past plots for two reasons. First, we would ultimately like to have multiple plots in one window. Second, to update the plot in an animation in the plot window, we need to define a variable to refer to the plot frame (`axis1`) and the line that will be plotted (`plot1`). Here, by using `plt.subplot()` function, we have allowed ourselves to have several plots in one window. The syntax for the `plt.subplot()` command is `plt.subplot(nrows, ncols, plot number)`, where `nrows` is the number of rows of plots, `ncols` is the number of columns of plots and `plot number` is the number of the plot in the list. Currently, we have 1 row, 1 column and 1 plot to display. Note that we have also defined the axis limits separately so they can be updated in the animation. For this part, you should
  1. First increase the number of rows to two for the first plot, then add the code necessary to generate a second plot similar to the example for plot 1. The second plot should be below the first plot and show the erosion rate **in mm/a** across the river profile with proper axis labels.

    :heavy_exclamation_mark: **NOTE**: Because the coordinate system for elevation is positive upwards, you should multiply the erosion rates that are calculated by -1 so that they are positive values.<br/><br/>
  If you run your simulation for 100,000 years, you should see something like the following plot:
  
    ![Subplot example](Images/subplot_example_100ka.png)<br/>
    *Figure 1. An example of using the `plt.subplot()` function. Your plot should look like this.*

  2. **Add your plot to your write-up and give it a descriptive figure caption**.
  3. **Run the program with a rock uplift rate of 1 mm/a and answer the following questions in your write-up**:
    - What are the fastest erosion rates your see in your river profile?
    - Do the fastest erosion rates always occur in the same place, or does the location of fastest erosion change? Explain why this occurs, based on the equations for stream-power erosion presented in Lecture 7.
  4. **Rerun the program with a rock uplift rate of 3 mm/a and answer the following questions in your write-up**:
    - What is the maximum elevation you observe in the model after 100,000 years now?
    - What is the maximum erosion rate in the model after 100,000 and 2,000,000 years? Does the river profile reach an equilibrium elevation?
3. Modify the program so that it now uses an initial topography that is sloping, rather than flat. This feature is already available in the code, but you will need to locate it and change the corresponding variable in order to use sloping initial topography. Rerun the program and perform the following steps:







3. Modify the file to include a `for` loop that calculates the surface elevation of the hillslope (variable `h`) as a function of horizontal distance (variable `x`). Your *x*-values should be in one-meter increments and the *x*-value range should be large enough to include one complete interfluve (ridge) from valley to valley. The equation for calculating the elevation as a function of horizontal distance (*x*) was presented in lecture and is already in the Python script. Your job is to make it calculate the elevation at each *x*-value.
2. Two channels are located 100 m apart and incise into a landscape being uplifted at a rate of 0.5 mm/a producing an interfluve with two symmetrical hillslopes. Calculate the profile of the hillslope system, assuming the erosion is a diffusive process with a diffusion coefficient of 50 × 10<sup>-3</sup> m<sup>2</sup>/a. You should do this calculation using the solution for the diffusion equation in the Python script, which is parabolic in form.
3. Add some calculated values for this hillslope geometry to the plot.
  - **At what value of *x* (distance from the divide) is the maximum slope?** Add lines of code to the bottom of the Python program to calculate the maximum slope and add it to the plot with the `text()` function (see `help(plt.text)` for help using this function). You can find the equation for the slope (*dh*/*dx*) in the notes from Lecture 6 where the diffusion equation was solved. **Where is the maximum slope in relation to the crest of the interfluve and the river channel?**
  - What is the maximum slope angle in degrees? Add this to your plot using the `text()` function below the maximum slope.
  - What is the maximum relief of the hillslope? The maximum relief is the difference in elevation between the hillcrest and the adjacent valley bottom. Add lines of code to the bottom of the Python script to calculate the maximum relief and display it on the plot with the `text()` function.
  - Diffusive problems have a characteristic timescale τ. **What does a characteristic timescale mean?** You may want to use [Google](https://www.google.fi) to look up the characteristic timescale of diffusion. Mathematically, the characteristic time scale for diffusion is simply the length scale of the problem squared, divided by the diffusivity. Convert the previous sentence into an equation in Python, and add lines of code to the bottom of the Python script to calculate the characteristic timescale and display this information on your plot using the `text()` function. **What is the value for the characteristic timescale? Does it seem reasonable? Why or why not?**

    :heavy_exclamation_mark: This is a good point to stop and save a copy of your plot with the values calculated in questions 3 displayed as text on the plot.

4. Explore the effect of different parameters on the hillslope geometry. Starting with the initial plot you made for question 2 above, make an additional plot for each of the four variations to the following parameters. In each case be sure you only vary a single parameter from the original values in question 2.
  - Change `L` to 100 m
  - Double the uplift rate
  - Double the diffusivity
  - Reduce the diffusivity by half

**For questions 2-4 of this exercise, you should modify the end of this document to include**

1. One plot with the values from question 3 displayed as text on the plot.
2. One plot for **each** of the four modifications in question 4.
3. A figure caption beneath **each** plot explaining what it shows as if it was in a scientific publication.
4. Answers to the questions in bold for question 3 beneath the plots and captions.

**You should also save a copy of your modified code in your Github repository**.

## Problem 2 - Mountain hillslope profiles
Active mountain ranges typically have poorly developed soils and abundant exposed bedrock.

### Part 1 - Mountain hillslope profiles
For this question, you can use your modified Python script from Problem 1. Assuming an interfluve width of 20 km, an uplift rate of 0.5 mm/a, and an appropriate diffusivity for rock of 10 m<sup>2</sup>/a, calculate a hillslope profile. Again calculate the maximum slope and its value in degrees, the maximum relief, and the characteristic timescale just as you did for Problem 1.

### Part 2 - Incision history of the western Sierra Nevada mountains, California, USA 
For this section we will apply our model equation to a real landscape, the western Sierra Nevada mountains in California, USA. We will use a [topographic profile](sierras_profile.txt) extracted across an interfluve between two streams draining into the Yuba River and change the landscape uplift rate in the equation until we get a reasonable match to the observed profile from our equation.

1. Before we load anything, it is important that you know the location of the topographic profile.

    ![Topographic profile location](Images/Sierras_profile_map.png)
    *Figure 1. Shaded relief digital elevation model of the western Sierra Nevada Mountains in California, USA. The line A-A´ is the location of a topographic profile used in Part 2 of Problem 2.*

2. Now that you know where the profile is located, you should download [a copy of the data file](sierras_profile.txt) for this week's exercise and save it in your directory `Lab-3` directory. The data file contains distances from the drainage divide and elevations for the topographic profile A-A´. For this part of the exercise you will also be using [another broken Python script](hillslope_profile_ex2.2.py) for loading and plotting the profile data and your calculated hillslope profile geometry. The profile data should be loaded into arrays `data_x[]` and `data_h[]`, noting that the first column in the data file should be `data_x` and the second should be `data_h`. There is no header on this file. As in Problem 1, part of this script is not currently working and you will need to add the `for` loop for calculating the hillslope elevations exactly like you did in Problem 1.
3. Once you have modified the program to add the `for` loop, you will want to change some of the variables that go into the equation for hillslope diffusion. You will be exploring a range of landscape uplift rates (`U`), but the values for the other variables should not change. Set the diffusion coefficient `kappa` to 1.8 m<sup>2</sup>/a and the half-width of the hillslope `L` should be half of the distance between the channels, which can be measured off the topographic profile in Figure 2 below. Your *x*-values should range across the entire interfluve with distance increments of 100 m.

    ![Topographic profile](Images/sierras_profile.png)<br/>
    *Figure 2. Topographic profile across an interfluve between 2 streams draining into the Yuba River, Sierra Nevada mountains, California, USA.*

4. Lastly, you will want to plot the observed topographic profile along with the model prediction to try and fit the observation by varying the uplift rate until you get a similar profile. Add a line in the script to plot the observed data using the `plot()` function. Be sure to use a different line color or pattern so that it is clear which line is the model and which is the data profile. Once you've determined your best-fit uplift rate, add text to the plot to display that rate using the `text()` function. Also, you will want to shift the model profile up about 750 m since the channels in the observed profile are at ~750 m elevation.

**For Problem 2 you should add the following to the end of this document**

1. A copy of the plot for Part 1 of Problem 2 with the 4 calculated values displayed on it.
2. A figure caption as if the figure was in a scientific publication.
3. A 1 paragraph discussion of the implications the results in Part 1 have for mountain hillslopes. What do the various values you have calculated imply for natural systems?
4. A plot comparing the observed and predicted topographic profiles for Part 2 with the landscape uplift rate displayed as text on the plot.
5. A figure caption explaining what is plotted as if it were in a scientific publication.

**As in Problem 1, you should also save a copy of your modified code in your Github repository**.

# Answers
## Problem 1
This is some text. You can use *italics* or **bold** text easily. You may want to read a bit more about [formatting text in Github-flavored Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/). You can see an example of how to display an image with a caption below.

![Text shown if image does not load](Images/sine.png)<br/>
*Figure 3: Sine wave calculated from 0 to 2π*
