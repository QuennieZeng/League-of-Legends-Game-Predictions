# League-of-Legends-Game-Predictions

This is a project for DSC80 where we predict the result of a League of Legends game using early-game statistics.

Our exploratory data analysis on this dataset can be found [here](https://quenniezeng.github.io/League-Of-Legends-Early-Stats-Analysis/).

Name(s): Quennie Zeng and Vaibhav Bommisetty

---

# Framing the Problem
It’s November 19, 2023. You are watching the World Championships where it is T1 vs Weibo Gaming. It’s been 15 minutes and you’re waiting to see if Faker will win his fourth World championship. But your mother calls you and tells you you need to go pick up milk from a grocery store three hours away. You won’t be able to see if Faker wins his fourth championship, all you have is the data from the first 15 minutes of the game. Will T1 win?

Our model was created to predict the outcome of a professional League of Legends match using early-game statistics. Here, we will be using **multiclass classification** because we are dealing with multiple types of data and seek a categorical outcome. The response variable is the **result** of the game, and we focus on early game statistics for prediction.

Using the early game statistics, we will be predicting the result of the game using the **2022 Esport** game statistics, keeping the same data cleaning we performed from our exploratory analysis [here](https://quenniezeng.github.io/League-Of-Legends-Early-Stats-Analysis/). Considering the time constraints and the nature of our predictive task, we use only the information available within the first 15 minutes of the game. This approach aligns with our goal of forecasting the match outcome based on early data. Our metric of choice is **accuracy** in the context of multiclass classification.

For those involved in betting on esports, particularly League of Legends matches, model **accuracy** holds significant financial implications. A high level of accuracy not only identifies the winning team but also distinguishes between various possible outcomes. This predictive capability is crucial for navigating the complexity of multiclass betting scenarios, where accurate assessments of diverse match results are essential for informed betting decisions and positive returns.

---

# Baseline Model
In our baseline model, we intend to predict the result of the game from the early game statistics data, such as differences in gold, XP, and CS at 10 and 15 minutes, first objectives, and total stats at 10 and 15 minutes. 

Quantitative Features: **`goldat10`**,  **`xpat10`**, **`csat10`**, **`golddiffat10`**, **`xpdiffat10`**, **`csdiffat10`**, **`killsat10`**, **`assistsat10`**, **`deathsat10`**, **`goldat15`**, **`xpat15`**, **`csat15`**, **`golddiffat15`**, **`xpdiffat15`**, **`csdiffat15`**, **`killsat15`**,**`assistsat15`**, **`deathsat15`**


Nominal Features: **`league`**, **`firstblood`**, **`firstdragon`**, **`firstherald`**, **`firsttower`**


Response Variable: **`result`** \(1\|0\)

We encoded the **`league`** with OneHotEncoder() and engineered a new feature, **`TrueCount`**, that counts the **`first`** objectives each team earned. All other features remained the same as the other nominal features are boolean and the quantitative features are discrete. 


## Conclusion

Our accuracy was about 63.42%. This is a low moderate performance. We believe this model is moderate as the accuracy is only slightly higher than 50%, which is a model that only predicts based on random chance. We did not include later game statistics, which would have been more accurate to the result of the game. 

---

# Final Model

For our final model, we used feature engineering to create new features that could help our model be more accurate.

## New Features:

We looked to add features by using the following transformers:

**MomentumFeatureEngineering:**

To quantify the momentum of the game, we assessed statistical differences at 15 and 10 minutes. Our approach involved standardizing these differences and computing their average. This process provides a concise and rough estimate of the game's momentum, where a positive value indicates the team's improved performance and a negative value suggests the opposite.

**StandardScalar:** 

This built-in feature would standardize the columns we run in it. We used it to standardize our numerical columns that did not include differences in them since we used those columns in our MomentumFeatureEngineering transformer. Using this would help make all of our information standardized by removing the mean and scaling to unit variance. This allows our data to be mean-centered, equally scaled, and normally distributed, all making the algorithm perform better. 

**Overfitting:**

While creating the model, we ran into the problem of overfitting, as our training accuracy was at 100%, while our validation accuracy was around 75%. To address this issue, we examined the features and considered whether feature engineering could help improve generalization.

To start, we took out the columns with ‘diff’ to make the data more simple, as we had included the columns with **`diff`** in our ‘momentum’ feature.

We also considered the heat maps and dropped the columns in which there wasn't as big of a difference between the winning and losing teams. We decided to drop **`csat10`**, **`csdiffat10`**, **`killsat10`**, **`assistat10`**, **`deathsat10`**, **`csat15`**, **`killsat15`**, and **`assistat15`** after looking at the graphs.



Heatmap result for **`csat10`**:
<iframe src="assets/Heatmap_result_v_csat10.html" width="800" height="600"></iframe>

Heatmap result for **`csdiffat10`**:
<iframe src="assets/Heatmap_result_v_csdiffat10.html" width="800" height="600"></iframe>

Heatmap result for **`killsat10`**:
<iframe src="assets/Heatmap_result_v_killsat10.html" width="800" height="600"></iframe>

Heatmap result for **`assistat10`**:
<iframe src="assets/Heatmap_result_v_assistsat10.html" width="800" height="600"></iframe>

Heatmap result for **`deathsat10`**:
<iframe src="assets/Heatmap_result_v_deathsat10.html" width="800" height="600"></iframe>

Heatmap result for **`csat15`**:
<iframe src="assets/Heatmap_result_v_csat15.html" width="800" height="600"></iframe>

Heatmap result for **`killsat15`**:
<iframe src="assets/Heatmap_result_v_killsat15.html" width="800" height="600"></iframe>

Heatmap result for **`assistat15`**: 
<iframe src="assets/Heatmap_result_v_assistsat15.html" width="800" height="600"></iframe>



## Conclusion:
After testing, our result is Training Accuracy: **.9782** and Validation Accuracy: **0.7613**.
Our Validation accuracy went up so it is not overfitting as much. We dropped the columns that we mentioned earlier (Columns that included the word **`diff`** in the title and others that were dropped due to visual analysis of their heatmaps and distributions).

## Overfitting (again):

It’s important to address that it would be difficult to control the overfitting of our data as there is limited predictive power of our early game statistics, high variability, and there incomplete data.

There is limited predicted power in early games when it comes to determining the outcome of a match. This limitation arises due to factors such as evolving strategies, dynamic team interactions, and individual player performances, all of which introduce complexity and potential variability in the final result. Thus, it would be difficult to determine the outcome of a game from early game statistics alone as it may not capture the complexity of the match.

There is also the question of whether the team chose a team composition that prioritizes early-game success or late-game success. Teams strategically select and ban champions based on whether they would like a strong early game or a strong late game. This tactical decision  is driven by the desire to either excel in the early stages of a match or focus on late-game dominance, aiming to scale up the power of their champions. The intricacies of champion selection thus reflect a team's deliberate approach to optimize performance in specific phases of the game.


Violin plot result for **`csat15`**:
<iframe src="assets/violin_plot_result_v_csat15.html" width="800" height="600"></iframe>

Violin plot result for **`csdiffat15`**:
<iframe src="assets/violin_plot_result_v_csdiffat15.html" width="800" height="600"></iframe>

Violin plot result for **`assistat15`**:
<iframe src="assets/violin_plot_result_v_assistsat15.html" width="800" height="600"></iframe>

Our analysis of the model's performance, particularly its reliance on early game statistics, has shown noise within the dataset. When examining violin plots, we observe that the overall distribution of the data remains similar, but noticeable differences are primarily evident in the outliers. This observation leads us to suggest that the model's susceptibility to overfitting arises from an excessive focus on outliers for result separation. By disproportionately emphasizing these extreme data points, the model may struggle to generalize effectively, contributing to overfitting tendencies. Addressing this issue and refining the model's ability to recognize meaningful patterns beyond outliers could be crucial in enhancing its predictive accuracy and generalization performance.

Our data is also incomplete, so we were not able to capture all the relevant aspects influencing the match outcome. The challenge in controlling overfitting also arises from missing data in the **`result`** column.


## Modeling Algorithm Choice:

The modeling algorithm we chose, in the end, was the `RandomForestClassifer()`. Though `SVC()`, `GradientBoostingClassifer()`, and `AdaBoostClassifier()` had comparable performance, we decided on this classifier for its versatility and robustness. RandomForest combines the predictions of multiple individual models (trees) which leads to more accurate and stable predictions compared to a single model handles missing values well and can maintain good performance even when some data is missing. RandomForest's ability to combine predictions from multiple trees provides enhanced accuracy, stability, and resilience. Additionally, its capacity to handle missing values contributes to maintaining good performance even with incomplete data.

## Hyperparameters and Selection Method:

The optimal hyperparameters for the RandomForestClassifier were determined through a systematic search. The chosen values were {'randomforestclassifier__max_depth': 10, 'randomforestclassifier__min_samples_split': 18}.

We employed a rigorous approach to hyperparameter tuning, utilizing a parameter grid and executing a grid search with 5-fold cross-validation. This process ensured the identification of hyperparameters that maximize the model's performance.

## Model Performance Improvement:
Compared to the baseline model, the final RandomForestClassifier demonstrated improved performance. It improved our accuracy by around **12.27%**, from 63.42% to 75.69%. Its versatility, robustness, and controlled overfitting, achieved through carefully selected hyperparameters, contributed to enhanced predictive capabilities and overall model effectiveness.

---

# Fairness Analysis

## Fairness Group:
We analyzed whether the prediction model had similar differences in accuracy for playoff matches versus non-playoff matches.
We chose **‘playoffs’** as the group to analyze, as playoff matches have higher stakes and a different atmosphere than regular matches. We believe that these factors may influence the results of a match and possibly sway the result in one way or another.
We decided to analyze fairness using accuracy, this is due to the 

## Null Hypothesis:
Our Win-Loss model has the same accuracy for playoff matches as non-playoff matches.

## Alternative hypothesis: 
Our Win-Loss model has a different accuracy for playoff matches compared to non-playoff matches.

## Test Statistic: 
Difference in Accuracy (Of playoff matches vs non-playoff matches)

## Significance level:
p < 0.05

## Permutation:
We achieved a p-value of 0.0, meaning that there was a statistically significant difference in the way that our model predicted playoff games vs non-playoff games.


<iframe src="assets/differences.html" width="800" height="600"></iframe>


Therefore, we reject our null hypothesis, there is a statistically significant difference in the accuracy of our Win-Loss model between playoff matches and non-playoff matches. The p-value of 0.0 indicates a highly improbable result under the assumption that the model's accuracy is the same for both types of matches.


