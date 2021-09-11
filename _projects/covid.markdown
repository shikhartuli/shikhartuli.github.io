---
layout: page
title: covid-19
description:
img: /assets/img/covid.PNG
importance: 1
---


<center>
<div>
<h2>Mixed Weibull Model</h2>
<b>Shreshth Tuli</b> (Department of Computing, Imperial College London)<br>

See published papers in <i><a href='https://www.auctoresonline.org/journals/biomedical-research-and-clinical-reviews-/current-issue/1193'>Biomedical Research and Clinical Reviews</a></i> and <i><a href='https://www.sciencedirect.com/science/article/pii/S254266052030055X?via%3Dihub'>Internet of Things</a></i> for more details. 
<br>Source code available on <i><a href='https://github.com/shreshthtuli/covid-19-prediction'>GitHub</a></i> under BSD-2 license.

<br>

For more details please contact the developer at <a href='mailto:shreshthtuli@gmail.com'>shreshthtuli@gmail.com</a>.

<br>
<b>This model is also being used by the National Health Service (NHS) of the United Kingdom. </b>

<br>
<i>The graphs are updated daily using the <a href='https://ourworldindata.org/coronavirus-source-data'>Our World in Data</a> dataset. <br> Last updated <object width="200" height="21" data="plots/lastupdated.txt"></object>

 GMT. </i><br>
</div>

<div class='container_covid_graphs'>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/World_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/World_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/India_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/India_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/United States_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/United States_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/United Kingdom_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/United Kingdom_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Brazil_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Brazil_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Italy_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Italy_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Argentina_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Argentina_total.html"></iframe>

<hr>

<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Russia_pred.html"></iframe>
<iframe width="700" height="500" frameborder="0" scrolling="no" src="plots/Russia_total.html"></iframe>

<hr>

</div>
</center>

## Predicting the Growth and Trend of COVID-19 Pandemic

This study applies an improved mathematical model to analyse and predict the growth of the epidemic. An ML-based improved model has been applied to predict the potential threat of COVID-19 in countries worldwide. We show that using iterative weighting for fitting Generalized Inverse Weibull distribution, a better fit can be obtained to develop a prediction framework. This has been deployed on a cloud computing platform for more accurate and real-time prediction of the growth behavior of the epidemic. Interactive prediction graphs can be seen at the following links:
1. Static model: https://collaboration.coraltele.com/covid/.
2. Dynamic LSTM model: https://collaboration.coraltele.com/covid2/.
3. Multi-peak dynamic model*: https://shreshthtuli.github.io/projects/covid/.

**\* This model is also being used by the National Health Service (NHS) of the UK.**

## Quick installation of real-time prediction webapp

To install and run the dynamic real-time prediction webapp on your server run the following commands:
```
$ git clone https://github.com/shreshthtuli/covid-19-prediction.git
$ mv covid-19-prediction covid
$ chmod +x run.sh
$ ./run.sh
```
To access your server go to $HOSTNAME/covid/ from your browser. The webapp is hosted on https://shreshthtuli.github.io/projects/covid/ where graphs get updated daily based on new data.

## Dataset

We use the <i>[Our World in Data](https://github.com/owid/covid-19-data/tree/master/public/data/)</i> dataset for predicting number of new cases and deaths in various countries.

## Model contributions

### Weibull Distribution
The model uses weibull distribution with the following function:
<div align="center">
<img src="readme/weibull.PNG" width="300" align="middle">
</div>

### Robust Curve Fitting
The model uses robust curve fitting as described in \[1\]. This is to give low weightage to outliers for curve fitting. The iterative loop of robust curve fitting is shown below.
<div align="center">
<img src="readme/Robust_Fitting.png" width="700" align="middle">
</div>

### Dynamic Parameter Updates
The model uses LSTM model to calculate the coefficients of the weibull distribution as described in \[2\]. This is to adapt to the data and give higher weightage to recent data.
<div align="center">
<img src="readme/drawing.png" width="700" align="middle">
</div>

### Mixed Weibull distribution
The model uses mixed weibull model to handle multiple peaks where each peak is modelled using a separate weibull distribution. This is summation of upto four weibull functions as described before but with same <img src="https://latex.codecogs.com/svg.latex?\beta"/> and <img src="https://latex.codecogs.com/svg.latex?\gamma"/> values to share the trend of the virus in a country.

<center>
Without mixed distribution (for UK):
<div class='container_covid_graphs'>
    <img src="readme/uk_daily_old.PNG" width="600">
    <img src="readme/uk_total_old.PNG" width="600">
</div>
With mixed distribution (for UK):
<div class='container_covid_graphs'>
    <img src="readme/uk_daily_new.PNG" width="600">
    <img src="readme/uk_total_new.PNG" width="600">
</div>
</center>

## Developer

[Shreshth Tuli](https://www.github.com/shreshthtuli) (shreshthtuli@gmail.com)

## Cite this work
If you use our static model, please cite:
```
@article{tuli2020predicting,
title = "Predicting the Growth and Trend of COVID-19 Pandemic using Machine Learning and Cloud Computing",
journal = "Internet of Things",
pages = "100--222",
year = "2020",
issn = "2542-6605",
doi = "https://doi.org/10.1016/j.iot.2020.100222",
url = "http://www.sciencedirect.com/science/article/pii/S254266052030055X",
author = "Shreshth Tuli and Shikhar Tuli and Rakesh Tuli and Sukhpal Singh Gill",
}
```
If you use our dynamic model, please cite:
```
@article{tuli2020modelling,
  title={Modelling for prediction of the spread and severity of COVID-19 and its association with socioeconomic factors and virus types},
  author={Tuli, Shreshth and Tuli, Shikhar and Verma, Ruchi and Tuli, Rakesh},
  journal={Biomedical Research and Clinical Reviews},
  year={2020},
  volume={1},
  issue={3},
  doi={10.31579/2692-9406/014}
  publisher={Auctores}
}
```

## References
* **Shreshth Tuli, Shikhar Tuli, Rakesh Tuli and Sukhpal Singh Gill, [Predicting the Growth and Trend of COVID-19 Pandemic using Machine Learning and Cloud Computing.](https://www.sciencedirect.com/science/article/pii/S254266052030055X?via%3Dihub) Internet of Things, ISSN: 2542-6605, Elsevier Press, Amsterdam, The Netherlands, May 2020.** ([Open access link](https://www.medrxiv.org/content/10.1101/2020.05.06.20091900v1))
* **Shreshth Tuli, Shikhar Tuli, Ruchi Verma and Rakesh Tuli, [Modelling for prediction of the spread and severity of COVID-19 and its association with socioeconomic factors and virus types.](https://www.auctoresonline.org/journals/biomedical-research-and-clinical-reviews-/current-issue/1193) Biomedical Research and Clinical Reviews. 1(3); DOI: 10.31579/2692-9406/014.** ([Open access link](https://www.medrxiv.org/content/10.1101/2020.06.18.20134874v1))

