---
title: Is School More Vulnerable to Mass Shootings ?
date: 2018-02-21T01:05:01+00:00
author: jmshi
layout: post
permalink: /school-mass-shootings/
image: /wp-content/uploads/2016/10/bird_nest.png
categories: Data Science
---


### 17 people were killed in the recent high school mass shooting in Parkland, Florida. 27 people were killed in Sandy Hook Elementary massacre in 2012. 32 people were killed in Virginia Tech in 2007. Are you wondering if a school is more vulnerable to such an attack than other places? Does the vulnerability make them potential targets for the murderers?  

In order to answer these questions, I started to look into existing data which covers recent and historic mass shootings and surprisingly found there wasn't much data being collected. The major two I have found are [Mother Jones' investigation] [1] which covered 1982-2018 and focus mostly on shootings that occurred in public space, and [Everytown's analysis] (#2) based on FBI report and CDC firearm data from 2009-2016 with more general scope. Nonetheless, both define a mass shooting as a single attack in which four or more victims were killed. Combining these two datasets, I am able to find 16 school shootings among 166 attacks in total (a python notebook is available [here] [4]). The average number of fatalities per attack in a school is significantly higher than other places:

<iframe width="700" height="500" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/8.embed"></iframe>


The Mother Jones' data also categorizes the venue of the attacks. The following chart shows the number of attacks and the sum of all fatalities by venues. To simplify the analysis, we drop those categorized as 'Other', meaning other than the five main venues displayed here. 

<iframe width="700" height="500" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/6.embed"></iframe>


Attacks occurred in workplace dominates both the total fatalities (173 victims), and number of incidents (28 times). However, the fatality rate of school attacks are much greater than that in the workplace as shown below:

<iframe width="700" height="500" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/4.embed"> </iframe>

It is also worth mentioning that the averaged fatalities in 'Religious', some religious building, is the highest among the five different venues based on somewhat limited samples. 





## cross check between these two datasets

* Binghamton,NY 04-03-2009 mass shooting is listed as a 'School' incident, but not in Mother Jones'
* Santa Monica 6/7/2013 is missing from MotherJones
* The rest are all covered in Mother Jones' report. 

[1]: https://www.motherjones.com/politics/2012/12/mass-shootings-mother-jones-full-data/) 
"US Mass Shootings, 1982-2018: Data From Mother Jones’ Investigation - The full data set from our in-depth investigation into mass shootings."


<a>name="2"</a>[2]: https://everytownresearch.org/reports/mass-shootings-analysis/  
"Everytown's Mass Shooting Analysis"


[3]: https://github.com/nprapps 
"Data analysis for Everytown's mass shooting database"


[4]: http://nbviewer.jupyter.org/gist/jmshi/76b3443353e42b19f59178187adf09ca 
"mother_jones.ipynb"


[5]: https://everytownresearch.org/gun-violence-by-the-numbers/  
"Everytown's Gun Violence by the Numbers"
