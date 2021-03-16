# corruption_index_analysis

The goal of this project was to **analyze how Corruption correlates with other indicators (Sustainability, Economy, Human Development) over +100 countries**. I worked with students from Ecole Polytechnique's MSc Data Science and from HEC's MSc Sustainability.

### Data

Our data includes Economic, Social and Environmental indicators. For (almost) all indicators, I used the values from 2013 to 2018, as well as the absolute growth over the period. I used several data imputation techniques (linear interpolation, mean) to fill in the missing data, and in the end we focus on **105 countries**, from all continents. See all indicators below:

* Corruption Perceptions Index (CPI). The CPI is published annually by Berlin-based Transparency International and ranks countries "by their perceived levels of public sector corruption, as determined by expert assessments and opinion surveys."

* Economic indicators (source: World Bank):
  * GDP per capita
  * Extreme poverty (<1.90$ per day) index
  * Extreme poverty (<5.50$ per day) index 
  * Gini index

* Environmental indicators source: World Bank):
  -	Sustainable Development Index (SDI)
  -	CO2 emissions per capita
  - Percentage of waste recycled
  - Percentage of plastic waste
  - Total municipal solid  waste (normalized)
  - National agency and laws governing solid waste management (boolean)

* Social (source: United Nations):
  -	Human Development Index
  -	Homicide rates
  -	Gender Equality index

### Related work

*	https://tejas.iimb.ac.in/articles/Corruption_Tejas_mar17.pdf
*	https://link.springer.com/article/10.1023/A:1013882225402
*	https://towardsdatascience.com/can-budget-allocation-be-related-to-poor-government-performance-and-corruption-f9a1dc397bf0

### Analysis

We went through different types of analysis:

* **Clustering**, for each of the 3 groups of indicators we have, using Tableau for interactive plots. Example below with social indicators:
![](/analysis/Clusters%20-%20Human%20development.png))

* **Bivariate analysis** (scatter plots and R2 coeficient evolution). Example below with R2 evolution of CPI vs. SDI:
![](/analysis/CPI%20vs%20SDI%20R2%20evolution.png))

* **Multivariate regression**, providing the **most import variables** to predict CPI. The model used to obtain the graph below is *AdaBoost*:
![](/analysis/feature_importance_AB.png))

* **Correlation** of variables with CPI. Heatmap below:
![](/analysis/variable_correlation.png))

* Descriptive statistics (countries with the largest increase in CPI over the period, region with the largest decrease, etc.)

### Conclusions

The **feature importance** graph is probably the most relevant one, as it corresponds to the model that had the best results at predicting CPI (i.e. the lowest mean squared error). It's a model based on probability trees, which can capture non-linear relationships between our variables and CPI - something a classic linear regression can't do. 

We can see from this graph that **GDP per capita** is the most relevant variable to predict CPI, explaining more than **25% of CPI variance**. This corresponds to the results found in most online studies (e.g. https://link.springer.com/article/10.1023/A:1013882225402), which consider GDP per capita as the **best proxy for corruption** (other good proxies seem to be black market activity and other such variables, but we weren't able to find good quality data for this type of information!).
 
Another approach for regression was **PCA regression**, which consists in turning each category of variables (sustainability, economy, human development) into a single (or a few) composite variable through PCA (dimensionality reduction technique), in order to output a result such as "Economy" is the most correlated to CPI (and not only "gdp per capita", as stated above). However this approach led to less satisfying results than AdaBoost, which is our final model.

See more in the slides !
