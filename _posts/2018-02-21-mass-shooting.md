

```python
import numpy as np
import matplotlib
import matplotlib.pyplot as plt
import pandas as pd
from __future__ import division
import plotly.offline
import plotly.plotly as ply
import plotly.figure_factory as ff  # generate table
from plotly.graph_objs import *     # generate bar charts etc.

from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot

%matplotlib inline

init_notebook_mode(connected=True)
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


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


<div id="0827c383-e0f2-4810-975a-d2cd99a18eca" style="height: 260px; width: 700px;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("0827c383-e0f2-4810-975a-d2cd99a18eca", [{"opacity": 0.75, "colorscale": [[0, "#00083e"], [0.5, "#ededee"], [1, "#ffffff"]], "showscale": false, "hoverinfo": "none", "z": [[0, 0, 0, 0], [0.5, 0.5, 0.5, 0.5], [1, 1, 1, 1], [0.5, 0.5, 0.5, 0.5], [1, 1, 1, 1], [0.5, 0.5, 0.5, 0.5], [1, 1, 1, 1]], "type": "heatmap"}], {"yaxis": {"showticklabels": false, "tick0": 0.5, "ticks": "", "gridwidth": 2, "dtick": 1, "zeroline": false, "autorange": "reversed"}, "height": 260, "width": 700, "xaxis": {"showticklabels": false, "tick0": -0.5, "ticks": "", "gridwidth": 2, "dtick": 1, "zeroline": false}, "margin": {"r": 0, "b": 0, "l": 0, "t": 0}, "annotations": [{"xref": "x1", "xanchor": "left", "yref": "y1", "text": "<b>Venue</b>", "align": "left", "y": 0, "x": -0.45, "font": {"color": "#ffffff"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "<b>sum</b>", "align": "left", "y": 0, "x": 0.55, "font": {"color": "#ffffff"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "<b>count</b>", "align": "left", "y": 0, "x": 1.55, "font": {"color": "#ffffff"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "<b>mean</b>", "align": "left", "y": 0, "x": 2.55, "font": {"color": "#ffffff"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "Airport", "align": "left", "y": 1, "x": -0.45, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "5", "align": "left", "y": 1, "x": 0.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "1", "align": "left", "y": 1, "x": 1.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "5.0", "align": "left", "y": 1, "x": 2.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "Military", "align": "left", "y": 2, "x": -0.45, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "38", "align": "left", "y": 2, "x": 0.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "5", "align": "left", "y": 2, "x": 1.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "7.6", "align": "left", "y": 2, "x": 2.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "Other", "align": "left", "y": 3, "x": -0.45, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "381", "align": "left", "y": 3, "x": 0.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "42", "align": "left", "y": 3, "x": 1.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "9.1", "align": "left", "y": 3, "x": 2.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "Religious", "align": "left", "y": 4, "x": -0.45, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "57", "align": "left", "y": 4, "x": 0.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "5", "align": "left", "y": 4, "x": 1.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "11.4", "align": "left", "y": 4, "x": 2.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "School", "align": "left", "y": 5, "x": -0.45, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "162", "align": "left", "y": 5, "x": 0.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "16", "align": "left", "y": 5, "x": 1.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "10.1", "align": "left", "y": 5, "x": 2.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "Workplace", "align": "left", "y": 6, "x": -0.45, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "173", "align": "left", "y": 6, "x": 0.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "28", "align": "left", "y": 6, "x": 1.55, "font": {"color": "#000000"}, "showarrow": false}, {"xref": "x1", "xanchor": "left", "yref": "y1", "text": "6.2", "align": "left", "y": 6, "x": 2.55, "font": {"color": "#000000"}, "showarrow": false}]}, {"linkText": "Export to plot.ly", "showLink": true})});</script>



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


<div id="3c270e47-0269-4995-8450-d1068c0bf64f" style="height: 500px; width: 700px;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("3c270e47-0269-4995-8450-d1068c0bf64f", [{"y": [5.0, 7.6, 11.4, 10.1, 6.2], "width": [0.5, 0.5, 0.5, 0.5, 0.5], "type": "bar", "marker": {"color": ["rgb(145,191,219)", "rgb(145,191,219)", "rgb(145,191,219)", "rgba(222,45,38,0.8)", "rgb(145,191,219)"]}, "x": ["Airport", "Military", "Religious", "School", "Workplace"]}], {"width": 700, "autosize": false, "height": 500, "title": "Mean # of Fatalities per Incident"}, {"linkText": "Export to plot.ly", "showLink": true})});</script>



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


<div id="f30db5fe-3d2c-4efe-84ca-4b18dfd49350" style="height: 500px; width: 700px;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("f30db5fe-3d2c-4efe-84ca-4b18dfd49350", [{"name": "Count", "width": [0.4, 0.4, 0.4, 0.4, 0.4], "y": [1, 5, 5, 16, 28], "x": ["Airport", "Military", "Religious", "School", "Workplace"], "type": "bar", "marker": {"color": ["rgb(190,191,219)", "rgb(190,191,219)", "rgb(190,191,219)", "rgba(250,45,38,0.8)", "rgb(190,191,219)"]}}, {"name": "Sum", "width": [0.4, 0.4, 0.4, 0.4, 0.4], "y": [5, 38, 57, 162, 173], "x": ["Airport", "Military", "Religious", "School", "Workplace"], "type": "bar", "marker": {"color": ["rgb(145,191,219)", "rgb(145,191,219)", "rgb(145,191,219)", "rgba(210,45,38,0.8)", "rgb(145,191,219)"]}}], {"width": 700, "autosize": false, "height": 500, "title": "# of Mass Shootings and Total # of Fatalities"}, {"linkText": "Export to plot.ly", "showLink": true})});</script>


# CDC data
* [Everytown's Gun Violence by the Numbers](https://everytownresearch.org/gun-violence-by-the-numbers/)
* [Everytown's Mass Shooting Analysis](https://everytownresearch.org/reports/mass-shootings-analysis/)
* [Data analysis for Everytown's mass shooting database](https://github.com/nprapps)



```python
fname='CDC_MassShooting_2009-2016.csv'
df_cdc=pd.read_csv(fname)
```


```python
df_cdc_school=df_cdc.groupby('School')['Number Killed [CALCULATED]'].agg(['count','sum'])
df_cdc_school
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>sum</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>No</th>
      <td>150</td>
      <td>783</td>
    </tr>
    <tr>
      <th>Yes</th>
      <td>6</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>



## cross check between these two datasets

* Binghamton,NY 04-03-2009 mass shooting is listed as a 'School' incident, but not in Mother Jones'
* Santa Monica 6/7/2013 is missing from MotherJones
* The rest are all covered in Mother Jones' report. 


```python
print(len(df[df['Venue']=='School']))
print(len(df_cdc[df_cdc['School']=='Yes']))
```

    16
    6


# Combine CDC and MotherJones


```python
df_cdc[df_cdc['School']=='Yes']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>City</th>
      <th>State</th>
      <th>Listed in FBI SHR (2009-2012)</th>
      <th>TOTAL SHOT (Not Including Shooter)</th>
      <th>Number Killed [CALCULATED]</th>
      <th>Number Injured</th>
      <th>Females Killed</th>
      <th>Males Killed</th>
      <th>Children Killed (17 and Under)</th>
      <th>...</th>
      <th>School</th>
      <th>Workplace</th>
      <th>Multiple</th>
      <th>Other (Note)</th>
      <th>Solely Home But Not DV [CALCULATED]</th>
      <th>Red Flag</th>
      <th>Subsequent FBI Terrorism Investigation</th>
      <th>Public Space</th>
      <th>Gun-Free Zone</th>
      <th>Took place exclusively in private residence(s)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>4/3/09</td>
      <td>Binghamton</td>
      <td>NY</td>
      <td>Yes</td>
      <td>17</td>
      <td>13</td>
      <td>4</td>
      <td>11</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>65</th>
      <td>4/2/12</td>
      <td>Oakland</td>
      <td>CA</td>
      <td>Yes</td>
      <td>7</td>
      <td>7</td>
      <td>0</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>79</th>
      <td>12/14/12</td>
      <td>Newtown</td>
      <td>CT</td>
      <td>No</td>
      <td>29</td>
      <td>27</td>
      <td>2</td>
      <td>19</td>
      <td>8</td>
      <td>20</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>89</th>
      <td>6/7/13</td>
      <td>Santa Monica</td>
      <td>CA</td>
      <td>NaN</td>
      <td>9</td>
      <td>5</td>
      <td>4</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>Yes</td>
      <td>home, road, school</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>113</th>
      <td>10/24/14</td>
      <td>Marysville</td>
      <td>WA</td>
      <td>NaN</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>4</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>136</th>
      <td>10/1/15</td>
      <td>Roseberg</td>
      <td>OR</td>
      <td>NaN</td>
      <td>18</td>
      <td>9</td>
      <td>9</td>
      <td>3</td>
      <td>6</td>
      <td>0</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
<p>6 rows × 49 columns</p>
</div>




```python
binary_df = pd.DataFrame(df_cdc_school)
binary_df.loc['Yes']=sum_per_venue.iloc[4]  
binary_df['mean'] = binary_df['sum']/binary_df['count']

binary_df.round(1)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>No</th>
      <td>150</td>
      <td>783</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>Yes</th>
      <td>16</td>
      <td>162</td>
      <td>10.1</td>
    </tr>
  </tbody>
</table>
</div>




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


<div id="edeb60bb-7cb7-4a97-ace5-c6de8bdd0aca" style="height: 500px; width: 700px;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("edeb60bb-7cb7-4a97-ace5-c6de8bdd0aca", [{"orientation": "h", "width": [0.5, 0.5], "y": ["Not School", "School"], "x": [5.22, 10.125], "type": "bar", "marker": {"color": ["rgb(145,191,219)", "rgba(222,45,38,0.8)"]}}], {"width": 700, "autosize": false, "height": 500, "title": "Mean # of Fatalities per Incident: School vs. Not School"}, {"linkText": "Export to plot.ly", "showLink": true})});</script>



```python

```
