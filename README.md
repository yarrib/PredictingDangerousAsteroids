# PredictingDangerousAsteroids

Title — What is your app/project called?
Overview — Why did you start this project?
Features — What are some key things your project can do?
Running the project — How could someone else get your code working for them?
Dependencies — What are the main outside resources your project needs to run?


## Overview
This project was completed for a course in Fall 2020. I selected the topic because of my interest in astrophysics and space in general. It was approved based on my proposal, which contained an outline of the objectives and methods likely to be used. It was intended that this run on Kaggle and be submitted as a notebook. However, the attempt to do this was cut short because I ran into issues around the use of the caret package. So it never was submitted. I'd likely move to python if I head down that route.

Data Source: https://www.kaggle.com/sakhawat18/asteroid-dataset (saved it as 'dataset.csv')
From this source, data has been obtained through NASA's Jet Propulsion Laboratory: Small Body Database. This analysis answers a task question from the data maintainer, though I never submitted it on Kaggle.


## Purpose
I have decided to apply data mining methods to determine asteroids which are potentially hazardous to our planet (Earth). My initial assumptions are that (1) the response classes are plausible and/or reliable given the scientific definitions of ‘potentially hazardous’, and (2) these data have features which both identify and differentiate the asteroids. 

## Target Audience
Beyond the researcher who has publicly posted this task, I believe folks in the astrophysics community would benefit from this predictive modeling. Because there is a response variable, it is presumed methods have already been explored by NASA’s JPL. As such, this analysis is benchmarking against unknown existing modeling. It is my hope that the predictive ability of the model provides useful insight into how well collected asteroid attributes inform us about the potential of impending doom.

## Technical Approach
For tabular data being loaded into memory, the data is moderately large (435mb). The shape is ~958k x 45 (ncol x prows). Based on high level exploration, it would be beneficial to remove a few columns which are not empirical measurements (object id, name of asteroid, etc.). It was fairly easy to identify a significant imbalance in the data; a small proportion of asteroids are truly hazardous ("pha"). Principal components analysis (PCA) was employed to reduce our dimensionality to principal components PC which satisfy 85% or more of the total variability in the data. Additionally, near zero variance handling and downsampling (via SMOTE) helped to account for important characteristics in these data.  With our principal components determined, model selection with cross validation for a few methods was used with grid searching over several models. Efficient methods like Logistic Regression (baseline), gradient boosting and tree based approaches, and support vector machines were prioritized. Lastly, a test set split prior to any training was evaluated over the model(s), the result being honest model scores with special consideration to Sensitivity (and Type II errors for that matter - when looking at a confusion matrix).

## Dependencies
This project was implemented in an R markdown notebook environment using r4.0.x and all dependencies are called at the beginning of the *PredicitngDangerousAsteroidsV2.rmd* markdown file.

## Limitations
There are some unused dependencies because it was intended some of the cross validation (CV) training for model selection be performed in parallel (via the caret package's doParallel method), but that was never added to the project. Perhaps some efficiencies in training time would be achieved using this method. This would facilitate exploration of more models (maybe).

Substituing a genetic algorithm or bayesian optimization in lieu of grid search would likely be a significant improvement in the results as yielded in the confusion matrix (Type I and Type II errors).

Loading the initial dataset into memory is computationally expensive and there is probably a better way, e.g. using Dask or some other method. I am not versed (yet!) in these methods thus I didn't venture down this road when I worked on the project.

## Other

License: MIT