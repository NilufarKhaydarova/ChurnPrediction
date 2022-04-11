# ChurnPrediction

**Report on Churn Analysis and Prediction**

[Link for the Jupyter notebook](https://colab.research.google.com/drive/10BC7ZgS17QzkeTovRk_3rHvzHRapy_vJ?usp=sharing)

_Overview._

This is the report on analyzing Customer Churn dataset, with the simple exploratory analysis of factors and prediction of whether the client will stay or not.

_Data Exploration._

Outlines:

- 18 features, 2 binary and 1 target attribute;
- No outliers were detected;
- No missing values.

Certain features were dropped such as:

- Phone number - since this is a relational dataset, each row is already unique and we do not need number to identify the client.
- State - there was no pattern between state and churn, although 2 states out of 51 showed a slight higher churn, the correlation is still insignificant.
- Area code - there were only 3 area codes for 51 states and there was no explanation in the description either. It did not make any sense, so it would be better to drop it (at least temporarily).
- Длина счёта (length of the client account?)- the correlation with the churn was insignificant. ![](RackMultipart20220411-4-5a65wi_html_19fcecb18f133a3b.png)

_Analytic methods._

Because data is very imbalanced (the data of customers churning is only 20%), it needed oversampling and I have applied SMOTE algorithm to generate synthetic samples, followed by re-scaling numerical attributes and splitting data into independent and dependent variables for modeling.

As for the feature selection and modeling, I have used Competitive Classification Tree and Random Forest Classifier. The tree gives higher importance to a particular set of features, while RFC selects it randomly, by using both we can see how correct our feature selection is. ![](RackMultipart20220411-4-5a65wi_html_57f2f210ef54eae8.png)

- International Plan - when the customer do have international plan in their service, their churn rate is higher;
- Calls to the service center - the more times the customer has called the center, the higher is the rate of leaving;
- Daily minutes/charges - the relationship of both features was linear and both scored highest for feature importance.

![](RackMultipart20220411-4-5a65wi_html_ae2dc6315cbe54fd.png)

Classification Tree (with the accuracy score of 0.94) gives us the features that are important insights - the blue boxes show the customers who might leave/left and orange boxes represent loyal customers who stayed. F.e. if daily minutes are higher than 264 or the service center calls are higher than, the clients who churned are more than clients who stayed. However, it can clearly be seen that most customers are very loyal to their provider, since most clients are the ones with daily minutes less than 264, less than 3 service calls and with no international plan (1738 clients out of 2333). ![](RackMultipart20220411-4-5a65wi_html_900d8c6894b1e56d.png)

As for the Random Forest Classifier, it performed very well with the accuracy score of 0.95, precision and 0.89 and ROC AUC score 0.87. It shows that the model correctly predicted 104 churn cases and 12 more cases of churned customers as not-churned.

Logistic Regression did not perform well (it was only given 3 most important features to train with), however, it did a relatively okay job concerning the probability of churning with the accuracy of 0.75.

In the table below, we can see 10 customers who churned and the column of Churn prediction (Уход Прогноз) is the RFC model and 2 columns of probability is LR. ![](RackMultipart20220411-4-5a65wi_html_72705f65299b6865.png)

_Conclusion:_

As for the models, linear regression is good for important features with high Gini score, however, the accuracy is not good enough (I believe it is due to the fact that relationships in the data are not linear)

Classification Tree explained different factors related to churn rate very well, however, I believe Random Forest Classifier performed better with higher predictive scores and higher recall (how many churn cases were correctly predicted as churn).

Ensemble learning with Gradient Boosting Classifiers (such as XGBoost or LightGBM) should definitely be considered to continually improve the model and due to the imbalance of the dataset.

