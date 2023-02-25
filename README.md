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
```py
print(recipes.head().to_markdown(index=False))
```
| name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                                                                                               | nutrition                                     |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   avg_rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates | avg_rating_missing   |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-------------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|:---------------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]      |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |            4 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 | False                |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]  |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |            5 |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 | False                |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]     |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |            5 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 | False                |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] | [878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0] |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |            5 |      878.3 |          63 |     326 |       13 |        20 |             123 |              39 | False                |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             | [267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]    |        17 | ['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |            5 |      267   |          30 |      12 |       12 |        29 |              48 |               2 | False                |
\
\
***Univariate Analysis:*** This box and whiskers plot shows the distribution of the number of steps. 50% of the data is in between the 6-13 range, but the maximum and 4th quartile skew the data towards a higher number of steps.
<iframe src="assets/fig1.html" width=800 height=600 frameBorder=0></iframe>

\
\
***Bivariate Analysis:*** This scatter plot shows the number of steps on the x-axis and the average rating on the y-axis. Majority of the data points are clumped in the top left corner however as the number of steps increased, the number of low average ratings decreased. 
<iframe src="assets/fig3.html" width=800 height=600 frameBorder=0></iframe>

\
\
***Interesting Aggregates:*** The average of the average rating is higher when the number of steps increases, with majority of the average ratings being 5 at the end of the dataframe.
|   n_steps |   avg_rating |
|----------:|-------------:|
|         1 |      4.64813 |
|         2 |      4.66612 |
|         3 |      4.65546 |
|         4 |      4.64004 |
|         5 |      4.61038 |
|         6 |      4.61137 |
|         7 |      4.62251 |
|         8 |      4.62609 |
|         9 |      4.61521 |
|        10 |      4.60389 |
|        11 |      4.61956 |
|        12 |      4.61869 |
|        13 |      4.6287  |
|        14 |      4.60289 |
|        15 |      4.61348 |
|        16 |      4.63361 |
|        17 |      4.64033 |
|        18 |      4.6261  |
|        19 |      4.65347 |
|        20 |      4.64079 |
|        21 |      4.63482 |
|        22 |      4.64615 |
|        23 |      4.62641 |
|        24 |      4.66983 |
|        25 |      4.60421 |
|        26 |      4.61642 |
|        27 |      4.57603 |
|        28 |      4.76479 |
|        29 |      4.66187 |
|        30 |      4.53663 |
|        31 |      4.69456 |
|        32 |      4.6779  |
|        33 |      4.63761 |
|        34 |      4.65258 |
|        35 |      4.68614 |
|        36 |      4.74912 |
|        37 |      4.71939 |
|        38 |      4.65304 |
|        39 |      4.72292 |
|        40 |      4.7375  |
|        41 |      4.8001  |
|        42 |      4.82574 |
|        43 |      5       |
|        44 |      4.5375  |
|        45 |      4.73387 |
|        46 |      4.22727 |
|        47 |      4.78819 |
|        48 |      4.71429 |
|        49 |      4.60833 |
|        50 |      4.42857 |
|        51 |      4.67857 |
|        52 |      4.22222 |
|        53 |      4.57143 |
|        54 |      5       |
|        55 |      4.7375  |
|        56 |      5       |
|        57 |      4.5     |
|        58 |      4.92857 |
|        59 |      5       |
|        60 |      5       |
|        61 |      4.1875  |
|        62 |      4.66667 |
|        63 |      5       |
|        64 |      5       |
|        65 |      5       |
|        66 |      5       |
|        67 |      5       |
|        68 |      4.5     |
|        69 |      5       |
|        70 |      5       |
|        71 |    nan       |
|        73 |      5       |
|        76 |      5       |
|        77 |      5       |
|        79 |      4.75    |
|        80 |      4.875   |
|        81 |      4.5     |
|        85 |      5       |
|        86 |      5       |
|        87 |      5       |
|        88 |      3.66667 |
|        93 |      5       |
|        98 |      5       |
|       100 |      5       |

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
