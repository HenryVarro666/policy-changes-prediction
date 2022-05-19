# Policy-Changes-Prediction

DATA605 big data system project

Predict National Policy Changes based on Case Data

<!--more-->

## Policy Data

Data Source:

[OxCGRT/covid-policy-tracker](https://github.com/OxCGRT/covid-policy-tracker)



## Two policy
![State and National](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519000951.png)

### **National Policy**
(We can focus on state policy as well, but we use national policy as an example. It is more clean and more complete)

![National Policy Screenshot](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220518235833.png)

After cleaning, we get a dataset about "Date", "Strictness Level" and "Policy".
![Date + Level + Policy](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519000524.png)

The number reveals the levels of strictness
|Number|Meaning|
|---|---|
|1.0|Low|
|2.0|Medium|
|3.0|High|
|NaN|No data|


#### How can we know when the policy changed?


Because it is national policy data, it won't change frequently.


The number of rows means the days in 2022. (Each row represent one day)

All I need to do is calculate the difference between each two day and find the variances.

```python
dfNP.loc[:,'C1_School closing'].rolling(window=2).apply(lambda x: x.iloc[1] - x.iloc[0]).unique()
```
The output is ` array([nan,  0.]) `, which means it haven't changed from beginning to the present.

To compare the results, we list c4.
```python
dfNP.loc[:,'C4_Restrictions on gatherings'].rolling(window=2).apply(lambda x: x.iloc[1] - x.iloc[0]).unique()
```
The output is ` array([nan,  0.,-2.]) `, which means it changed and skipped 2 levels.

We mark the row where the differences are not 0, and we get the date when the policy changes.
![Policy Changes Date](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519003247.png)


#### Since the number of level is so small, how can we make it visualiable?
Use the  difference times total case.

Most differences are 1.0. 

We can do fusion and plot the policy and cases in one graph.



## COVID Case Data


### Main source

[United States COVID-19 Cases and Deaths by State over Time](https://data.cdc.gov/Case-Surveillance/United-States-COVID-19-Cases-and-Deaths-by-State-o/9mfq-cb36/data)

It provides csv file.
![CDC screenshot](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519000125.png)



#### Backup datasets

-  [CSSEGISandData/COVID-19](https://github.com/CSSEGISandData/COVID-19)

      (Messy)

      Novel Coronavirus (COVID-19) Cases, provided by JHU CSSE

- [C~~OVID-19 Open Research Dataset Challenge (CORD-19)~~](https://www.kaggle.com/datasets/allen-institute-for-ai/CORD-19-research-challenge)

  CORD-19 is a resource of over 1,000,000 scholarly articles, including over 350,000 with full text, about COVID-19, SARS-CoV-2, and related coronaviruses. 

- [nytimes/covid-19-data](https://github.com/nytimes/covid-19-data)

  <u>Only foucs on USA</u>

  An ongoing repository of data on coronavirus cases and deaths in the U.S.

- [pcm-dpc/COVID-19](https://github.com/pcm-dpc/COVID-19)

  Only focus on **Italy**

  COVID-19 Italia - Monitoraggio situazione (not English?)

- [owid/covid-19-data](https://github.com/owid/covid-19-data)

  Looks good~ But not so reliable.


### Case Data
![Case Data](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519003444.png)

After sorted by submission date, We can draw a graph based on new cases data.
![New case](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519003803.png)

#### Why is it so rough? Can we make it more smoother?
Weekend (except some missing data)

Count the mean number of each 20 days.
![New case MA 20](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519004232.png)
It is really good.


## Fusion
```python
matplotlib.rcParams['figure.figsize'] = [15, 10]
dfC_proc.plot(x='submission_date',y=polColumns+['new_case_MA20'])
# <AxesSubplot:xlabel='submission_date'>
```


![2020 added](https://raw.githubusercontent.com/HenryVarro666/images/master/images/20220519013243.png)


In this graph, we can clearly tell the trend of new cases and when the policies changed.

> First Omicron in US:November 2021 (11/22/2021)[First Confirmed Case of Omicron Variant Detected in the United States](https://www.cdc.gov/media/releases/2021/s1201-omicron-variant.html)


## Conclusion
1. Normally, it takes one month to respond.
2. Last peak was caused by Omeicron.
3. We can speculate that new policy changes will happen in June.

----
## 4Vs
### Volume
Total datasets are up to 500 MB.
The experiment dataset contains 400000 rows and 87 columns.

### Variety
Policy and Case.
But it includes so many different datasets.

### Velocity
Though it was reported that "Java heap space", it runs fast and is almost real-time.

### Veracity
Those two sources are reliable.
(CDC and [OxCGRT](https://www.bsg.ox.ac.uk/research/research-projects/covid-19-government-response-tracker))

