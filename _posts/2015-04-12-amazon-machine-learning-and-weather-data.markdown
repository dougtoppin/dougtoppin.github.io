---
layout: post
title: "Amazon Machine Learning and Weather Data"
date: 2015-04-12 16:50
comments: true
categories: [aws]
description: Amazon Machine Learning and Weather Data
keywords: aws, machinelearning, ml, weatherprediction

---
This is part 1 of a series of posts.

Amazon recently announced a [Machine Learning Facility](http://aws.amazon.com/machine-learning/) (ML) which is a very interesting area to explore in terms of using historical data to predict future values.
In fact, the data does not need to be historical but instead simply represent what is needed to deduce (predict) the results that you need.
Regarding applications for this sort of technology, do you need custom (and complex) rules engines if you have enough input data that can be used to describe the result that you want to predict?
ML predictions can result in a binary value, numeric (produced by regression) and what is called categorical which means the statistical likelihood of each of a list of values.
AWS Machine Learning may be a good way to find out.
I will post my experiences over the next few days with trying out ML as I learn more.

There are a variety of usages for ML that can be imagined such as weather prediction, insurance rate calculations, fraud detection and stock market activity.

I decided to give it a try and weather seems like a reasonable area because there is a lot of historical data that can be easily obtained to make use of with [Weather Underground](http://www.wunderground.com/) being one example.
The data consists of 20 or so columns of various values that are the data points for each day (the EDT column).


    EDT,Max TemperatureF,Mean TemperatureF,Min TemperatureF,Max Dew PointF,MeanDew PointF,Min DewpointF,Max Humidity, Mean Humidity, Min Humidity, Max Sea Level PressureIn, Mean Sea Level PressureIn, Min Sea Level PressureIn, Max VisibilityMiles, Mean VisibilityMiles, Min VisibilityMiles, Max Wind SpeedMPH, Mean Wind SpeedMPH, Max Gust SpeedMPH,PrecipitationIn, CloudCover, Events, WindDirDegrees

It is a good idea to include the column headings as the first row.
ML will ask if this is the case and the process is a bit more streamlined if so.

Here is an example of retrieving historical weather data (365 days) using the DCA airport data location

[ http://www.wunderground.com/history/airport/KDCA/2014/4/13/CustomHistory.html?dayend=13&monthend=4&yearend=2015&req_city=&req_state=&req_statename=&reqdb.zip=&reqdb.magic=&reqdb.wmo=&format=1]( http://www.wunderground.com/history/airport/KDCA/2014/4/13/CustomHistory.html?dayend=13&monthend=4&yearend=2015&req_city=&req_state=&req_statename=&reqdb.zip=&reqdb.magic=&reqdb.wmo=&format=1)

For the weather data I decided to have the prediction be for the mean temperature.
I do not know if this is the best choice or not but seems reasonable first start.
Since I am interested in a single numeric value you can assume that ML will use a regression model to predict the results.

While ML can ignore data that may not be correctly formatted it is a good idea to clean it up yourself before making use of it.
The lessons learned section below details a few experiences encountered during my initial test cases.

Download the data into a csv file and then you may need to change a few things in it before using it with Machine Learning (ML).

* remove any html such as `<br>` at the end of each line if necessary
*  on the first line, remove any embedded blanks in each column name

The method that I am using is to build a model using complete historical data and then try uploading data set that is missing one of the fields for a period of time and see if the model predictions for that field matches actual values in a complete set.

The data used by ML for training (producing the model) can be read by ML via an S3 bucket or from a URL that it can reach.
For my tests I created a specific S3 bucket and stuck my files in it.

If you try to use a bucket that you have not modified the permissions on you should be prompted if AWS can do it for you.
That is a much better user experience than having to go back and do it yourself.

Note that ML automatically sends data to AWS CloudWatch which makes it easier to determine activity levels of your ML environment.
The ML metrics will appear in in `ML` under the Cloud Watch Metrics choice as batch and potentially real time prediction counts if that is enabled, more on that later.
ML may charge based on the prediction related counts so it is a good idea to get familiar with them to ensure that you are not surprised if you start working with large or complex data sets.

In my next post I will include what was involved in training and evaluating and then making use of the model for predictions.

Lessons learned (so far)

* field names need to match a regular expression pattern that does not allow blanks so change fields such as `Max TemperatureF` to `MaxTemperatureF`
* data sets may have missing values, if so you may get something like this after the analysis
   
	Data processing completed. We found the following potential issues with your input data.
	Review your data before you train your ML model. The quality of your data affects the
	quality of your ML model.
	1 of 23 Attributes have missing values
	
	The Weather Underground column `MaxGustSpeedMPH` and `Events` for my test had a number of empty fields in them 



