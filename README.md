
# Coffee Shop Data Analysis

## Introduction

The primary objective of this project is to create a set of marketing strategies that the coffee shop can implement to attract potential customers and encourage them to make purchases. By meticulously analyzing customer data, understanding their preferences, and strategically leveraging targeted approaches, we aim to provide impactful managerial implications and actionable suggestions for the coffee shop management team.


## Data Collection

The dataset “Coffee Shop Sample Data” was obtained from Kaggle https://www.kaggle.com/datasets/ylchang/coffee-shop-sample-data-1113. It contains retail data from a coffee chain with three New York City locations encompassing a series of nine spreadsheets: Sales Receipts, Pastry Inventory, Sales Targets, Customer, Dates, Product, Sales Outlet and Staff and Generation.

## Research Topics

The research topics I investigated are as follows: 
    

- forecasting sales
- predicting the interaction of customers' age and gender on sales
- measuring the magnitude of change in the quantity due to the change in price
- predicting the variables that affect customers decision to order online versus in store purchase and
- identify and select groups of potential customers

## Method
      

**Overview of the Analytical Methods**
    
- To get an initial understanding of the data, I conducted some explanatory analysis mainly evolving around the target variable ‘quantity’ sold in the coffee shop.
- For forecasting sales, I have used OLS, and KNN.
- For predicting the interaction effect of gender and age on sales I have used OLS with interaction term.
- For measuring the magnitude of quantity change due to a change in price I have used Price Elasticity method. 
- For predicting the variables that affect customers decision to purchase in store I have used Decision Tree, Logistic Regression, SVM, Random Forest and finally 
- I have used Clustering Analysis for customer segmentation. 

**Data Pre-processing and Cleaning**

  - **Explanatory Analysis**: In order to conduct the explanatory analysis, I first merged the files sales_receipts, and product on product_id and got around 50,000 rows. For variables with spaces in Product Category I used python codes to take out the spaces and replace them with hyphens. I also took dummies of product_category and tax_exemption_yn and finally dropped the null values to get the final table.

  - **Linear regression and KNN**: To predict if the quantity of products sold depends on the retail price, product category and tax exemption I merged the files sales_receipts, and product on product_id and took dummies of product_category and tax_exemption_yn for the OLS model. Besides this, I have split the data into test and training data and then conducted the KNN.

  - **OLS with interaction**: To find the effect of age and gender on sales I first dropped the ‘N’ values from ‘Customer’ and then merged it with ‘Sales Receipt’ on ‘customer_id’. Thereafter, I grouped the data by customer_id and transaction_date on the aggregate quantity sold and ultimately merged them into one table.

  - **Price Elasticity**: I took the log of both unit_price and quantity from the file ‘Sales_Receipt’ and performed Own Price Elasticity. 

  - **Decision Tree, Logistic Regression, SVM & Random Forest**: For predicting the variables that affect the most in making in store purchase decisions of customers I chose the files ‘sales_receipt’, ‘customer’, ‘product’, and ‘generations’. Firstly, I merged ‘sales_receipt’ and ‘customer’ on ‘customer_id’ and named it Table_1. Then I merged Table_1 and ‘product’ on ‘product_id’ and named it Table_2 and merged it with ‘generation’ creating Table_3. Next, in Table_4 I saved the clean data after dropping the unnecessary variables and took dummies of the categorical variables. Then I considered ‘instore_yn’ as my dependent variable and 'quantity', 'unit_price', 'birth_year',   'home_store_dum_3', 'home_store_dum_5', 'home_store_dum_8', 'gender_F', 'gender_M', 'product_category_Bakery', 'product_category_Branded', 'product_category_Coffee', 'product_category_Coffee_beans', 'product_category_Drinking_Chocolate', 'product_category_Flavmys', 'product_category_Loose_Tea', 'product_category_Packaged_Chocolate', 'product_category_Tea', 'tax_exempt_yn_N', 'tax_exempt_yn_Y', 'generation_Baby_Boomers', 'generation_Gen_X', 'generation_Gen_Z',  'generation_Older_Millennials', 'generation_Younger_Millennials' as my independent variables. Thereafter, I split the data into tests and training, with 30% for testing and 70% for training. 

  - **Clustering**: For my clustering analysis I merged my variables from my generation table and OLS (merged table) to identify which generation of customers makes the most in store purchases by running k-means clusters.

## Analysis and Interpretation

**Explanatory Analysis**

- **Positive Correlations**:
  - Coffee: There’s a positive correlation between coffee and quantity sold. Customers seem to purchase more when coffee is involved.
  - Tea: Similarly, tea also shows a positive correlation with quantity sold.
  - Tax Exemption: The presence of tax exemption positively impacts sales.
- **Negative Correlation**:
    - Retail Price: The negative correlation between retail price and quantity sold suggests that higher prices may lead to lower sales.

    ![1corr](https://github.com/user-attachments/assets/e64edde6-4451-48ff-9ccf-6c657424684c)


  - **Top-Selling Product categories**: Based on the GroupBy analysis Coffee is the top selling category followed by Drinking Chocolate, Various Flavours and Tea.

![image](https://github.com/user-attachments/assets/946eaad4-4813-49a6-9614-684c2dac34af)
 
  - **Tax Exemption Impact**: When the store receives tax exemption, it appears to positively influence the quantity sold.


![image](https://github.com/user-attachments/assets/49bc9d57-f1d6-4b03-b32e-8712326764dc)

  - **Price Range and Quantity Sold**: Between $0.8 and $4.5, the average quantity sold is around 15 units and as the price increases beyond this range, the quantity sold decreases. However, there is an exception noticed. o	At a price of $45, there’s a sudden increase in quantity sold.o	This unique case is due to Civet Coffee, considered the most expensive coffee globally, extracted from the faces of civet cats. The fermentation process during digestion results in a distinct and rich flavor.

  ![image](https://github.com/user-attachments/assets/f1ecf8ad-71ce-473a-aa6e-dbd267963b7f)


**Linear Regression and KNN**

  - **OLS Regression**
      
      My OLS regression model is:

    *Quantity = β0 + β1current_retail_price + β2 Bakery + β3 Branded + β4 Coffee_beans + β5 Drinking_Chocolate + β6 Flavors + β7 Loose_Tea + β8 Packaged_Chocolate + β9 Tea + β10  tax_exempt_yn_Y.*

    From this model, I found:

    - All the variables are significant with p-value of 0.00 except Drinking Chocolate (0.33) and Tea (0.23).
    - The R-squared value is 0.130 which means that my model explains only 13% of the variance in quantity sold. 
    - Bakery was the most sold product category followed by the category branded products and ultimately coffee as implied by the positive coefficients of Bakery and Branded and negative coefficients for the other products in the model.
    - Sales increase when there is tax exemption as implied by the positive coefficient of tax_exempt_yn_Y (1.5).
    - There is a negligible effect of price change on quantity sold as implied by the coefficient of current retail price (0.0073).

    ![image](https://github.com/user-attachments/assets/0d6e4ac2-3f3d-4519-8341-db3b0f6479fb)

  - **KNN**

      To check the test accuracy, if there are any overfitting issues, and to classify the above-mentioned data set based on its nearest neighbors I performed KNN analysis.  First of all, I standardized the predictors and then split the data into training and test data. Thereafter, I ran KNN analysis for k = 1 ~ 10 and provided the accuracy scores on the test data. Next, I plotted the accuracy scores of training and test data and chose an optimal K-value to report the accuracy score on the test data. According to my analysis:

      - Optimal k-values: Based on your analysis, the optimal values of k were 2 and 6 (as indicated in Appendix G).
      - Test Accuracy: For both optimal k-values, the test accuracy score was 0.58.
      - Overfitting: The negligible difference between training and test accuracy scores suggests that there are no overfitting issues in the model.

      ![image](https://github.com/user-attachments/assets/85e84f70-edc2-4e66-bed4-b0b245e9d7ef)

      ![image](https://github.com/user-attachments/assets/f267b2bc-59a1-4c60-b075-735c6910cb1b)

      

**OLS with Interaction Terms**

The regression model:

*quantity_x = β0 + β1gender+ β2 birth_year + β3 gender * birth_year + e*

Based on the analysis:

- **Statistical Significance**:
    
    - Gender and the interaction of gender with birth year are both statistically significant (p-value of 0.00).
    - Birth year, although not statistically significant (p-value of 0.678), should still be included due to its impact on the interaction term.

- **Gender Differences**:

    - Male customers purchase around 7 units more than female customers on average.
    - However, as male customers age, their purchasing behavior decreases compared to female customers.

- **Age and Gender Interaction**:

   - Female customers tend to buy more as they age.
   - The positive effect of gender on quantity sold is reduced for older male customers.

   ![image](https://github.com/user-attachments/assets/32063af4-eb91-48f0-850b-21c47519344a)


**Price Elasticity**

For Price elasticity, I took the log of unit_price and log of quantity from the file ‘Sales_Receipt’ and performed price elasticity. The model is: 

*lnQuantity_x = β0 + β1lnunit_price + e*                                                                                                     

Based on the analysis:

- An R-squared value of 0.023 indicates that only 2% of the variance in the model is explained by the independent variable.
- The coefficient of ‘lnunit_price’ is statistically significant (p-value of 0.00).
- With a one-unit increase in the natural logarithm of price, the log of quantity sold decreases by 0.124 units.
- Given that the quantity response is less than half the price increase, you indeed have an elastic demand.
- Elastic demand means that changes in price significantly impact the quantity sold.

![image](https://github.com/user-attachments/assets/85a1a233-f134-42de-ba62-b76b9e72c39d)


**Decision Tree, Logit, SVM, & Random Forest**

To find how the quantity of products sold, unit price, different home store locations, different categories of product, tax exemption, customer’s gender and their generation affect their decision to purchase in store I used decision tree model and logistic regression to first find the key features affecting their decision. The logistic regression model used for my first research question is:

*takeout_order = β0 + β1quantity + β2 unit_price+ β3birth_year+ β4home_store_dum_5 + β5home_store_dum_8 + β6gender_M + β7generation_Gen_X + β8generation_Gen_Z+ β9generation_Gen_Z + β10generation_Older_Millennials + β11generation_Younger_Millennials + β12product_category_Bakery + β13product_category_Branded+β14product_category_Coffee_beans+β15product_category_Drinking_Chocolate+β16product_category_Flavmys+β17product_category_Loose_Tea+β18product_category_Packaged_Chocolate + β19product_category_Tea + β20 tax_exempt_yn_Y + e*

The reference dummies that I have used are ‘home_store_3’ for location, Male for gender, Baby Boomers for generation, Coffee for product_category and ‘Tax_exemption_Yes’ for tax exemption.
Next, I checked test and training accuracy scores for decision tree, logit model, SVM and random forest model. To check which max depth minimizes the difference between the train accuracy score and the test accuracy score of the decision tree, I found that max depth 2 and 3 have very little difference and thus can be used to minimize overfitting problems. Ultimately, I used 2 as the max depth for the decision tree. Finally, I compared the four models based on accuracy scores, precision scores, recall scores and specificity scores and finally selected the decision tree model with the highest overall scores for future prediction.

Based on the analysis, I found that, for:

- **Logistic Regression Model**: The model is significant (LLR p-value < 1). HoIver, none of the coefficients have statistically significant p-values. So, I do not explain the variables.

![image](https://github.com/user-attachments/assets/c2b14492-3891-4e6f-b326-a522e35237ab)

- **Decision Tree Model**:The most important features affecting customers’ in-store purchase decisions are ‘birth_year’ and ‘product_category_Coffee’.

![image](https://github.com/user-attachments/assets/549e08a1-6575-463d-86ee-40f8cff52c23)

- **Intra-Model Evaluation**:

    - Negligible differences exist between training and test accuracy scores for all four models.
    - Intra-model overfitting is not a concern.
    - Based on test accuracy scores:
      - Decision Tree: 0.509
      - Logit: 0.513
      - SVM: 0.503
      - Random Forest: 0.509

- **Inter-Model Evaluation**:
    
    - Precision, recall, and specificity scores vary across models:
      - Decision Tree: Better at predicting positive cases.
      - Logit: Equally good for both positive and negative cases.
      - Random Forest: Better at predicting negative cases.
      - SVM: Good at predicting positive cases but not negative cases.

   - Considering overall performance, Random Forest stands out:
     - Highest precision score (0.511)
     - Highest recall score (0.603)
     - Moderate specificity (0.3022)

**Clustering**

To identify and select groups of potential customers, I incorporated k-means clustering within my data analysis. I ran a total of five k-means clustering which included finding the top instore purchases, birth year, unit price, product id, and their generation.For that, ), I first scaled and standardized all variables, as each of the columns within my table had different units and variable sizes. I then used the elbow method to determine the number of clusters I would use to run my analysis. In terms of less error, I decided to perform a 5-cluster k-means analysis using random state 10. My first k-means focused on determining which generation had the highest in-store purchases. I found that:

- Cluster 4 had the most instore purchases with a mean of 0.04. 
- Segmenting cluster 4 I found, top birth year for customers is from Gen Z with a mean of 2.65.
- The top products within this cluster are Drip Coffee, Barista Espresso, Brewed Chai Tea 
- Top customers are mix of male and female.

![image](https://github.com/user-attachments/assets/521d2604-add1-4b0f-979a-ec61118bb956)

## Managerial implications

- **Targeted promotions**

  - Based on the results from the OLS, the coffee shop should use promotions and advertisements that are specifically targeted toward their bakery products, branded products and coffee. 
  
  - Also, from the results based on the interaction OLS model, the coffee shop should target more young male customers and aged female customers. For example, in its advertisement it can show an aged female customer ordering coffee and cake through the drive through, whereas a young group of male customers hanging out in their store, chatting over coffee and some branded products. 

- **Store Interiors**

    - The coffee shop should design the interiors with a 1990s theme, catering to customers born in that era as the decision tree results indicates that these customers prefer in-store purchases.

- **GenZ Focus**
    
    - Based on the results in k-means clustering analysis, I would recommend managers to focus their attention on Gen Z customers as well and potentially open a location near a college campus as this generation is more likely to make in-store purchases. 

## Conclusion

Thus, to conclude the coffee shop needs to focus more on its young male and female, old female customers and employ more promotion strategies to bring in more customers without reducing the price of its products significantly.


