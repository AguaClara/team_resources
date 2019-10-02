# AguaClara Research Report & Manual Template
#### Natalie Mottl, William Pennock, Janak Shah, and Jillian Whiting
#### February 20, 2019

<!-- Template Description -->
This template will lay out all possible sections that could be used for a research report and manual. All research reports and manuals should strive to comply with this template, but not all sections will be relevant to all teams. In order to use this template, copy this file from the AguaClara team resources repository to your team's repository, and rename it for your team in a format similar to  "[Team Name] [Semester]". An example would be "Filter and Treatment Train Flow Control Spring 2017." For guidance on writing Markdown documents, refer to the [AguaClara Tutorial wiki pages](https://aguaclara.github.io/aguaclara_tutorial/). Once you are ready to write your report, please delete this description and everything above.

# Team Name, Semester Year
#### Authors
#### Date

## Abstract
Briefly summarize your previous work, goals and objectives, what you have accomplished, and future work. (100 words max)

## Introduction
Explain how the completion of your challenge will affect AguaClara and the mission of providing safe drinking water (or sustainable wastewater treatment!). If this is a continuing team, how will your contribution build upon previous research? What needs to be further discovered or defined? If this is a new team, what prompted the inclusion of this team?

## Literature Review and Previous Work
Discuss what is already known about your research area based on both external work and that of past AguaClara Teams. Connect your objectives with what is already known and explain what additional contribution you intend to make. Make sure to add APA formatted in-text citations. If you mention the author(s) in your sentence, you can simply give the year of publication. [(Logan et. al. 1987)](http://www.jstor.org/stable/pdf/25043431.pdf?acceptTC=true)


## Methods
Explain the techniques you have used to acquire additional data and insights. Reserve fine detail for the Manual at the end of the report, but use this section to give an overview with enough detail for the reader to understand your Results and Analysis. Be especially careful to detail the conditions your experiments were conducted under, as this information is especially important for interpreting your results.

Below, some example sections are given. Sectioning the report is meant to keep similar information together.  Continue making sections as necessary, or delete sections if you do not need them. Feel free to add subsubsections to further delineate the information. For example, under the Experimental Apparatus section below, the EStaRS team might consider having sections such as "Filter Design" and "Filter Fabrication".

### Experimental Apparatus
Describe your apparatus and justify every decision you made and every parameter you chose in its design. Explain your apparatus setup using enough detail such that future teams can recreate it.

Make sure to include:

* Design calculations
  * Use [LaTeX](https://www.overleaf.com/learn/latex/Mathematical_expressions) to format mathematical equations. LaTeX equations can be written in-line ($x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$) or as equation elements:

  \[x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\]  

 * Schematic drawing
   * Clearly labeled components, flow paths, sensors, and reactor geometry.

  <center>
    <img src="/Images/Example Schematic.png" height=300>
  </center>

  <center>
    Figure 1. Above is an example schematic drawing of the Summer 2018 High Rate Sedimentation apparatus. It is labeled with components, flow paths, sensors, and reactor geometry.
  </center>

* Labeled images


  <center>
    <img src="/Images/Example Lab Image.JPG" height=300>
  </center>
  <center>
    Figure 2. Above is an example image of the Summer 2018 High Rate Sedimentation apparatus. All photos should be clearly labeled and captioned.
  </center>

  | Label | Component             | Label | Component             |
  |:-----:|:--------------------- |:-----:|:--------------------- |
  |   1   | Water Pump            |   8   | Effluent Turbidimeter |
  |   2   | Clay Pump             |   9   | Pressure Attenuator   |
  |   3   | Coagulant Pump        |  10   | Coagulant Stock       |
  |   4   | Waste Pump            |  11   | Clay Stock            |
  |   5   | Flocculator           |  12   | Sedimentation Tank    |
  |   6   | Pressure Sensor       |  13   | Waste Tube            |
  |   7   | Influent Turbidimeter |       |                       |

### Procedure
Discuss your experimental procedure. How did you run your experiment? What were you testing? What were the values of relevant parameters?

## Results and Analysis
Present an observation (results), then explain what happened (analysis).  Each paragraph should focus on one aspect of your results and interpret that result. In other words, there should not be two distinct paragraphs, but one paragraph containing one result and the interpretation and analysis of this result. Here are some guiding questions for results and analysis:

When describing your results, present your data, using the guidelines below:
* What happened? What did you find?
* Show your experimental data in a professional way (see [Figure Requirements](#figure-requirements)).

After describing a particular result, within a paragraph, go on to connect your work to fundamental physics, chemistry, statics, fluid mechanics, or whatever field is appropriate. Analyze your results and compare with theoretical expectations; or, if you have not yet done the experiments, describe your expectations based on established knowledge.
* Why did you get those results/data?
* Did these results line up with expectations?
* What went wrong?
* If the data do not support your hypothesis, is there another hypothesis that describes your new data?

Include implications of your results. How will your results influence the design of AguaClara plants? If possible provide clear recommendations for design changes that should be adopted.

### Figure requirements
The [Data Analysis in Python](https://aguaclara.github.io/aguaclara_tutorial/python/data-analysis.html) page of the AguaClara Tutorial wiki pages shows how to create graphs in Python to meet these requirements. Make sure to read the sections on [Plotting with Matplotlib](https://aguaclara.github.io/aguaclara_tutorial/python/data-analysis.html#plotting-with-matplotlib) and, if you are working with ProCoDA data files, [Reading ProCoDA Data with the AguaClara Package](https://aguaclara.github.io/aguaclara_tutorial/python/data-analysis.html#reading-procoda-data-with-the-aguaclara-package).

Basics
- Create your graphs using Python. Include the code for your graph in the [Python Code](#python-code) section of your report.
- Place a caption with a brief description below the graph. Add this caption using the wiki formatting, not in your graphing software.
- Insert the graph in your report after the first paragraph with a reference to it.

Appearance
- Use a white background.
- Use the same font in the graphs as you use in the text of the report.
- Scale the size of the graph so it is large enough to see the data and read the text without having to follow a link to see a larger image. Avoid using hyperlinks on images, because an export to Microsoft Word will not include the image.

 Axes
 - Data with x and y values should be presented using an xy scatter plot.
 - Label all axes and include units.
 - Axis scale labels should be in the margin of the graph, not inside the graph border.
 - If the x-axis is time, then make time zero the beginning of the test.
 - Eliminate ranges of the x and y axes that are not used or meaningful.

Data Representation
 - Use data symbols, not a line, to show discrete data points.
 - However, if there is so much data that the symbols overlap, it is better to connect the data points with a line and not show the data symbols.

Multiple Plots
 - When presenting multiple plots on a single graph make sure that it is easy to distinguish the plots using the legend.

Curve Fitting
 - If curve fitting is used, explain why and include the equation elsewhere in the report.
 - The model or theoretical curve should be a smooth curve without data points.

Here is an example graph:

 <center>
   <img src="/Images/Turbidity.png">
 </center>

 Figure 3. Descriptive captions are very important for figures. The code used to create this graph can be found in the [Python Code](#python-code) section of this report.


## Conclusions
Explain what you have learned and how that influences your next steps. Why does what you discovered matter to AguaClara?

Make sure that you have defended your conclusions with facts and results.

## Future Work
Describe your plan of action for the next several weeks of research. Detail the next steps for this team. How can AguaClara use what you discovered for future projects? Your suggestions for challenges for future teams are most welcome. Should research in this area continue?

## Bibliography
Logan, B. E., Hermanowicz, S. W., & Parker,A. S. (1987). A Fundamental Model for Trickling Filter Process Design. Journal (Water Pollution Control Federation), 59(12), 1029–1042.

# Manual
The goal of this section is to provide all of the guidance that would be necessary for a future team to pick up your work where you left off. Please try to be thorough and put yourselves in the shoes of a newcomer to the project. Below are some recommended sections, but the manual will likely take a slightly different form for each team.

## Fabrication Details
Include any information related to the fabrication of equipment, technologies, or experimental apparatuses, such as

* materials, with dimensions
* fabrication methods and the purpose of each step
* complications and constraints in construction
* revisions made to a previous design, with a reference to the report where the design is described
* appropriate safety precautions

## Special Components
If your subteam uses a particular part that is unique and you could foresee a future subteam needing to order it or learn more about it, please include basic information such as its vendor, its catalog/item number, and a link to any documentation.

## Experimental Methods
### Set-up
Step 1.
* Put tasks in a sequential order.
* It is okay to have sub-lists.
  - Like this.

### Experiment
Step 1.

### Cleaning Procedure
Step 1.

## Experimental Checklist
Another potential section could include a list of things that you need to check before running an experiment.

## ProCoDA Method File

**Upload your ProCoDA method file to your Github repository and provide a [link]() it in your report.**

Use the rest of this section to explain your method file. Your explanation can be broken up into several components as shown below:

### States
Here, you should describe the function of each state in your method file, both in terms of its overall purpose and also in terms of the details that make it distinct from other states. For example:

 - **OFF**: Resting state of ProCoDA. All sensors, relays, and pumps are turned off.

### Set Points
Here, you should list the set points used in your method file and explain their use as well as how each was calculated.

## Python Code

In this section, provide any code that was a significant part of your research, including in making theoretical calculations, determining parameters for your experiment, or analyzing your data.

**Note: your code should be able to run as is in your report. This means any files you reference should have the correct paths/URL's, so that anybody can run the code in your report and find the same results.**

### Code for Figure 3

```python
import aguaclara as ac
from aguaclara.core.units import u
import matplotlib.pyplot as plt

path = "https://raw.githubusercontent.com/AguaClara/team_resources/master/Data/datalog%206-14-2018.xls"

time = ac.column_of_time(path=path, start=2250, end=5060).to(u.hr)
influent_turbidity = ac.column_of_data(path=path, start=2250, column=3, end=5060)
effluent_turbidity = ac.column_of_data(path=path, start=2250, column=4, end=5060)

# set up multiple subplots with same x-axis
fig, ax1 = plt.subplots()
ax2 = ax1.twinx()

# make the first subplot (Effluent Turbidity vs Time)
ax1.set_xlabel("Time (hours)")
ax1.set_ylabel("Effluent Turbidity (NTU)")
line1, = ax1.plot(time, effluent_turbidity, color="blue")

# make the second subplot (Influent Turbidity vs Time)
ax2.set_ylabel("Influent Turbidity (NTU)")
ax2.set_ylim(60,120)
line2, = ax2.plot(time, influent_turbidity, color="green")

plt.legend((line1, line2), ("Effluent", "Influent"))
```

### Code for Experimental Design

Make sure variables in your code, as well as anything that might not be easily understood by a newcomer, is well commented. Also include the outputs of your code, if applicable and not given earlier in the report.

```python
import aguaclara as ac
from aguaclara.core.units import u

# volume per revolution flowing from the pump for PACl (coagulant) stock
vol_per_rev_PACl = ac.vol_per_rev_3_stop("yellow-blue")
# revolutions per minute of PACl stock pump
rpm_PACl = 3 * u.rev/u.min
# flow rate from the PACl stock pump
Q_PACl = ac.flow_rate(vol_per_rev_PACl, rpm_PACl)

# desired system flow rate
Q_sys = 2 * u.mL/u.s
# desired system concentration of PACl
C_sys = 1.4 * u.mg/u.L
# a variable representing the reactor and its parameters
reactor = ac.Variable_C_Stock(Q_sys, C_sys, Q_PACl)

# required concentration of PACl stock
C_stock_PACl = reactor.C_stock()
# concentration of purchased PACl super stock in lab
C_super_PACl = 70.28 * u.g/u.L
# dilution factor of PACl super stock necessary to achieve PACl stock
# concentration (in L of super stock per L water)
dilution = reactor.dilution_factor(C_super_PACl)
mL_per_L = dilution * 1000

print("A reactor with a system flow rate of", Q_sys, ",")
print("a system PACl concentration of", C_sys, ",")
print("and a PACl stock flow rate of", Q_PACl)
print("will require a dilution factor of", round(mL_per_L.magnitude, 3),
  "milliliters of PACl super")
print("stock per liter of water for the PACl stock.")
```

Output:

A reactor with a system flow rate of 2 milliliter/second, a system PACl concentration of 1.4 milligram/liter, and a PACl stock flow rate of 0.007442 milliliter/second will require a dilution factor of 5.353 milliliters of PACl super stock per liter of water for the PACl stock.


<!-- DELETE THIS SECTION BEFORE SUBMITTING -->
----------------------------------------------
## Add/Delete/Change this Template as you see Fit
When using this template keep in mind that this serves three purposes. The first is to provide your team feedback on your progress, assumptions, and conclusions. The second is to keep your team focused on what you are learning and doing for AguaClara. Another is to educate future teams on what you've learned and done. This document should be comprehensive, consistent, and well-written. With that in mind, add, subtract, or move sections. Reach out to the RAs and graders for help with figuring out what should or shouldn't include. Focus on how wonderful a reference you are making through this and work hard on communicating amongst yourselves and with future teammates.

## Converting this Document to a PDF

1. Make sure you are opening this document in **Atom** and that you have installed the package **Markdown Preview Enhanced** (not Markdown Preview or Markdown Preview Plus).
2. Open the formatted preview with ``(Ctrl + Shift + M)``.
3. Right click on the formatted preview and click on “Open in Browser”.
4. Right click on the browser page and click on “Print…”.
5. Change the Destination to “Save as PDF”, then click Save/Print.
