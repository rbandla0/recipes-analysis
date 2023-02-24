# Does Taking Longer To Prepare Food Make It That Much Better??
by Raghava Bandla (rbandla@ucsd.edu)

---

# Introduction

This dataset contains the recipes, recipes's information, and average ratings. Using this dataset, the one question I want to answer is: \
\
***Is there a relationship between the number of steps in the recipe and the average rating of recipes?***\
\
Through this analysis, I have find out if there is a connection between longer food preparation time and the average rating of that food. The dataset has 83,782 rows, and the columns that are relevant to my question are 'n_steps' and 'avg_rating'. The 'n_steps' column contains the number of steps the recipe takes to prepare and the 'avg_rating' column contains the average of all the ratings given to the recipe in that row. 

---

# Cleaning and EDA
`print(recipes.head().to_markdown(index=False))`

---

# Assessment of Missingness

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
