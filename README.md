# Hard-Drive-Failure-Prediction
![image](https://user-images.githubusercontent.com/129183971/230729353-d36ffb5e-7ec6-420a-981b-b23816184b82.png)

To use the script, you would need to modify the dir_path variable to match the directory path where your CSV files are located. You would also need to modify the condition variable to match the filter condition you want to apply to each file.
The script uses the os and pandas libraries to iterate over the files in the directory and read the CSV files into a temporary dataframe. It then applies the filter condition to the temporary dataframe using the query() method and concatenates the filtered dataframe to the df dataframe using the concat() method. The ignore_index parameter is set to True to ensure that the index values are reset after concatenation.
Finally, the compiled dataframe is printed using the print() function.

![image](https://user-images.githubusercontent.com/129183971/230729567-7843c4a0-1dd0-44d0-80c1-b790983abd40.png)

Here , it calculates the minimum count of non-null values that each column must have in order to remain in the dataframe. This minimum count is calculated as a percentage of the total number of rows in the dataframe, with the percentage specified by the perc variable (which is set to 50 in this code). Any column that has fewer non-null values than this minimum count is dropped from the dataframe.

After dropping columns with insufficient non-null values, the code drops any columns that have all null values (i.e., NaN) using the dropna() method with the how='all' parameter. It then drops any rows that have at least one null value using the dropna() method without any parameters.Finally, the resulting dataframe is printed using the print() function.Overall, this code is designed to clean and preprocess data by removing columns and rows that have too many null values. This can be useful for machine learning tasks where missing data can lead to inaccurate predictions or models.

![image](https://user-images.githubusercontent.com/129183971/230729914-e8e305af-ce7f-47b8-b1a8-95434ecbe3af.png)

An empty list called master is defined,it will be used to store data from the filtered CSV files in some way.This code appears to be setting up some initial parameters and functions to be used in a data analysis or processing task. The file filtering and column dropping functions shows the code is intended to preprocess data.

![image](https://user-images.githubusercontent.com/129183971/230732909-74e9c1ca-201c-4208-b2a3-4f003f469af8.png)

Data analysis on a pandas DataFrame called "master_df" that contains information on different models and whether or not they failed. The code calculates the number of failures, non-failures, and total counts of each model in the entire dataset and stores the results in separate DataFrames called "failure_counts," "no_failure_counts," and "count," respectively. The resulting DataFrames contain information on the number of failures, non-failures, and total counts of each model, which can be used for further analysis.

![image](https://user-images.githubusercontent.com/129183971/230733096-de25aadc-968d-4744-bbb4-a218e8942792.png)
This code block is combining the "no_failure_counts" and "failure_counts" DataFrames into a single DataFrame called "merged_level_1". The "merge" method is used to combine the two DataFrames based on the "name" column, which contains the names of the models. The resulting DataFrame contains three columns: "no_failed_count," "name," and "failed_count."The "NaN" values in the "failed_count" column indicate that there were no failures for those particular models in the dataset.

![image](https://user-images.githubusercontent.com/129183971/230733107-0dd91e64-7107-43b0-b981-17c8aeff7951.png)

This code block is merging the "count" DataFrame, which contains the total count of each model, with the previously created "merged_level_1" DataFrame, which contains the counts of failures and non-failures for each model. The resulting DataFrame is called "merged_level_2."

The "merge" method is again used to combine the two DataFrames based on the "name" column, which contains the names of the models. The "fillna" method is then used to replace any missing values in the "failed_count" column with zeros, since missing values indicate that there were no failures for those particular models in the dataset.

The "astype" method is then used to convert the "failed_count" column to integer type. Finally, the "sort_values" method is used to sort the DataFrame by the "failed_count" column in descending order, so that the models with the most failures are listed first.

![image](https://user-images.githubusercontent.com/129183971/230733279-50381791-4d07-4e3c-b0fd-21a165f86a98.png)

This code is removing columns from the "master_df" DataFrame that have too many missing values to be useful for analysis. The resulting DataFrame can be used for further analysis without the dropped columns.

** Splitting the Data**
![image](https://user-images.githubusercontent.com/129183971/230733385-5b2f4afc-0404-40bc-b936-1f0b09868742.png)
![image](https://user-images.githubusercontent.com/129183971/230733388-df1c4da1-30d0-4b6b-8742-de936eaabcaa.png)
![image](https://user-images.githubusercontent.com/129183971/230733392-717a85e4-4830-4322-b6d1-11f474747230.png)

Here splitting the datset for train and test

![image](https://user-images.githubusercontent.com/129183971/230733593-dd657e40-f596-4ea0-a509-5c4b4b764d9e.png)



Performing classification using a Random Forest model, with hyperparameter tuning using a GridSearchCV object.First, the "StandardScaler" class is imported from the "sklearn.preprocessing" module, which is used to standardize the input features before feeding them into the model.Then, the training and testing data are standardized using the "fit_transform" and "transform" methods of the "StandardScaler" object, respectively.Next, a dictionary of hyperparameters for the Random Forest model is defined in the "param_grid" variable, which includes values for the number of estimators, maximum features, splitting criterion, maximum depth, and whether or not to use bootstrap samples.

A Random Forest model is then passed to a "GridSearchCV" object along with the parameter grid and the number of cross-validation folds. The "GridSearchCV" object searches for the best combination of hyperparameters based on the accuracy score and returns the best set of hyperparameters found.

After finding the best hyperparameters, a new Random Forest model is instantiated with those hyperparameters and fit to the standardized training data using the "fit" method.

Finally, the fitted model is used to predict the classes of the standardized test data and the results are summarized.

*** Accuracy****

![image](https://user-images.githubusercontent.com/129183971/230733761-2047b611-b550-49fc-8f69-cbe8ff68c8a6.png)

The model achieved an accuracy of 91.35% on the test set, which is a good performance. The training accuracy is slightly higher than the testing accuracy, but the difference is not very large, suggesting that the model is not overfitting.

The output of the code above shows the confusion matrix of the model's predictions on the test set. The matrix shows that the model made 10196 correct predictions of the negative class and 880 correct predictions of the positive class. It also made 860 incorrect predictions of the negative class (false positives) and 820 incorrect predictions of the positive class (false negatives).

The classification report shows that the model has an accuracy of 0.91, with precision of 0.88 for class 0 (correctly predicted negative samples), and precision of 0.96 for class 1 (correctly predicted positive samples). Recall (i.e., true positive rate) for class 0 and 1 are 0.96 and 0.86, respectively. The f1-score (harmonic mean of precision and recall) for class 0 and 1 are 0.92 and 0.91, respectively. The macro-average f1-score is 0.91, indicating that the model is performing well for both classes. The weighted average f1-score is also 0.91, taking into account the imbalance in class sizes.

**** After Cross Validation****
![image](https://user-images.githubusercontent.com/129183971/230733947-2ad7e0d0-bbb3-4920-815c-9b84ae830627.png)

Cross-validation on a Random Forest classifier with hyperparameters gives max_depth=5, criterion='gini', max_features='sqrt', and n_estimators=75. The cross-validation is performed with 5 folds. The code outputs the mean training and validation accuracy, precision, recall, and f1 score, as well as the individual training and validation scores for each fold.

The mean training accuracy is 0.9144, and the mean validation accuracy is 0.8826. The mean training precision is 0.9190, and the mean validation precision is 0.8938. The mean training recall is 0.9144, and the mean validation recall is 0.8826. The mean training f1 score is 0.9141, and the mean validation f1 score is 0.8817.

The individual training and validation scores for each fold are not shown in the output.

![image](https://user-images.githubusercontent.com/129183971/230734032-e30f6e5d-b225-40f1-8b30-5c4960f1d81e.png)
A bar plot to compare the training and validation accuracy scores of a random forest classifier model in 5 folds. The plot will have "Accuracy scores in 5 folds" as its title, "Accuracy" as the y-axis label, and "1st Fold", "2nd Fold", "3rd Fold", "4th Fold", "5th Fold" as the x-axis labels. The training accuracy scores will be plotted as green bars and the validation accuracy scores as red bars. The model name will be "Random forest classifier".

![image](https://user-images.githubusercontent.com/129183971/230734052-8513bf5b-cad4-4d41-9cee-5d3582175847.png)

The plot_results function from "Random forest classifier", the metric to be plotted, "Precision", the title of the plot, "Precision scores in 5 folds", and the training and validation precision scores extracted from some previously executed code.

![image](https://user-images.githubusercontent.com/129183971/230734122-dd5cef90-21fc-457a-a135-3857df92f926.png)

The model name is "Random forest classifier", and the plot title is "Recall scores in 5 folds". The function takes the training and validation recall scores from the "result" dictionary as inputs.

![image](https://user-images.githubusercontent.com/129183971/230734158-6bde72f6-3452-4c45-8d83-4078b933ae77.png)

To visualize the F1 scores of the random forest classifier model. The graph will have the model name as the title, "F1" as the y-axis label, and "F1 scores in 5 folds" as the subtitle. The training F1 scores and validation F1 scores are taken from the result dictionary using the keys "Training f1 score" and "Validation f1 score", respectively.



