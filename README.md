1. (CapeV4V5_distribution_yearlydifference.ipynb)\
Calculate the yearly distribution and difference of cape_roof_condition_rating in V4 and V5. Their distribution is shown below and their population stability index (PSI) are all < 0.01, which V5 has a slightly lower score. The yearly difference indicates that V5 gives a more stable rating (>70% same rating) than V4 (60% same rating), details in the following Excel. 

2. (generate_X.ipynb)\
Divide the May data into V4 and V5 first, then import the PRAC data from Xinyi (Oct run results). Exclude the HO4 and HO6 data form, and highpoint data (!=HPPREF)  in PRAC samples. Match the PRAC samples with Cape results (matching algorithm seeing below).\
Save the results for PRAC and Cape. We don't merge them together so that we can examine them later.
	
3. (analyzed_X.ipynb)\
Step 2 gives matched Cape and PRAC records. Divide Cape and PRAC data into train and validation based on PRAC keyword 'tv'. Save the data into different files, easy for future check.\
Please note that we finished this step early due to historical reason (obtaining baseline data late), and it could be finished later.
	
4. (load_baseline.ipynb)\
Since Cape and PRAC are already matched, we only need to match PRAC and baseline. Then use the resulting indices to match the cape data accordingly.\
For the baseline, since it only contain 'pol_num' and 'year' information, we will use them when matching with PRAC. (Sanity check seeing below).
	
5. (cape_response_okok.ipynb)\
Select the data that both Cape V4 and Cape V5 are 'OK' for 'cape_response_status' to reduce NaN data. 

6. (split_train_valid_test.ipynb)\
After obtaining the matched records for Cape, PRAC, and baseline, we want to split the dataset into training, validation, and holdout. The PRAC 'tv' has only train (0.7) and valid labels (0.3). Thus we divide the train into new_train (0.5), new_valid (0.2), and make the valid labels become our holdout (0.3). Calculate the inflation adjusted Ncat. Keep years, state, legacy stratified.

7. (EDA_plot.ipynb)\
Plot the statistical distribution for the selected variables. The columns are the frequency and the line is ee weighted parameters. \
Compare the V4 and V5 difference, and we will use the same Y-axis range. Save the data to Excel for the future plotting. 

	
9. (build_model_new.ipynb)\
After loading the training, validation, and holdout datasets, we remove the unnecessary variables, such as address, time, and id. We calculate the baseline Gini score for training and validation. Write a simple model to see the performance and a XGBoost model to fine tuning. Evaluate the performance on the holdout samples (baseline compared with prediction), save the holdout results, and get importance. V5 has better Gini score. 
	
10. (plot_model.ipynb)\
Using saved holdout results and Pumpkin.metrics to plot lift chart and standardized dual lift chart. Calculate the MAE for the Cape V4 and V5. V5 has better performance.
