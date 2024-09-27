# Seita ML Ops assignment

Thanks for taking the time to apply at Seita Energy Flexibility!

## The task

We'd like to train a simple model on an energy consumption dataset and make it available with a simple API endpoint.

## A few words on expectations

This assignment mixes a little data science with a little API development.

We want you to keep the effort needed for this task limited, for your sake mostly but also ours. We don't expect you to work more than a few hours on this, less is good.
Stop before completion, if needed. Next to seeing your work, the main goal is to talk to you about your work.

A few notes on effort:
- We do assume here that you are familiar with using data science libraries and basic API development
- It's okay to use / be inspired by code you find on the internet, but: we expect comments and we will ask you to explain
- If you make it easy for yourself, your code will of course look like many other solutions. Being interesting/effective in your preferred way makes sense for interviewing (to both sides).

Notes on what we look for:
- We see data science / ML as being not more than a third of the project you apply for, maybe less. The rest is software/data engineering.
- We care about developer empathy (readability, docs, style, test, installable, extensible) at least as much as feature-richness or ML accuracy.


## Part 1: Train a simple forecasting model

Download the energy consumption dataset [1] and train a model on it.

- Use a (Python-based) library of your choice.
- There are two options here:
  A) Use a library specialized to do forecasting on time series (fbprophet, NeuralProphet, ...). This is the most simple approach, just feed in historical data. As we said, it's fine to be straightforward.
  B) Use extra features regressors (like day of week, hour of day, day of year) to make a regression model (e.g. with xgboost, statsmodels, nixtla or sktime). See [2] for an example. This is the more extensible approach.
- Show a quick validation on a part of the data set (visual and/or mean error)
- Store the model on file [3]


## Part 2: A simple API endpoint

Implement an API endpoint (GET) which returns the predicted energy consumption. (Input varies based on chosen option A or B from above)

- Use a (Python-based) API library of your choice, e.g. Flask, FastAPI, Django (we are using Flask & MarshMallow)
- The endpoint loads the stored model (Part 1) from file and gets the forecast from it.
- With option A, your model can predict N hours starting from its training data, so the input would be N
  With option B, your model can predict based on features, so the input are the features you used
- Both input and output are expected in JSON. Example input: `{"N" : 8}` for option A or `{"hour_of_day": 8, "day_of_week": 3, "day_of_year": 122}` for option B. Example output: `{"prediction" : 1333.06337}`
- Do some checks on the input, so that wrong input gets a proper response, not a runtime error or misleading result.


## Delivery

You can deliver this task as a GitHub repo, or (only if you have privacy concerns) as a ZIP file (to nicolas@seita.nl).For a repo, great if it's public (putting yourself out there is good!) but if you can't, then we prefer a closed repository on GitHub, where you add our accounts (nhoening, flix6x) so we are able to read.

Part 1 can be a notebook or script. We should be able to create the model with your code, but do include your model, so we can test Part 2 in any case.

For both parts, please instruct us how to open / install / test your code on a Unix computer.

Please place the last commit 24 hours before our interview.



[1] https://raw.githubusercontent.com/ourownstory/neuralprophet-data/main/datasets/energy/SF_hospital_load.csv
[2] https://www.kaggle.com/code/robikscube/tutorial-time-series-forecasting-with-xgboost
[3] With many libraries, pickle works well, while for instance prophet brings its own (de)serialization: https://facebook.github.io/prophet/docs/additional_topics.html 


