# Data and Methodology




## Data
The data for this analysis was sourced from Kegel and consists of two primary datasets encompassing men's college basketball statistics. The first data set provides KenPom rankings tracking overall offensive and defensive metrics dating back to 2002 containing 13 tables and 357 total columns. The second data set spans from 2008 to 2025 offering more granular statistical data like shooting splits and originally contained 34 tables and 1,054 columns. The public repository for this data is located at: 
https://www.kaggle.com/datasets/jonathanpilafas/2024-march-madness-statistical-analysis
https://www.kaggle.com/datasets/nishaanamin/march-madness-data




## Summary of Key Variables
The following table outlines the core features used to model tournament success focusing on efficiency, shooting metrics, and Dean Oliver's “Four Factors”




### Variable Name
Description/What it measures
Type/Format
tournament_winner
The response variable indicating if a team won the March Madness championship.
Binary (1/0)
adjusted_offensive_efficiency

A team’s scoring output per 100 possessions, adjusted for opponent defense
Numeric

adjusted_defensive_efficiency
A team’s points allowed per 100 possessions, adjusted for opponent offense.
Numeric

seed
The team’s assigned rank in their tournament region.
Numeric

top_12_in_ap_top_25_during_week_6?
Indicates if a team was established in the top 12 of the AP poll by week 6.
Binary

efgpct_off
Offensive field goal efficiency percentage (one of Dean Oliver’s “Four Factors”)
Numeric

orpct_off
Offensive rebound percentage (one of Dean Oliver’s “Four Factors”)
Numeric

topct_off
Turnover percentage on offense (one of Dean Oliver’s “Four Factors”)
Numeric

ftrate_off
How often a team gets to the free-throw line relative to their field goal attempts (one of Dean Oliver’s “Four Factors”)
Numeric

fg3pct
A team’s actual three-point shooting percentage
Numeric

 




## Data Preparation and Cleaning
To prepare the data set for analysis the two primary cable databases were merged using team name and season as the primary keys to create a single, unified data frame. This required extensive cleaning to ensure data Integrity into format the data for machine learning:
Structural Formatting: All column names were converted to lowercase with spaces replaced by underscores for consistency. duplicate columns resulting from the merge (ending in _x or _y) were dropped.
Addressing Data Integrity: Initial validation revealed that certain seasons falsely listed multiple tournament winners. Investigation showed this was caused by a duplicated conference column with inaccurate values. The incorrect conference field was removed, which resolved the duplicate rows and correctly reduced the data to one champion per season.
Filtering Scope: Due to data quality issues in early records and incomplete Seasons data from 1999-2001, the COVID-shortened 2020 season, and incomplete 2025 test datasets were removed. The final clean dataframe covers the 2002 to 2024 seasons.
Imputation and Handling Nulls: Columns with a majority of missing data or irrelevant miscellaneous stats were dropped entirely. For remaining numerical columns, missing values (~ 855 missing rows out of 16,205) were imputed using the median value of their respective columns. Finally, categorical nulls in target variables such as ‘made final four’ or ‘tournament winner” were replaced with a binary "0 " or"No ". 




## Methodology
The analytical approach centered on exploratory data analysis (EDA), feature analysis, and supervised machine learning to identify the statistical profile of a championship team. 




## Analytical approach
### Exploratory Data Analysis (EDA): The analysis began by visualizing distributions in historical trends. line charts were utilized to track the evolution of the game over the 20-year span (e.g., tracking the rise in 3-point usage by season). Stacked bar plots, scatter plots, and box plots were used to isolate and contrast the metrics of tournament winners against the rest of the tournament field, directly establishing baseline thresholds like the 110/95 offensive and defensive efficiency mark.  
Correlation Analysis: To establish linear relationships between performance metrics and tournament success, a correlation heatmap was generated. This helped calculate R-squared scores to identify which variables (such as seed and week 6 AP rankings) possessed strong initial correlations with the tournament_winner label. 
Predictive Modeling (Tree-Based Machine Learning): To go beyond simple correlation, a supervised, tree-based machine learning model was deployed. The model analyzed all variables to assign a relative “feature importance” score to each column. This method provided a ranked list of the top 15 most impactful variables for predicting a tournament winner, confirming that adjusted defensive and offensive efficiency were the strongest on-court predictors. One-hot encoding was used to manage the categorical response variables during the modeling phase. 




## Tools for Reproducibility
Python: The entirety of the data wrangling, merging, cleaning, correlation heatmaps, and machine learning modeling was conducted using Python within Jupyter Notebooks. The Matplotlib and Seaborn libraries were explicitly used for initial EDA plotting. Every major step was separated and categorized into distinct, commented Python scripts to ensure the transformations were repeatable. 
Tableau: While Python and Streamlit were evaluated for reporting, Tableau was ultimately selected as the final visualization software due to its superior capacity for storytelling and generating audience-friendly business dashboards. Tableau was used to create the final scatter plots, line charts, and the visualizations of the machine learning feature importance scores. 
