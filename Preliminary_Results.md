# Preliminary Results
 
**Date:** 2020-03-06

See Data_Exploration_Modeling.ipynb for code and visualizations. 

## Results

The datasets were loaded, cleaned, and prepped for analysis and modeling. 

Univariate analysis showed that the target variable (whether the reported side effect is present in SIDER) is imbalanced. The False side effect class is ~3 times greater than the True side effect class. There was a significant proportion of missing data in the weight variable (65% missing), so this variable was dropped. Outliers in Age and Number of Cocomitant drugs were also identified. These samples were removed from the dataset. 

Bivariate anlysis showed that that there was no correlation between the independent variables. 

Feature engineering and selection was performed separately for the numeric variables, single-label categorical variables, and multi-label categorical variables. All numeric variables were included since there were only three variables. The single-label (i.e.each drug had only a single category label) were one-hot encoded first. Then SciKit Learn's SelectKBest was used to find the top 50 variables based on the Chi-squared  F-score. The multi-label categirical variables (i.e. each drug could have zero or more category labels), ATC category and Target Protein, were encoded into vectors using hashing. Eoth were included in the model.

Using the most recent 5 years of data, a random forests model was used to preform binary classification. The model achieved an accuracy of 0.788 and an AUC of 0.85.

## Left to Do

### Molecular fingerprint as an independent variable

The orginal plan was to determine the molecular fingerprint from the chemical structure of each drug and include it as an independent variable. This has not yet been implemented.

### Improve the completeness of the datset

The dataset was assembled by combining three different datasets. This was performed by joining on text strings, which resulted in loss of data. It might be possible to use fuzzy matching to reduce data loss.

### Run the model for a different time period

The model was perfomed on only the most recent 5 years of data to test the performance and to limit processing time for the preliminary results. 

### Try a different strategy to deal with the class imbalance. 

To handle the class imbalance, class_weight='balance' was set to allow the classifier to automatically adjust weights inversely proportional to class frequencies in the input data. Subsetting the training data may produce better results. 
