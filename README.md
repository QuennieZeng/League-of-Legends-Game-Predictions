# League-of-Legends-Game-Predictions

This is a project for DSC80 where we predict the result of a League of Legends game using early-game statistics.

Our exploratory data analysis on this dataset can be found [here](https://quenniezeng.github.io/League-Of-Legends-Early-Stats-Analysis/).

Name(s): Quennie Zeng and Vaibhav Bommisetty

---

# Framing the Problem
It’s November 19, 2023. T1 vs Weibo Gaming. It’s been 15 minutes and you’re waiting to see if Faker will win his fourth World championship. But your mother calls you and tells you you need to go pick up milk from a grocery store three hours away. You won’t be able to see if Faker wins his fourth championship, all you have is the data from the first 15 minutes of the game. Will T1 win?

Our model was created to predict the outcome of a professional League of Legends match using early-game statistics. Here, we will be using **multiclass classification** because we are dealing with multiple types of data and seek a categorical outcome. The response variable is the **result** of the game, and we focus on early game statistics for prediction.

Using the early game statistics, we will be predicting the result of the game using the **2022 Esport** game statistics, keeping the same data cleaning we performed from our exploratory analysis [here](https://quenniezeng.github.io/League-Of-Legends-Early-Stats-Analysis/). Considering the time constraints and the nature of our predictive task, we use only the information available within the first 15 minutes of the game. This approach aligns with our goal of forecasting the match outcome based on early data. Our metric of choice is **accuracy** in the context of multiclass classification.

For those involved in betting on esports, particularly League of Legends matches, model **accuracy** holds significant financial implications. A high level of accuracy not only identifies the winning team but also distinguishes between various possible outcomes. This predictive capability is crucial for navigating the complexity of multiclass betting scenarios, where accurate assessments of diverse match results are essential for informed betting decisions and positive returns.

---

# Baseline Model
In our baseline model, we intend to predict the result of the game from the early game statistics data, such as differences in gold, XP, and CS at 10 and 15 minutes, first objectives, and total stats at 10 and 15 minutes. 

Quantitative Features: **`goldat10`**,  **`xpat10`**, **`csat10`**, **`golddiffat10`**, **`xpdiffat10`**, **`csdiffat10`**, **`killsat10`**, **`assistsat10`**, **`deathsat10`**, **`goldat15`**, **`xpat15`**, **`csat15`**, **`golddiffat15`**, **`xpdiffat15`**, **`csdiffat15`**, **`killsat15`**,**`assistsat15`**, **`deathsat15`**


Nominal Features: **`league`**, **`firstblood`**, **`firstdragon`**, **`firstherald`**, **`firsttower`**


Response Variable: **`result`** (1|0)

We encoded the **`league`** with OneHotEncoder() and engineered a new feature, **`TrueCount`**, that counts the **`first`** objectives each team earned. All other features remained the same as the other nominal features are boolean and the quantitative features are discrete. 


## Conclusion

Our accuracy was about 63.42%. This is a low moderate performance. We believe this model is moderate as the accuracy is only slightly higher than 50%, which is a model that only predicts based on random chance. We did not include later game statistics, which would have been more accurate to the result of the game. 

---

# Final Model

Heatmap result for **`assistat10`**:
<iframe src="assets/Heatmap_result_v_assistsat10.html" width="800" height="600"></iframe>

Heatmap result for **`assistat15`**: 
<iframe src="assets/Heatmap_result_v_assistsat15.html" width="800" height="600"></iframe>

Heatmap result for **`csat10`**:
<iframe src="assets/Heatmap_result_v_csat10.html" width="800" height="600"></iframe>

Heatmap result for **`csat15`**:
<iframe src="assets/Heatmap_result_v_csat15.html" width="800" height="600"></iframe>

Heatmap result for **`csdiffat10`**:
<iframe src="assets/Heatmap_result_v_csdiffat10.html" width="800" height="600"></iframe>

Heatmap result for **`csdiffat15`**:
<iframe src="assets/Heatmap_result_v_csdiffat15.html" width="800" height="600"></iframe>

Heatmap result for **`deathsat10`**:
<iframe src="assets/Heatmap_result_v_deathsat10.html" width="800" height="600"></iframe>

Heatmap result for **`deathsat15`**:
<iframe src="assets/Heatmap_result_v_deathsat15.html" width="800" height="600"></iframe>

Heatmap result for **`goldat10`**:
<iframe src="assets/Heatmap_result_v_goldat10.html" width="800" height="600"></iframe>

Heatmap result for **`goldat15`**:
<iframe src="assets/Heatmap_result_v_goldat15.html" width="800" height="600"></iframe>

Heatmap result for **`golddiffat10`**:
<iframe src="assets/Heatmap_result_v_golddiffat10.html" width="800" height="600"></iframe>

Heatmap result for **`golddiffat15`**:
<iframe src="assets/Heatmap_result_v_golddiffat15.html" width="800" height="600"></iframe>

Heatmap result for **`killsat10`**:
<iframe src="assets/Heatmap_result_v_killsat10.html" width="800" height="600"></iframe>

Heatmap result for **`killsat15`**:
<iframe src="assets/Heatmap_result_v_killsat15.html" width="800" height="600"></iframe>

Heatmap result for **`xpat10`**:
<iframe src="assets/Heatmap_result_v_xpat10.html" width="800" height="600"></iframe>

Heatmap result for **`xpat15`**:
<iframe src="assets/Heatmap_result_v_xpat15.html" width="800" height="600"></iframe>

Heatmap result for **`xpdiffat10`**:
<iframe src="assets/Heatmap_result_v_xpdiffat10.html" width="800" height="600"></iframe>

Heatmap result for **`xpdiffat15`**:
<iframe src="assets/Heatmap_result_v_xpdiffat15.html" width="800" height="600"></iframe>

Violin plot result for **`assistat10`**:
<iframe src="assets/violin_plot_result_v_assistsat10.html" width="800" height="600"></iframe>

Violin plot result for **`assistat15`**:
<iframe src="assets/violin_plot_result_v_assistsat15.html" width="800" height="600"></iframe>

Violin plot result for **`csat10`**:
<iframe src="assets/violin_plot_result_v_csat10.html" width="800" height="600"></iframe>

Violin plot result for **`csat15`**:
<iframe src="assets/violin_plot_result_v_csat15.html" width="800" height="600"></iframe>

Violin plot result for **`csdiffat10`**:
<iframe src="assets/violin_plot_result_v_csdiffat10.html" width="800" height="600"></iframe>

Violin plot result for **`csdiffat15`**:
<iframe src="assets/violin_plot_result_v_csdiffat15.html" width="800" height="600"></iframe>

Violin plot result for **`deathsat10`**:
<iframe src="assets/violin_plot_result_v_deathsat10.html" width="800" height="600"></iframe>

Violin plot result for **`deathsat15`**:
<iframe src="assets/violin_plot_result_v_deathsat15.html" width="800" height="600"></iframe>

Violin plot result for **`goldat10`**:
<iframe src="assets/violin_plot_result_v_goldat10.html" width="800" height="600"></iframe>

Violin plot result for **`goldat15`**:
<iframe src="assets/violin_plot_result_v_goldat15.html" width="800" height="600"></iframe>

Violin plot result for **`golddiffat10`**:
<iframe src="assets/violin_plot_result_v_golddiffat10.html" width="800" height="600"></iframe>

Violin plot result for **`golddiffat15`**:
<iframe src="assets/violin_plot_result_v_golddiffat15.html" width="800" height="600"></iframe>

Violin plot result for **`killsat10`**:
<iframe src="assets/violin_plot_result_v_killsat10.html" width="800" height="600"></iframe>

Violin plot result for **`killsat15`**:
<iframe src="assets/violin_plot_result_v_killsat15.html" width="800" height="600"></iframe>

Violin plot result for **`xpat10`**:
<iframe src="assets/violin_plot_result_v_xpat10.html" width="800" height="600"></iframe>

Violin plot result for **`xpat15`**:
<iframe src="assets/violin_plot_result_v_xpat15.html" width="800" height="600"></iframe>

Violin plot result for **`xpdiffat10`**:
<iframe src="assets/violin_plot_result_v_xpdiffat10.html" width="800" height="600"></iframe>

Violin plot result for **`xpdiffat15`**:
<iframe src="assets/violin_plot_result_v_xpdiffat15.html" width="800" height="600"></iframe>

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


