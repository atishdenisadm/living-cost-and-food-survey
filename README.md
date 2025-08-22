# Living Cost & Food Survey (UK)
This project investigates the relationship between household characteristics and their financial well-being in the UK. It focuses on key factors such as social class, employment type, number of adults and children in a household, and expenditure patterns to assess how these influence economic stability.  
  
The research aims to answer whether certain groups face greater financial pressure than others, and how spending habits vary across different household types. By analyzing these dimensions, the study highlights the broader social and economic challenges households encounter, particularly regarding food costs and living expenses.

⚠️ Note: The original dataset (UK Living Cost and Food Survey) is restricted and cannot be shared publicly. This research was done as a part of my training along with my team in Mayerfeld Consulting.

## Research Question
Is There a Relationship Between Occupational Class, Tenure Type, Number of Adults, Number of Children and Expenditure of a Household?
  
## Key Findings
1. Housing Tenure
   1. Privately rented households spend ~39% more than public-rented households.
   2. Owned households spend ~46% more than public-rented households.
2. Occupational Class
   1. Lower spending compared to higher managerial occupations:
      1. Intermediate occupations: -20%
      2. Routine/manual occupations: -31%
      3. Long-term unemployed/students/unclassified: -45%
      4. Unclassified occupations: -39%
3. Household Size (Adults)
   1. Larger households spend significantly more:
      1. 2 adults: +75%
      2. 3 adults: +116%
      3. 4+ adults: +161%
4. Children
   1. 1 child: +10% (marginally significant)
   2. 2+ children: +20%
5. Model Fit
   1. Explained variance: 48.6% (Adjusted R² = 0.485)
   2. Strong overall fit (F = 440.4, p < 0.001)
  
## Transformation
A logarithmic transformation was applied to the Expenditure variable to address skewness and better meet model assumptions. While the transformed distribution remained similar to the original, statistical tests showed a modest improvement in normality and variance homogeneity. Therefore, the log-transformed version was used for further analysis and compared against the non-transformed model.
  
## Analysis Techniques Used
1. **ANOVA (Analysis of Variances):**  
   Used to test whether the mean household expenditure differs significantly across categories of a variable. For example, it helps determine if spending levels vary by occupational class.
2. **Multiple Linear Regression:**  
   Applied to analyze how household expenditure (dependent variable) is influenced by multiple factors such as occupational class, tenure type, number of adults, and number of children. The model was run on both the original expenditure values and their log-transformed values, enabling comparison of results and evaluation of whether the transformation improved model assumptions.

## Code Samples
```r
# Load libraries  
x<-c("plyr", "dplyr", "tidyr", "moments","ppcor","ggplot2","hrbrthemes", "MASS","car","rstatix")  
lapply(x, require, character.only = TRUE)

# Descriptive statistics
summary(df$household_expenditure)

# Summary of the model with log transformation
model <- lm(log(household_expenditure) ~ occupational_classes + tenure_type + childrens + adults, data = df)
summary(model)

# Distribution of Household Expenditure (Density plot with curve)
ggplot(df, aes(x = log(household_expenditure))) +
  geom_histogram(aes(y = ..density..), bins = 30,
                 fill = "skyblue", color = "black", alpha = 0.7) +
  geom_density(color = "red", size = 1.2) +
  labs(title = "Distribution of Household Expenditure",
       x = "Household Expenditure",
       y = "Density") +
  theme_minimal()
```

## Graphs and Visualization
Raw Data Distribution of Household Expenditure by Occupational Classes
<img width="1598" height="877" alt="household_expenditure_by_classes" src="https://github.com/user-attachments/assets/f9e07533-ecf6-4569-b301-6da2e1bd6518" />

Log Transformed Distribution of Household Expenditure
<img width="1184" height="861" alt="Log_transformed_distribution_expenditure" src="https://github.com/user-attachments/assets/025e8cf8-13ce-43a9-bfd9-bb295a06221a" />

## Conclusion
Overall, the analysis highlights a strong and consistent relationship between the four predictors and household spending, with household size showing the greatest impact, followed by tenure type and occupational class. Applying a log-transformation improved interpretability, enabling clear percentage-based comparisons that make the findings more intuitive and actionable.

