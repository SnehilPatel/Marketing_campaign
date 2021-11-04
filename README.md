# Marketing Performance Predictor


## Structure

This project contains two parts, a regression model builder/trainer and a web app to predict results.

1) Model: Basic training pipeline in training.py, consuming first_glance.py (basic descriptive analysis), helpers.py (helper functions), preprocessing.py (data preprocessing) and regression.py (regression class with 4 different regressor methods).

2) App: Single page app defined in api.py. HTML views in templates, custom CSS in static/css.

## Contribution

Please submit any issue you have. If you have any ideas how to further improve the predictor please get in touch or feel free to fork this project and create a pull request with your proposed updates.

## Environment

- Python 3.6
- Flask (web framework)
- zappa (deployment to AWS lambda)
- numpy (Python computing package)
- pandas (Python data analytics library)
- statsmodels (Python statistics module)
- Matplotlib (Python plotting library)
- Seaborn (Python visualization library)
- Scikit-learn (Python machine learning library)
- Joblib (Python pipelining library)
- Psycopg (Python PostgreSQL adapter)
- Boto 3 (AWS Python SDK)

## Prediction pipeline (as in training.train())

1) Load data from CSV or (Postgres) database
2) Preprocess data
3) Build regressors (linear, tree, forest and SVR)
4) Evaluate regressors
5) Fit best regressor to data
6) Save best regressor

## Predict results

Now we have a model ready to predict the results of future marketing campaigns. We only have to call the predict method on it passing a specific feature vector and will receive the respective prediction for the metric we trained our regressor on. We can also compare the true impressions from the existing dataset to their predictions based on our new model:
![image](https://user-images.githubusercontent.com/53311202/140272615-f67937dd-8a1e-4a74-b82c-c3b490b80822.png)

The average relative deviation of a prediction from its actual, true value equals 26%, ergo we reached an accuracy of 74%. With only 14% the median deviation is even smaller.

Here are the results:

Training accuracies: Linear 0.34, Tree 0.67, Forest 0.75, SVR 0.63
Test accuracies: Linear 0.32, Tree 0.64, Forest 0.66, SVR 0.61

Our best regressor is the random forest with the highest test accuracy of 66%. It seems to be a little overfit though since the deviation from its training accuracy is relatively large. Feel free to experiment with other values for the hyperparameters to further improve all of the models.
Before finally saving our model to make predictions on new data, we will fit it to all available data (training and test set) to incorporate as much information as possible.

## Conclusion

We were able to build and train regressors that allow us to predict the number of impressions (and other performance metrics in an analogue fashion) for future marketing campaigns from historical campaign data.
The highest prediction accuracy has been achieved with a random forest model.
We can now use these predictions to evaluate a new marketing campaign even before its start. Also, this allows us to determine the best parameters including e.g. timeline and budget size for our campaigns since we can calculate the predictions with different values for those features.
