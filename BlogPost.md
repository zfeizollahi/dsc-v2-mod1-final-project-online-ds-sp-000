
<p align="left">
    
## Everything looks alike
#### a.k.a. measures of data variation and model error 

If you're like me, reading through a lesson on statistics ans machine learning is straightforward and usually makes sense. (So long as the curriculum was well-thought out and explained!). But after a while the terms and concepts jumble together, formulas and greek notation look similar, and my mind starts to boggle. Part of being a data scientist is being able to intelligently explain and use the different measures of variation and error correctly. I often copy paste definitions and formulas that make sense to me, and wanted to make a nice cheat sheet for future reference. Hopefully, this is useful not just to myself but to others. 

#### Measures of dispersion
#### "How spread out is the data, and where does this data point lie w.r.t. the ther rest of the data?"


|<i></i>| Dispersion Term          | Intuition |Steps| Formula |
|---|--------------|------------|--------------------|------|
|1. |<p align="left"> absolute deviation|<p align="left"> how far is this one data point from the mean?|<p align="left">a.subtract the data point from the average<br/> b. remove minus sign for absolute distance| $$ \left|datapoint - {mean}\right| $$ |
|2.|<p align="left"> average absolute deviation |<p align="left">On average how spread out is the data? |<p align="left"> a. do 1 for all data points <br/> b. add them all up <br/> c. take average (i.e. divide by number of data points)| $$ \dfrac{1}{n}\sum^n_{i=1}\left|datapoint - mean\right| $$|
|3.| <p align="left">variance |<p align="left">On average how spread out is the data? <br/> (except units are all messed up because of squaring)|<p align="left"> a. take the square instead of absolute value <br/> b. continue as in 2 |    $$ \dfrac{1}{n}\displaystyle\sum^n_{i=1}(datapoint - mean)^2 $$ |
|4.|<p align="left">standard deviation |<p align="left">On average how spread out is the data? <br/> (except the number is back to 'normal' because of taking the square root) |<p align="left"> a. calculate number 3<br/> b. take the square root| $$ \sqrt{\dfrac{1}{n}\displaystyle\sum^n_{i=1}(datapoint - mean)^2} $$ |
|5.|<p align="left">z-score |<p align="left">How extreme is this result, using a unit (standard deviations) such that we can compare across different types of data?|<p align="left"> a. subtract data point from mean<br/>b. divide by standard deviation (4)| $$ \dfrac{datapoint - mean}{standard\:deviation} $$ |

1. **Absolute Deviation** ask the question "given one single data point, how far is this data point from the mean?" This is the building block for the formulas below. The "absolute" refers to takeing hte absolute value (remove the negative sign) when you calculate the distance from the mean, in the case that the data point is less than the mean. I suppose one could just calculate "deviation" so that the negative sign (below the mean) provided something useful. But if you dont' remove it, when you try to calculate averages over the entire data set, you'll end up with 0. (Try it!) Some formulas take the square instead of absolute value to get around the negative sign / zero problem.


2. **Average Absolute Deviation** simply trying to ask the same question as absolute deviation but for the entire data set. How spread out is this data overall? To do that, we do #1 for all the data points, sum it up, and then find the average amount of distance from the mean (as in divide but total number of data points).


3. **Variance** is basically the same as average absolute deviation, except that we take the square of the distance instead of the absolute value. The only problem here is that the final number you get is much larger than the units you started with. For example, if you were measuring variation in weight, you'd have pounds^ 2 not pounds. That's why we do number 4. 


4. **Standard Deviation** basically converts variance back into a unit that is the same as the data. If we measured pounds, we can say the standard deviation is X pounds. 



5. ***Z*-score** computes a number for a single data point but in a way that we can compare across units. The unit being 1 for the very top value, and 0 being the lowest value in the dataset. So we could compare the z-score of someone's height  and weight. For example, .9 for height, they are super tall! but if they have a .5 for weight that would mean they have a fairly average weight. (Consequently, we'd have to build some sort of height/weight table to figure out .. oh for their height they are actually quite underweight, give the average weight for someone in that height range, but that's another story!)


#### Some other terms related to above to note

One thing to note about standard deviation, is that it is sometimes used as a unit. Lots of data tends to follow a normal gaussian curve - or bell curve you heard of. The  data is has a mean, median and mode that are equal, and often 68% of the data lies within 1 standard deviation from the mean. Meaning, whatever we calculated for standard deviation, 68% of the data \+\/\- that amount from the mean. For example, if we have a mean of 10 dollars and a standard deviation of 5 dollars. 68% of the data lies between $5 - 15.  If someone says something about 0.4 standard deviations, then we can just multiple 0.4 by 5 (standard deviation) and find out that they mean 2 dollars. It's another way of being able to standardize the units and compare regardless of the original units we're using.

### Error: Measures of Dispersion on the model

A lot of formulas below look like the ones we just discussed. However the ones in the previous section are all about the data itself. The ones here are all about how well the model does - hence the term error or "goodness of fit". Meaning the model made a prediction, and we as how far is that prediction from the actual data point. Similar to variance, standard deviation, etc. we want a number that gives the overall average errors, and then do something to make the number something we can compare across models with different types of units.





| <i></i> | Term          | Intuition |Laymen's Explanation| Formula |
|---|---------------|-----------|--------------------|-------|
|1. |<p align="left"> Residual Sum of Squares - RSS|<p align="left"> Error of the model given the prediction |<p align="left"> a. subtract data point from the model prediction<br/> b. square it<br/> c. do for all data points<br/> d. add it up | $$ \sum_i(datapoint - prediction)^2 $$|
|2. |<p align="left"> Total Sum of Squares - TSS | <p align="left">Error of the baseline model (predict mean for everything) |<p align="left"> a. subtract data point from the "prediction" which is just the mean<br/> b. continue as in 1| $$ {\sum_i(datapoint - mean)^2} $$|
|3. |<p align="left"> R-squared - R<sup>2</sup> <br/>(coefficient of variance/determination) |<p align="left"> How good is this model compared to just predicting the mean | <p align="left">a. calculate RSS (1)<br/>b. calculate TSS<br/> c. divide RSS by TSS<br/> d. subtract from 1 |    $$ 1- \dfrac{RSS}{TSS} $$|
|4. |<p align="left">Adjusted Residual Sum of Squares |<p align="left"> Minor adjustment for adding too many indpendent vairables |<p align="left"> a. do all the calculations aabove <br/> b. plug in the numbers, with n=number of samples, k=number of variables in the model| $$ 1 - \dfrac{(1 - R^2)(n - 1)}{n - k - 1} $$  |


1. **RSS - Residual Sum of Squares - Linear Regression Model** - This calculates the total error for the linear regression model. For each data point, take the actual correct value, find what your model predicts, and find how far off it is. So, subtract the actual value from the predicted value. Then we do the normal squaring and adding up for all datapoints. (See what I mean, subtracting Y and squaring and summing, sounds a lot absolute average deviation, variance, and standard deviation). Obviously, you want the error to be a small number.


2. **Total Sum of Squares - Baseline model** The baseline model just predicts mean for every single data point. In a way we're asking, how bad would it be if we were lazy and just predicted the mean for everything? Most of the time, this is a pretty bad idea and the error is likely to be very large.



3.  **R-squared - coefficient of errors** - takes a ratio of the RSS and TSS (and then substracts it from one). But first lets go through each piece. As I mentioned RSS, we want to be small (if it's a good model), and TSS is likely to be pretty big. So if we did well in fitting our model we should get an even smaller number. A small number divided by a big number is going to be an even smaller number. Then we take that small number and subtract from 1. Subtracting a small number from one means that we should end up with something close to one (if the model is good). This way we can also compare across models how well each one got to one.


4. **Adjusted R-squared - coefficient of errors** I'm not even going to attemp to explain the formula for Adjusted R<sup>2</sup>. Sometimes statistians add in things to account for mathy stuff, or real world information like 'don't add too many variables'. Apparently, adding lots of variables makes the R<sup>2</sup> error go up. I guess lots of variables means there's lots of ways to predict incorrectly. Adjusted R<sup>2</sup> simply penalizes additional independent variables. 



It's easy to get overwhelmed with formulas and statistics. The important thing to remember is that statistics is an entire field that people specialize in. Statisticians are constantly evaluating the definitions and formulas trying to make sure that the number we get from those formulas appropriate capture the data and the context about that data. They build on the former concepts but add some mathematical terms to adjust for real world knowledge, difficulty of the problem, dataset size, or to hedge a bit more. (Kinda like saying "Hey, take this number with a grain of salt!"). It's a lot of info to cram into one number. On the one hand we shouldn't be scared of these giant formulas, but by building a formula up from the ground we can understand just what each concept covers and doesn't cover. Stats are great, but if you understand what they mean and how they are used, you can say and understand a lot of about the world, (and even more importantly distinguish what we don't know).

#### Appendix: Not removing the sign results in 0 average deviation/variance

```python
import numpy as np
a = [1,2,3,4,5]
sum(a)```
15
```python
np.mean(a)
```
3.0
```python
def non_abs_average(a):
    b = []
    for i in a:
        b.append(i - np.mean(a))
    return sum(b) / len(b)
non_abs_average(a)
```
0.0


```python

```
