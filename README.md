# E-commerce Sales Analysis

## Project Overview 
This project presents a sales analytics workflow for an e-commerce dataset.
It explores sales performance across countries, continents, traffic channels, devices, and product categories, and applies statistical methods to identify relationships between key business metrics.

💻 [**Project Notebook**](https://colab.research.google.com/github/Kornieks/E-commerce-Performance/blob/main/Final_Project_.ipynb) - You are more than welcome to explore code and visuals. 

**The analysis includes:**

* extracting data from Google BigQuery using SQl
* performing exploratory and statistical analysis in Python
* building  interactive analytical dashboards in Tableau

## Project Goals 
The main objectives of the analysis were: 

* identify top-performing continents and countries 
* analyze product category performance
* understand the impact of traffic sources and device types on sales
* evaluate the behavior of registered vs non-registered users
* analyze sales dynamics over time
* identify statistical relationships between key metrics
* analyse A/B testing results

## Tools 

* SQL (Google BigQuery)
* Python: NumPy, Pandas, Matplotlib, Seaborn, Scipy (statistical testing)
* Tableau Public

## Data OverView 
The dataset contains information about sessions of a particular online store, including orders from 2020-11-01 to 2021-01-31.
It consists of 349,544 rows and 18 columns (excluding the index).

12 columns contain **categorical data**, including information about continent, country, device, browser, mobile model name, operating system, language, channel info, channel, product category, product name, and product description.

2 columns are **identifier variables:** ga_session_id and customer_id (for registered customers).

2 columns contain **boolean data** describing email status: email_is_verified and email_is_subscribed.

1 column contains **numerical data:** product_price (USD).

1 column contains date/time information: dbdate (the date of the session), stored as a datetime variable.

A large portion of **missing values** was detected in several columns. These missing values are informative and reflect customer behavior (non-registered sessions and sessions without orders), rather than data quality issues. Therefore, no imputation was applied.

**Duplicate rows were not found.** The dataset was checked for exact and hidden duplicate rows. Where necessary text normalization was applied.

**Anomalities:** Using the IQR and Z-score methods potential outliers were identified in the product_price column, representing from 0.54% to 0.81% of the dataset. This suggests that extreme prices are rare and unlikely to distort the overall analysis. Also, this portion indicates that the mistake in entring data was not likely.

##  Key Business Insights 

* *Revenue distribution* accross countries is highly uneven with the United States dominating in total sales and sessions, accounting for 43.6% share of total revenue, while the bottom countries contribute insignificantly.
* We can see that revenue is driven primarily by traffic volume rather than  high average order sale.
* *There are five categories which make almost 80% of company's total revenue:*
```
Sofas & armchairs	          26.24%
Chairs          	          19.23%
Beds	                      15.39%
Bookcases & shelving units    11.39%
Cabinets & cupboards.         7.31%
```
*The pattern is largely consistent across the leading countries, particularly in the United States, which influences significantly the overall revenue distribution.
The revenue is highly concentrated in a few categories, which highlights strong dependence on core products. While this indicates clear strengths, it also suggests potential risk if demand shifts. Expanding focus on mid- and low-performing categories could help diversify revenue and capture additional growth opportunities.*
* The revenue distribution shows that Organic Search is the dominant channel, contributing 35.76% of total revenue. Paid Search follows with 26.62%, while Direct traffic accounts for 23.44%, indicating strong brand recognition and returning users. In contrast, Social Search (7.92%) and Undefined sources (6.26%) contribute relatively small shares of revenue.
  
*This highlights the importance of continued investment in SEO strategies, while also presenting an opportunity to optimize social and properly track undefined traffic sources to potentially increase their contribution.*

*The analysis reveals several important insights about user registration, purchasing behavior, and email engagement as well:*

1. Only a small portion of total sessions belongs to registered users - 7.99%. This suggests that the majority of traffic comes from unregistered (guest) users.

2. Despite being registered, only 0.8% of sessions result in an order. This indicates either:

   * weak conversion among registered users, or
   * that registration is not strongly linked to purchase intent.

3. Overall sessions with orders (9.59%)
   The overall purchase rate (9.59%) is significantly higher than the rate among registered sessions (0.8%).
   This may suggest that many purchases are happening from **guest users**, which could mean:

   * users prefer faster checkout without registration
   * the registration flow may create friction

4. High email verification rate (71.7%), which is positive.

5. Relatively low unsubscribe rate (16.94%). Over 83% of users remain subscribed, indicating healthy email retention and potential for lifecycle marketing campaigns.

*The Revenue Dynamics* plot shows significant fluctuations in revenue over the observed period. According to the rolling Average, there is a clear seasonal trend: sales rise in late November–December, then drop sharply towards the end of December. In January sales start recovering.

On average, there is almost no difference in revenue across weekdays. However,in total, Tuesday and Wednesday are High-Performing days. Performance  moderately decreases on Thursday until it declines almost by 25% on weekends.

## Statistical Analysis Insights:

* The Spearman correlation coefficient indicates a strong positive correlation between the number of sessions and revenue, which is statistically significant.
* Organic Search, Paid Search, and Direct demonstrate high correlations. *This suggests that improvements in search visibility and brand presence can generate compounded effects across multiple revenue streams.*
* The Mann–Whitney U test indicates a statistically significant difference in median revenue between registered and non-registered users. Although the central tendencies appear relatively close, the distribution for registered users shows greater variability and includes higher revenue values.

## 📊 [**Tableau Dashboard**](https://public.tableau.com/app/profile/kseniia.kornienko/viz/E-commercePerformanceDashboard_17716185145720/E-commercePerformanceDashboard?publish=yes)


# A/B Testing Analysis 

💻 [**Project Notebook**](https://colab.research.google.com/drive/1P11I3B2HW9fAvw9paVVJMuV_KijAP7dH?authuser=1#scrollTo=Vx3JkG0k9meL) - You are more than welcome to explore code. 


## Project Goal 

The objective of this part of the project is to analyze the results of an A/B test using statistical methods in Python and visualize key conversion metrics in Tableau.
The analysis evaluates whether differences between the control and test groups are statistically significant across several user conversion events in the purchase funnel.

## Statistical Significance Calculation (Python)

Instead of using online statistical calculators, the statistical significance was calculated programmatically using Python.
The analysis was designed to be scalable: the script processes arrays of metrics and uses loops so that additional metrics can easily be added without modifying the core logic of the code.

**For each metric the following values were calculated:**
* conversion rate for control and test groups
* absolute difference between groups
* statistical significance
* p-value
* confidence level

This approach allows the analysis to be automated for multiple tests and segmentation levels.

##  Overall A/B Test Results

Test #1

Statistically significant uplifts were observed in several mid-funnel metrics:
* Add payment info rate increased from 4.38% to 4.93% (+12%)
* Add shipping info rate increased from 6.69% to 7.13% (+6.5%)
* Begin checkout rate increased from 8.34% to 8.90% (+6.6%)

**The test variant positively impacted key mid-funnel conversion steps, while the overall purchase conversion remained statistically unchanged, suggesting that improvements in the funnel did not fully translate into completed transactions.**

Test #2
A statistically significant decrease was observed in view promotion rate, from 63.92% to 63.05% (-1.3%).

Test #3

Statistically significant downward trends were observed in:
* View promotion rate, from 58.77% to 58.15% (-1%)
* Begin checkout rate, from 13.61% to 13.15% (-3.3%)
** These results suggest that the test variant may have negatively affected user engagement at both early and mid-funnel stages.**

Test #4

Statistically significant decreases were observed in several metrics:
* View promotion rate, from 50.13% to 49.44% (-1.3%)
* Begin checkout rate, from 11.95% to 11.67% (-2.3%)
* New accounts rate, from 8.55% to 8.26% (-3.3%)

**This indicates a potential negative impact of the test variant on both user engagement and account creation.**

Although the dataset contains a large volume of observations, only a limited number of metrics show statistically significant differences between control and test variants. 
Additionally, most observed effects are relatively small in magnitude.

**This makes it difficult to draw strong product conclusions based solely on the current experiment results. The findings suggest that further investigation may be required, including deeper segmentation analysis (by device, country, or traffic source) or running the experiment for a longer period to collect additional data.**

Additional testing could help determine whether the observed patterns represent consistent behavioral changes or random variation in user behavior.

## 📊 [**Tableau Dashboard**](https://public.tableau.com/app/profile/kseniia.kornienko/viz/ABtestanaysis/FinalABtestanalysis?publish=yes)

