# Does Taking Longer To Prepare Food Make It That Much Better??
by Raghava Bandla (rbandla@ucsd.edu)

---

# Introduction

This dataset contains the recipes, recipes's information, and average ratings. Using this dataset, the one question I want to answer is: \
\
***Is there a relationship between the number of steps in the recipe and the average rating of recipes?***\
\
Through this analysis, I have to find out if there is a connection between the number of steps and the average rating of that food. The dataset has 83,782 rows, and the columns that are relevant to my question are 'n_steps' and 'avg_rating'. The 'n_steps' column contains the number of steps the recipe takes to prepare and the 'avg_rating' column contains the average of all the ratings given to the recipe in that row. 

---

# Cleaning and EDA
The first thing I did was getting a series containing the average rating of each recipe id which was also the index of the series. I merged this series with the recipes dataframe using the left merge so that every recipe id in recipes was in the resulting dataframe but the average rating of each recipe id in the series that was also in recipes was included in the dataframe. I named this new column 'avg_rating'. After that, I replaced all the 0 values in the 'minutes' column with np.nan because taking 0 minutes for a recipe doesn't make sense. I also replaced the maximum minutes value of 1051200 with np.nan because it skewed the data too much and the actual recipe wasn't an edible reciple. After this, I got calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates numbers from the 'nutrition' column and added them to their own columns. 
`print(recipes.head().to_markdown(index=False))`
\
\
***Univariate Analysis:*** This box and whiskers plot shows the distribution of the number of steps. 50% of the data is in between the 6-13 range, but the maximum and 4th quartile skew the data towards a higher number of steps.
<iframe src="assets/fig1.html" width=800 height=600 frameBorder=0></iframe>
\
\
***Bivariate Analysis:*** This scatter plot shows the number of steps on the x-axis and the average rating on the y-axis. Majority of the data points are clumped in the top left corner however as the number of steps increased, the number of low average ratings decreased. 
<iframe src="assets/fig3.html" width=800 height=600 frameBorder=0></iframe>

---

# Assessment of Missingness
***NMAR Analysis:*** In this dataset, there is a column that is NMAR which is the 'description' column because the missingness depends on the actual values. If the recipe is self explanatory, then there would be no reason for a description or if the description basically contains the name of the recipe. 

***Missingness Dependency:*** The 'n_steps' column is a column that 'avg_rating' depends on because the p-value was 0.0 and the significance level was 0.05. This means we reject the null that the missingness of 'avg_rating' doesn't depends on 'n_steps'. This could be evidence for the question I am trying to answer because the missingness of average rating is dependent on the number of steps. The 'name' column is a column that 'avg_rating' doesn't depend on because the p-value was 0.126 and the significance level was 0.05. This means we fail to reject the null that the missingness of 'avg_rating' does depend on 'n_steps'.
<iframe src="assets/fig5.html" width=800 height=600 frameBorder=0></iframe>

---

# Hypothesis Testing

***Null Hypothesis:*** There is no relationship between the number of steps and the average rating of recipes. The observed difference in the samples is due to random chance.\
\
***Alternative Hypothesis:*** There is a relationship between the number of steps and the average rating of recipes. The observed difference in the samples can't be explained by random chance.\
\
***Test Statistic:*** Total Variation Distance (TVD)\
\
***Significance Level:*** 0.05\
\
***P-value:*** 0.019\
\
***Conclusion:*** Since the p-value is less than the significane level, we reject the null because there isn't enough statistical evidence to support it. SInce we reject the null, it proves that there is a relationship between the number of steps and the average rating of recipes. These choices are good for answering the question because if we reject the null based on the permutation test performed, then it answers the question. 
