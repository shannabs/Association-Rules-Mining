# Association Rules Mining

Project Part 3: Association Rule Mining

Learning objectives:

1. To be able to mine frequent item sets and frequent association rules from a dataset, using an appropriate mining method and selecting good support and confidence thresholds.  
2. To be able to accurately describe the association rule mined in English.
3. To be able to apply good quality measures to select the best rules.
4. To concisely summarize the main findings that are supported by the analyses.  
5. Students are expected to select appropriate methods for their analysis and objectively apply the methods so that the analysis and results do not contain major flaws or biases.  When unexpected results are obtained, use another method to verify the findings. 


Tasks:
We would like to continue examining the similarities and differences in police shootings involving male vs. female subjects. We would like to answer questions : (1) what were the typical scenarios where incidents involving male vs. female subjects happened, and (2) are there strongly associated attributes related to male vs. female shooting incidents? To answer these two questions, do the following

1. Keep as many useful attributes as possible from the fatal-police-shootings-data1.csv for this analysis. Explain any data preprocessing steps you need to perform. 

2. Divide the police shooting data into two subsets: one part involving only male victims, and the other part involving only female victims. From each subset, 
a. Mine 5 longest frequent item sets.
b. Mine 5 strong association rules as measured with Kulc and Imbalance Ratio scores.

3. Answer the two questions above by comparing and contrasting the itemsets and rules mined from male and female subsets.

4. Note: you may need play with different support and confident thresholds

Summary
(1) what were the typical scenarios where incidents involving male vs. female subjects happened, and (2) are there strongly associated attributes related to male vs. female shooting incidents?


To mine the five longest frequent item sets, we selected a minimum support value of 0.1. With the minimum support value set to 0.1, the longest frequent items for the male data were Black men, armed with a gun, and not related to mental illness ({armed_with=gun,race=B,was_mental_illness_related=False}). This combination was present in 16% of records in the male dataset. See the dataframe male_max_df for the full 5 longest frequent items. With regard to the female data, the longest frequent items were white women, not fleeing the scene, and the incidents were related to mental illness ({flee_status=not,race=W,was_mental_illness_related=True}). This combination was present in 19% of records in the female dataset. See the dataframe female_max_df for additional details and the full 5 items.

We also experimented with lower support and higher support values, but the results were not as favorable to identify patterns in the dataset. A lower support value resulted in itemsets with more items (higher K value), but these had very low occurrence percentages in the data, which did not offer useful insights. For example, with a support value of 0.01, the longest frequent itemset for males was K = 6, and consisted of the variables {threat_type=shoot,flee_status=not,armed_with=gun,race=B,was_mental_illness_related=False,year=2021}. However, this combination was present in only 0.06% of the male data, so did not represent a typical scenario. A higher support value resulted in itemsets with much higher occurrences in the data, but fewer items (lower K value). For example, with a support value of 0.5, the itemset with the most support for males was K = 1, with only the variable {flee_status=not}, which occurred in ~64% of the male records. While the occurrence percentages were much higher, the shorter itemsets did not offer valuable association information.

When comparing the male and female frequent itemsets, we found that typical scenarios that occurred for both genders involved victims that were not fleeing, white, armed with a gun, and were not mental illness related. This combination comprised approximately 15% of both the female and male data. We also found some differences when comparing frequent itemsets for each gender. For example, we found that nearly 14% of the female data occurred in the year 2017, but the male data frequent items were not associated with a year. Additionally, one of the top 5 frequent items for men included Hispanic men and not mental illness related, but Hispanics were not included in the top 5 frequent items for females. Also, only the female dataset included a frequent itemset with was_mental_illness_related=True; there did not appear to be frequent occurences related to mental health for males.

Additionally, we analyzed the association rules as measured with Kulc and Imbalance Ratio scores by focusing on the top 5 Kulc values within each gender subset. The top 5 Kulc values for the male and female data are in Top5KulcMale and Top5KulcFemale data frames, respectively. We spent some time experimenting with the variables included in the datasets to output meaningful associations, which took some trial and error. We ended up removing armed_with from the data, since the top 5 kulc values for both gender data subsets involved some variation of threat_type=shooting and armed_with=gun and took up a majority of the items in the itemsets. The Kulc value telling us level of association items have and with our original test with armed_with included, we know that threat_type and armed_with have a relatively strong association. This is not new information as it can be assumed and can easily be seen with simply tallying the data (which shows that threat_type=shoot happens over half the time when armed_with=gun). Due to the armed_with and threat_type consisting most of the top five spots the information is reiterated over and over, though this did support that our code was accurately finding associations, we decided it was best to remove armed_with and explore other, more hidden interesting knowledge.

After armed_with was removed, the top association rules in the female data primarily involved attributes related to mental illness and fleeing status. This suggests that in the presence of mental illness, females are less likely to flee the scene. The male data also captured the same association with the presence of mental illness and not fleeing the scene. Both genders also showed that fleeing in a car is associated with the absence of mental illness. The male data showed that there is an association with incidents involving black men to be classified as not being related to mental illness.
