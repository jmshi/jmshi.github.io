---
title: school mass shootings
date: 2018-02-21T01:05:01+00:00
author: jmshi
layout: post
permalink: /school-mass-shootings/
image: /wp-content/uploads/2016/10/bird_nest.png
categories:
  - Data Science
tags:
  - mass shooting
---


<h1><center>Is School More Vulnerable to Mass Shootings ? </center></h1>


### 17 people were killed in the recent high school mass shooting in Parkland, Florida. 27 people were killed in Sandy Hook Elementary massacre in 2012. 32 people were killed in Virginia Tech in 2007. Is the school more vulnerable to such an attack than other places? Does the vulnerability make them potential targets for the murderers?  


<iframe width="900" height="800" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/8.embed"></iframe>

# Data from MotherJones
* [US Mass Shootings, 1982-2018: Data From Mother Jones’ Investigation](https://www.motherjones.com/politics/2012/12/mass-shootings-mother-jones-full-data/) --The full data set from our in-depth investigation into mass shootings.
 by Mark Follman, Gavin Aronsen and Deanna Pan


```python
fname='MotherJones_MassShooting_1982-2018.csv'
df = pd.read_csv(fname,converters={"Fatalities":int})

# correct a few indices
df.loc[df['Venue'] == '\nWorkplace', 'Venue'] = 'Workplace'
df.loc[df['Venue'] == 'Other\n', 'Venue'] = 'Other'
df.groupby(['Venue'])['Fatalities'].agg({'Fatalities': ['sum']})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Fatalities</th>
    </tr>
    <tr>
      <th></th>
      <th>sum</th>
    </tr>
    <tr>
      <th>Venue</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Airport</th>
      <td>5</td>
    </tr>
    <tr>
      <th>Military</th>
      <td>38</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>381</td>
    </tr>
    <tr>
      <th>Religious</th>
      <td>57</td>
    </tr>
    <tr>
      <th>School</th>
      <td>162</td>
    </tr>
    <tr>
      <th>Workplace</th>
      <td>173</td>
    </tr>
  </tbody>
</table>
</div>




```python
#df.loc[df['Venue'] == 'Other']['Sources'][2]
sum_per_venue.index
```




    Index([u'Airport', u'Military', u'Other', u'Religious', u'School',
           u'Workplace'],
          dtype='object', name=u'Venue')




```python
sum_per_venue=df.groupby(['Venue'])['Fatalities'].agg(['sum'])
count_per_venue=df.groupby(['Venue']).agg('count')['Case']
```


```python
sum_per_venue['count'] = count_per_venue
sum_per_venue['mean'] = np.around(sum_per_venue['sum']/count_per_venue,decimals=1)
sum_per_venue['Venue'] = sum_per_venue.index
sum_per_venue = sum_per_venue.reindex(columns=['Venue','sum','count','mean'])
table = ff.create_table(sum_per_venue,height_constant=30)
table.layout.width=700
#ply.iplot(table, filename='table1')
iplot(table, filename='table1')
```


<iframe width="900" height="800" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/2.embed"></iframe>



```python
#sum_per_venue.iloc[:,2].plot(kind='bar')
df_mj = sum_per_venue.drop(['Other'])

ctable = ['rgb(145,191,219)']*5
ctable[3] = 'rgba(222,45,38,0.8)'
width = list(np.full(5,0.5))

data = [Bar(x=df_mj['Venue'],
            y=df_mj['mean'],marker=dict(color=ctable),width=width)]

layout = Layout(autosize=False,width=700,height=500, title='Mean # of Fatalities per Incident')
         #margin=Margin(l=20,r=20,b=20,t=20,pad=4),
         #paper_bgcolor='#7f7f7f',
         #plot_bgcolor='#c7c7c7')
fig = Figure(data=data,layout=layout)
#ply.iplot(fig, filename='mean_fatalities_per_incidents')
iplot(fig, filename='mean_fatalities_per_incidents')
```


<iframe width="900" height="800" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/4.embed"></iframe>


```python
#sum_per_venue.plot.barh(y=['sum','count'],stacked='True',colormap='jet')
ctable1 = ['rgb(145,191,219)']*5
ctable1[3] = 'rgba(210,45,38,0.8)'
ctable2 = ['rgb(190,191,219)']*5
ctable2[3] = 'rgba(250,45,38,0.8)'
width = list(np.full(5,0.4))

data1 = Bar(x=df_mj['Venue'],
            y=df_mj['sum'],marker=dict(color=ctable1),width=width,name='Sum')
data2 = Bar(x=df_mj['Venue'],
            y=df_mj['count'],marker=dict(color=ctable2),width=width,name='Count')

layout = Layout(autosize=False,width=700,height=500, title='# of Mass Shootings and Total # of Fatalities')
         #margin=Margin(l=20,r=20,b=20,t=20,pad=4),
         #paper_bgcolor='#7f7f7f',
         #plot_bgcolor='#c7c7c7')
data=[data2,data1]
fig = Figure(data=data,layout=layout)
#ply.iplot(fig, filename='count_sum_fatalities_by_venue')
iplot(fig, filename='count_sum_fatalities_by_venue')
```


<iframe width="900" height="800" frameborder="0" scrolling="no" src="//plot.ly/~jmshi/6.embed"></iframe>


# CDC data
* [Everytown's Gun Violence by the Numbers](https://everytownresearch.org/gun-violence-by-the-numbers/)
* [Everytown's Mass Shooting Analysis](https://everytownresearch.org/reports/mass-shootings-analysis/)
* [Data analysis for Everytown's mass shooting database](https://github.com/nprapps)



## cross check between these two datasets

* Binghamton,NY 04-03-2009 mass shooting is listed as a 'School' incident, but not in Mother Jones'
* Santa Monica 6/7/2013 is missing from MotherJones
* The rest are all covered in Mother Jones' report. 


# Combine CDC and MotherJones






```python
binary_df = pd.DataFrame(df_cdc_school)
binary_df.loc['Yes']=sum_per_venue.iloc[4]  
binary_df['mean'] = binary_df['sum']/binary_df['count']

binary_df.round(1)
```






```python
ctable = ['rgb(145,191,219)','rgba(222,45,38,0.8)']
width = list(np.full(2,0.5))

data = [Bar(y=['Not School','School'],x=binary_df['mean'],orientation='h',marker=dict(color=ctable),width=width)]

layout = Layout(autosize=False,width=700,height=500, title='Mean # of Fatalities per Incident: School vs. Not School')
         #margin=Margin(l=20,r=20,b=20,t=20,pad=4),
         #paper_bgcolor='#7f7f7f',
         #plot_bgcolor='#c7c7c7')
fig = Figure(data=data,layout=layout)
#ply.iplot(fig, filename='mean_fatalities_school_no_school')
iplot(fig, filename='mean_fatalities_school_no_school')
```
