# Flight delays project

![Network _map](https://github.com/usermarat/Flight_delays_project/assets/87779469/a9162128-d03d-4d6c-b53c-172f50a73180)

This is the final data-science project I made at the completion of Data Analyst School provided by Sberbank Corporate University.

It is based on Kaggle dataset consisting of logs for the all domestic flights in the USA for the year of 2015 gathered by The U.S. Department of Transportation's Bureau of Transportation Statistics.

The whole dataset is about 600 MB size and has approximately 6 million rows which hold information about all big commercial flights (flight number, origin/destination, airline, timetable, delay/cancellation etc. - something like 30 features): 

https://www.kaggle.com/datasets/usdot/flight-delays

## Project goals

I was given 3 side tasks concerning proper EDA and the one big goal - to build a ML model which predicts flights' delays and results in making suggestion of the three top destination airports based on the smallest prediction of flight delays, given the information of the origin airport. The proposed metric for the model evaluation is RMSE.

## Approaches & results

The notebook [EDA_model_training](https://github.com/usermarat/Flight_delays_project/blob/main/EDA_model_training.ipynb) is where the most of the work was done:
* first part consists of understanding the data, converting to the correct format, working with missing values, datetime etc., also there was a problem with incorrect airports' codes fillings which affected significant part of data logs - basically for the whole month of October instead of correct IATA codes there were some digits without any key-value mapping provided, so I was challenged with a riddle of breaking the code in order to clean messy data
* the next part is EDA and data visualisation
* I decided to take some steps further in analysis and dataviz and applied my knowledge in network analysis to reconstruct all flights' connections as a network with airports as a nodes and connecting flights as an edges - different measures of centrality for all the nodes were calculated as well as for the edges, also the network itself was pictured - the image you can see at the preambule
* at the next parts I'm solving side tasks such as 'find the airport with the smallest departure delay' and so on of this kind with standart data analysis approaches
* at last parts I was going through standart ML modeling pipline: feature generation (in addition to the given features I added above mentioned measures of centrality calculated for the network), train/test splitting, model choosing, cross-validating and hyper-parameters fine-tuning, and at last evaluating the final model with the best parameters on the test data. For the model I choosed plain linear regression as a baseline, linear regression with regularisation (elasticnet) and a catboost gradient boosting implementation. For the other models variety my choice was restricted due to the size of the real data (final feauture dataset reached more than 2 Gb) and absence of the resources which can process such data quickly and efficiently. The catboost model I trained using google colab's gpu, which as expected was the most effective model - RMSE score on the test data is 35.97 with the score on cross-validation 35.6, which shows no sign of overfitting.

The notebook [model_usage_app](https://github.com/usermarat/Flight_delays_project/blob/main/model_usage_app.ipynb) is were I implemented the model's predictions in a form of an application prototype. User will just have to choose the airport from which he/she would like to depart and the date/time of planned departure, and it will give the top 3 destination airports with the smallest flight delay based on the model's prediction. Also user could optionally choose destination airport, preferred airline, and it will give the prediction of a delay. You can also open it as well as the main notebook via colab badges placed at the beginning of each to check the app yourself.

Thank's for your attention! 

I would love to hear your feedback and any recommendations on my work, I can be found on telegram @usermarat

Thank you!

## Tech stack used for the project

* python
* google colab/jupiter notebook
* pandas
* numpy
* networkx
* geopandas
* matplotlib
* seaborn
* sklearn
* catboost
* ipywidgets
