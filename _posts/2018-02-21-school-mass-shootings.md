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

In order to answer these questions, I started to look into existing data which covers recent and historic mass shootings and surprisingly found there wasn't much data being collected. The major two I have found are Mother Jones' investigation [<sup>1</sup>](#1) which covered 1982-2018 and focus mostly on shootings that occurred in public space, and Everytown's analysis[<sup>2</sup>](#2)[<sup>3</sup>](#3) based on FBI report and CDC firearm data from 2009-2016 with more general scope. Nonetheless, both define a mass shooting as a single attack in which four or more victims were killed. Combining these two datasets, I am able to find 16 school shootings among 166 attacks in total (a python notebook is available in [<sup>4</sup>](#4)). The average number of fatalities per attack in a school is significantly higher than other places:

[//]: # <iframe width="700" height="500" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/8.embed"></iframe>

<div>
   <a href="https://plot.ly/~jmshi/8/?share_key=lZtunbhrWLIgHwGdU4fPhT" target="_blank" title="mean_fatalities_school_no_school_1" style="display: block; text-align: center;"><img src="https://plot.ly/~jmshi/8.png?share_key=lZtunbhrWLIgHwGdU4fPhT" alt="mean_fatalities_school_no_school_1" style="max-width: 100%;width: 500px;"  width="500" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
       <script data-plotly="jmshi:8" sharekey-plotly="lZtunbhrWLIgHwGdU4fPhT" src="https://plot.ly/embed.js" async></script>
</div>

The Mother Jones' data also categorizes the venue of the attacks. The following chart shows the number of attacks and the sum of all fatalities by venues. To simplify the analysis, we drop those categorized as 'Other', meaning other than the five main venues displayed here. 

[//]: # <iframe width="700" height="500" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/6.embed"></iframe>

<div>
   <a href="https://plot.ly/~jmshi/6/?share_key=V1ZTbTfSV7blzSbbYj22VZ" target="_blank" title="count_sum_fatalities_by_venue" style="display: block; text-align: center;"><img src="https://plot.ly/~jmshi/6.png?share_key=V1ZTbTfSV7blzSbbYj22VZ" alt="count_sum_fatalities_by_venue" style="max-width: 100%;width: 500px;"  width="500" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
       <script data-plotly="jmshi:6" sharekey-plotly="V1ZTbTfSV7blzSbbYj22VZ" src="https://plot.ly/embed.js" async></script>
</div>

Attacks occurred in workplace dominates both the total fatalities (173 victims), and number of incidents (28 times). However, the fatality rate of school attacks are much greater than that in the workplace as shown below:

[//]: # <iframe width="700" height="500" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/4.embed"> </iframe>

<div>
    <a href="https://plot.ly/~jmshi/4/?share_key=QqupdYcyKF16wmXvec5V19" target="_blank" title="mean_fatalities_per_incidents" style="display: block; text-align: center;"><img src="https://plot.ly/~jmshi/4.png?share_key=QqupdYcyKF16wmXvec5V19" alt="mean_fatalities_per_incidents" style="max-width: 100%;width: 500px;"  width="500" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
        <script data-plotly="jmshi:4" sharekey-plotly="QqupdYcyKF16wmXvec5V19" src="https://plot.ly/embed.js" async></script>
</div>

It is also worth mentioning that the averaged fatalities in 'Religious', i.e., some religious buildings, is the highest among the five based on a 
somewhat limited number of samples. 





## Cross check between these two datasets

* Binghamton,NY 04-03-2009 mass shooting is listed as a 'School' incident, but not in Mother Jones'
* Santa Monica 6/7/2013 is missing from MotherJones.
* The rest are all covered in Mother Jones' report. 
 
## Some thoughts

*The results indicate that the attack in an environment such as a school, which is high in crowd density and low in security control, does result in larger fatalities.*

But is this vulnerability being targeted by the criminals? Perhaps we need to know not only those attacks have been carried out, but those attempts that failed. Perhaps we need to study the motives as well. For instance, during the Rancho Tehama shooting spree, the shooter picked a nearby elementary school as his next target after shooting a few neighbors and passers-by [<sup>5</sup>](#5). According to news report, the motive is unclear. The invetigators have not connected the shooter with anyone at the school. It could be very likely that the shooter choose the school to increase its impact. 

## Caveats

The analysis could be biased due to the relatively small number of incidents we are study (thank god!). 


<a id="1"></a> [1]: [US Mass Shootings, 1982-2018: Data From Mother Jones’ Investigation - The full data set from our in-depth investigation into mass shootings.](https://www.motherjones.com/politics/2012/12/mass-shootings-mother-jones-full-data/) 


<a id="2"></a> [2]: [Everytown's Mass Shooting Analysis](https://everytownresearch.org/reports/mass-shootings-analysis/) 


<a id="3"></a> [3]: [Data analysis for Everytown's mass shooting database](https://github.com/nprapps)


<a id="4"></a> [4]:[http://nbviewer.jupyter.org/gist/jmshi/76b3443353e42b19f59178187adf09ca](http://nbviewer.jupyter.org/gist/jmshi/76b3443353e42b19f59178187adf09ca) notebook link 


<a id="5"></a> [3]: [NBC news coverage on Rancho Tehama shootings](https://www.nbcnews.com/news/us-news/gunman-kills-four-wounds-child-school-california-shootings-n820766)

