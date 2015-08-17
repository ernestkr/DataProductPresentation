MPG Predictor
========================================================
author: Ernest Kurniawan
date: 17 August 2015
transition: rotate
  
<br>
<br>
  
<small>
Course assignment for Coursera  
**Developing Data Products** class  
Part of Data Science Specialization series.
</small>

Motivation
========================================================

**Miles per galon** (MPG) is commonly used as the criteria for buying a car. This application helps predict the car's MPG based on its specifications. Namely, it takes as input the following car properties:
- Car weight
- Horse power
- Number of Cylinders
- Transmission type (automatic/manual)

and perform a prediction on the likely MPG that the car can achieve.

Prediction Method
========================================================
The prediction is done by fitting linear model to the **mtcars** data, which has the structure (32 types of cars with 11 attributes):
<small>

```
'data.frame':	32 obs. of  11 variables:
 $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
 $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
 $ disp: num  160 160 108 258 360 ...
 $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
 $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
 $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
 $ qsec: num  16.5 17 18.6 19.4 17 ...
 $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
 $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
 $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
 $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```
</small>

Prediction Method (continued)
========================================================

In fitting the linear model, we used *mpg* as the outcome, with *cyl*, *hp*, and *wt* as the predictors. Two linear models are created, one for each types of transmission (automatic/manual) as follows.

```r
FitA<-lm(mpg~cyl+hp+wt,subset(mtcars,am==0))
FitM<-lm(mpg~cyl+hp+wt,subset(mtcars,am==1))
```
Depending on the user inputs obtained from the web form, the appropriate linear model will then be used for prediction as follows (assuming *Automatic* transmission):

```r
predict(FitA,data.frame(wt=wtInput,hp=hpInput, cyl=cylInput))
```

Usage and Features
========================================================

The user only need to input the car **weight** and **horse power**, and select the number of **cylinders** and **transmission type** on the web form. The application will then predict the MPG value of the car specified.

To improve the responsiveness of the web interface, the prediction calculation will only be done when the user press the ***Predict!*** button.

Finally, whenever the prediction results in a valid prediction (positive MPG), the predicted MPG value will be displayed accordingly. Otherwise a message **Unable to predict the MPG** is displayed.
