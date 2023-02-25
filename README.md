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
The first thing I did was getting a series containing the average rating of each recipe id which was also the index of the series. I merged this series with the recipes dataframe using the left merge so that every recipe id in recipes was in the resulting dataframe but the average rating of each recipe id in the series that was also in recipes was included in the dataframe. I named this new column 'avg_rating'. After that, I replaced all the 0 values in the 'minutes' column with np.nan because taking 0 minutes for a recipe doesn't make sense. I also replaced the maximum minutes value of 1051200 with np.nan because it skewed the data too much and the actual recipe wasn't an edible reciple. After this, I got calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates
`print(recipes.head().to_markdown(index=False))`
\
\
***Univariate Analysis:***
\
<iframe src="assets/fig1.html" width=800 height=600 frameBorder=0></iframe>
\
\
***Bivariate Analysis:***
\
<iframe src="assets/fig3.html" width=800 height=600 frameBorder=0></iframe>

---

# Assessment of Missingness
***NMAR Analysis:*** In this dataset, there is not a column where

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
***Conclusion:*** 
