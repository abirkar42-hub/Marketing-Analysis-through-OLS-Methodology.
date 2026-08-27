# Marketing-Analysis-through-OLS-Methodology.
The study measures how different market and consumer variables drive sales and purchasing decisions. It uses extensive OLS regression and standard ML technique to test relationships and provide reliable data estimates. Four distinct analytical models to examine variables and evaluate the significance, direction, and strength of each factor's impact on overall performance.

---

### 📊Description of the Metrics

* **ID**: Customer's unique identifier
* **Year_Birth**: Customer's birth year
* **Education**: Customer's education level
* **Marital_Status**: Customer's marital status
* **Income**: Customer's yearly household income
* **Kidhome**: Number of children in customer's household
* **Teenhome**: Number of teenagers in customer's household
* **Dt_Customer**: Date of customer's enrollment with the company
* **Recency**: Number of days since customer's last purchase
* **MntWines**: Amount spent on wine in the last 2 years
* **MntFruits**: Amount spent on fruits in the last 2 years
* **MntMeatProducts**: Amount spent on meat in the last 2 years
* **MntFishProducts**: Amount spent on fish in the last 2 years
* **MntSweetProducts**: Amount spent on sweets in the last 2 years
* **MntGoldProds**: Amount spent on gold in the last 2 years
* **NumDealsPurchases**: Number of purchases made with a discount
* **NumWebPurchases**: Number of purchases made through the company's website
* **NumCatalogPurchases**: Number of purchases made using a catalogue
* **NumStorePurchases**: Number of purchases made directly in stores
* **NumWebVisitsMonth**: Number of visits to company's website in the last month
* **AcceptedCmp1**: 1 if customer accepted the offer in the 1st campaign, 0 otherwise
* **AcceptedCmp2**: 1 if customer accepted the offer in the 2nd campaign, 0 otherwise
* **AcceptedCmp3**: 1 if customer accepted the offer in the 3rd campaign, 0 otherwise
* **AcceptedCmp4**: 1 if customer accepted the offer in the 4th campaign, 0 otherwise
* **AcceptedCmp5**: 1 if customer accepted the offer in the 5th campaign, 0 otherwise
* **Response**: 1 if customer accepted the offer in the last campaign, 0 otherwise
* **Complain**: 1 if customer complained in the last 2 years, 0 otherwise
* **Country**: Customer's location
  
---

### ❔Problem Statement
You're a marketing analyst and you've been told by the Chief Marketing Officer that recent marketing campaigns have not been as effective as they were expected to be. You need to analyse the data set to understand this problem and propose data-driven solutions.

### Section 01: Data Wrangling & Exploratory Data Analysis (EDA)

**Q: Are there any missing values or outliers in the dataset, and how were they handled?**  
**A:** Yes. The `Income` variable contained approximately 1% missing values, which were imputed using the **median** to account for right-skewness and extreme values. Outliers were present across several continuous variables, with spend categories (`MntFruits`, `MntFishProducts`, `MntMeatProducts`, `MntSweetProducts`, and `MntGoldProds`) exhibiting over 5% outlier density.

**Q: Which variables warranted statistical transformations and why?**  
**A:** A logarithmic transformation was applied to the spend variables (`MntFruits`, `MntFishProducts`, `MntMeatProducts`, `MntSweetProducts`, and `MntGoldProds`). This scaled down extreme values, normalised feature distributions, and reduced outlier leverage in downstream modelling.

**Q: What new features were engineered from the raw data?**  
**A:** Key engineered features and interaction terms include:
* `Total_Purchases`: Aggregate count of purchases across all channels.
* `Campaign_Success`: Total number of marketing campaigns accepted by a customer.
* `Married_PhD`: Binary interaction term for customers who are both married and hold a PhD.
* `Country × Campaign_Success`: Interaction term evaluating regional campaign responsiveness.
* Categorical encodings for `Education`, `Marital_Status`, and `Country`.

**Q: What notable patterns or anomalies were discovered during EDA?**  
**A:** 
* `Total_Purchases` positively correlates with total spends across product categories and overall `Income`.
* Higher education levels show a positive trend with increased wine expenditure.
* Higher-income customers exhibit positive trend to campaign conversion rates (`Income_clean` vs. `Campaign_Success`), but the correlation is weak.
* `Kidhome` negatively correlates with overall spend, income and purchase volume; households with more children rely more heavily on discounted purchases (`NumDealsPurchases`).
* High-volume gold buyers show a higher relative preference for Catalog ordering compared to Web or Store channels.

### Section 02: Statistical Analysis & Business Insights

**Q: What factors are significantly related to the number of in-store purchases?**  
**A:** Based on the regression analysis ($\alpha = 0.05$), the key statistically significant drivers of store purchases are:
* **Channel Activity**: `NumDealsPurchases`, `NumWebPurchases`, `NumCatalogPurchases`, `NumWebVisitsMonth`.
* **Income Earned**: `Income_Clean`
* **Purchase Time**: `Recency`
* **Demographics**: `Kidhome`, `Teenhome`, `Education_Level`, and residing in Spain (`SP`).
* **Campaign Interactions**: `AcceptedCmp2`, `AcceptedCmp4`, `Response`, `Campaign Success×IN`, `Campaign SuccessxSP`
* **Product Spend**: Log-transformed spend on fruits (`ln_MntFruits`), meat (`ln_MntMeatProducts`), and sweets (`ln_MntSweetProducts`).

**Q: Does the US perform significantly better than the rest of the world in total purchases?**  
**A:** No. The US ranks 6th overall in total transactions. **Spain (`SP`) leads all geographic regions** in total purchase volume.

**Q: Does purchasing an above-average amount of gold lead to more in-store purchases?**  
**A:** No. Although higher gold sales show a directionally positive association with store purchases in the regression model, the coefficient is **not statistically significant** at the 95% confidence level. Above-average gold spend is not a reliable predictor of store visits.

**Q: Do "Married PhD candidates" spend significantly more on fish, and what else drives fish sales?**  
**A:** No. The interaction term for `Married_PhD` shows a slight negative impact (-3.73% per unit shift) on fish sales, but the relationship is **statistically insignificant**. The variables that significantly drive fish spend are `Teenhome`, `NumWebVisitsMonth`, `AcceptedCmp1`, `Education_Level`,log-transformed spend on fruits, meat, sweets, gold and interaction variables `Campaign SuccessxCA`,`Campaign SuccessxGER`,`Campaign SuccessxSA`,`Campaign SuccessxSP`,`Campaign SuccessxUS`.

**Q: Is there a significant relationship between geographical region and campaign success?**  
**A:** No. Campaign effectiveness does not vary significantly by geographic region. While Mexico (`MX`) shows a slight positive lift relative to the baseline (Australia) at an 81% confidence level, the interaction between geography and campaign acceptance remains statistically insignificant overall.

### Section 03: Data Visualisation Insights

**Q: Which marketing campaign was the most successful?**  
**A:** The final campaign (**`Response`**) was the most effective overall, generating the highest conversion rate and driving the highest transaction volume compared to campaigns 1 through 5.

**Q: What does the average customer profile look like?**  
**A:** 
* **Birth Year**: 1969–1970 (~54–55 years old)
* **Household Income**: ~$52,000 / year
* **Education**: Master's degree (or equivalent graduate degree)
* **Household Composition**: ~1 child/teenager at home
* **Purchase Volume**: ~15 total transactions
* **Average 2-Year Spend**: Wine (303), Meat (167), Gold (44), Fish (38), Sweets (27), Fruits (26)

**Q: Which product categories are performing best?**  
**A:** **Wines** and **Meat Products** are the top-performing categories by revenue, generating substantially higher sales over the last 2 years than any other product line.

**Q: Which purchasing channels are underperforming?**  
**A:** **Deals** (`NumDealsPurchases`) and **Catalog** (`NumCatalogPurchases`) are underperforming, accounting for a lower transaction volume compared to Web and Store channels relative to average overall unit sales.

---

## 📝 Acknowledgement
  - **Data & Problem Statement:** https://www.kaggle.com/code/jennifercrockett/marketing-analytics-eda-task-final/notebook
  - **License:** Shared under the [MIT License](https://github.com/blob/main/LICENSE)
