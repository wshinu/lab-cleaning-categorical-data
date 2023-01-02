![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Cleaning categorical data

For this lab, we will be using the dataset in the Customer Analysis Business Case of the previous lab. This dataset can be found in `files_for_lab` folder. In this lab we will explore categorical data. 

### Special instructions

As in this lab we will keep working of the same dataset of the previous lab, please make a copy of the final Jupyter notebook of the previous lab in the current lab folder. Next, use Markdown to add a new section in the Jupyter notebook named `Lab Cleaning Categorical Data`. Then restart the Kernel and run all the previous cells. Finally, keep working of the same notebook according to the next instructions.

### Instructions

1. Define a function that given a pandas DataFrame as input creates a **seaborn countplot** of each categorical column. Make sure to sort the bars by frequency ie: the most frequent values should be placed first. Hint: use .value_counts(). In addition, if the amount of unique values of a categorical column (cardinality) is six or more, the corresponding countplot should have the bars placed in the `y` axis instead of the `x` one.
2. `policy_type` and `policy` columns are redundant, and what's worse `policy` column has a lot of possible unique values (high cardinality) which will be problematic when they will be dummified with a OneHotEncoder because we will increase a lot the number of columns in the dataframe. Drop the column `policy_type` and transform the column `policy` to three possible values: L1, L2, and L3 using a function.
3. Time dependency analysis. Use a seaborn lineplot using the column `effective_to_date` to see if `total_claim_amount` is bigger at some specific dates. Use a figsize=(10,10)
4. To continue the analysis define an empty pandas DataFrame, and add the following new columns:
* `day` with the day number of `effective_to_date`
* `day_name` with the day NAME of `effective_to_date`
* `week` with the week of `effective_to_date`
* `month` with the month NAME of `effective_to_date`
* `total_claim_amount` with `total_claim_amount`
5. Compute the total `target` column aggregated `day_name` rounded to two decimals and then reorder the index of the resulting pandas series using `.reindex(index=list_of_correct_days)`
6. Use a seaborn lineplot to plot the previous series. Do you see some differences by day of the week?
7. Get the total number of claims by day of the week name and then reorder the index of the resulting pandas series using `.reindex(index=list_of_correct_values)`
9. Get the median "target" by day of the week name and then sort the resulting values in descending order using .sort_values()
10. Plot the median "target" by day of the week name using a seaborn barplot
11. What do you can conclude from this analysis?
12. Compute the total `target` column aggregated `month` rounded to two decimals and then reorder the index of the resulting pandas series using .reindex(index=list_of_correct_values)
13. Can you do a monthly analysis given the output of the previous series? Why?
14. Define a function to remove the outliers of a numerical continuous column depending if a value is bigger or smaller than a given amount of standard deviations of the mean (thr=3).
15. Use the previous function to remove the outliers of continuous data and to generate a continuous_clean_df.
16. Concatenate the `continuous_cleaned_df`, `discrete_df`, `categorical_df` and the relevant column of `time_df`. As after removing outliers the continuous_cleaned dataframe will have less rows, when you concat all the dataframes using `p, you will generate NaN's because of the different size of each dataframe. 
16. Concatenate the `continuous_cleaned_df`, `discrete_df`, `categorical_df` and the relevant column of `time_df`. As after removing outliers the continuous_cleaned dataframe will have less rows, when you concat using `pd.concat()`, the resulting dataframe will have NaN's because of the different size of each dataframe. Use `pd.dropna()` and `.reset_index()` to fix the final dataframe.
17. Reorder the columns of the dataframe to place 'total_claim_amount' as the last column.
18. Turn the `response` column values into (Yes=1/No=0).
19. Reduce the class imbalance in `education` by grouping together ["Master","Doctor"] into "Graduate" while keeping the other possible values as they are. In this way, you will reduce a bit the class imbalance at the price of loosing level of detail.
20. Reduce the class imbalance of `employmentstatus` grouping together ["Medical Leave", "Disabled", "Retired"] into "Inactive" while keeping the other possible values as they are. In this way, you will reduce a bit the class imbalance at the price of loosing level of detail.
21. Deal with column `Gender` turning the values into (1/0).
22. Now, deal with `vehicle_class` grouping together "Sports Car", "Luxury SUV", "Luxury Car" into a commoun group called `Luxury` leaving the other values as they are. In this way, you will reduce a bit the class imbalance at the price of loosing level of detail.
23. Now it's time to deal with the **categorical ordinal columns**, asigning a numerical value to each unique value respecting the ìmplicit ordering`. Encode the coverage: "Premium" > "Extended" > "Basic".
24. Encode employmentstatus: "Employed" > "Inactive" > "Unemployed".
25. Encode location code: "Urban" > "Suburban" > "Rural".
26. Encode vehicle size: "Large" > "Medsize" > "Small".
27. Get a dataframe with the **categorical nominal columns**
28. Create a list named `levels` which has as many elements as categorical nominal columns. Each element must be another list with all the possible unique values of the corresponding categorical nominal column: ie:

```python
levels = [ [col1_value1, col1_value2,...], [col2_value1, col2_value2,...], ...]
```
28. Instantiate an [sklearn OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) with drop set to `first` and categories to `levels`
