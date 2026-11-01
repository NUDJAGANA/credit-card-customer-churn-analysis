# Credit Card Customer Churn Analysis
![Credit Card Customer Churn Analysis](assets/Credit%20card%20Churn%20Image.png)

**Credit Card Customer Churn Analysis** is an exploratory data project focused on understanding why credit card holders leave a financial institution. By reviewing customer demographics, account activity, and transaction metrics, this project highlights key pattern shifts that signal when a credit card account is about to be cancelled.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

## Interactive Tableau Dashboards

- [Obsidian Intelligence / Command Center](https://public.tableau.com/app/profile/nadjat.djagana7788/viz/Creditcarddashboard_17935251019710/OBSIDIANINTELLIGENCECOMMANDCENTERCREDITCARDCHURN10127CUSTOMERS)
- [Behavior Signals](https://public.tableau.com/app/profile/nadjat.djagana7788/viz/Creditcarddashboard2/BEHAVIORSIGNALS)
- [Customer Segments](https://public.tableau.com/app/profile/nadjat.djagana7788/viz/Creditcarddashboard3/CUSTOMERSEGMENTS)

## Dataset Content

* **Source:** The dataset comes from the credit card **BankChurners** file hosted on Kaggle.
* **Size:** 10,127 individual records across 21 raw columns.
* **Target Variable:** `churn` (Created from `Attrition_Flag`: `1` represents a churned credit card customer, `0` represents an active customer).
* **Main Features:**
  * **Demographics:** `Customer_Age`, `Gender`, `Dependent_count`, `Education_Level`, `Marital_Status`, `Income_Category`.
  * **Account Information:** `Card_Category`, `Months_on_book`, `Total_Relationship_Count`, `Months_Inactive_12_mon`, `Contacts_Count_12_mon`.
  * **Spending & Activity:** `Credit_Limit`, `Total_Revolving_Bal`, `Avg_Open_To_Buy`, `Total_Amt_Chng_Q4_Q1`, `Total_Trans_Amt`, `Total_Trans_Ct`, `Total_Ct_Chng_Q4_Q1`, `Avg_Utilization_Ratio`.

## Business Requirements

* The bank's credit card retention team wants to reduce account cancellations and keep card revenue stable.

* **Requirement 1:** Check if demographic background (like age, gender, or income) plays a meaningful role in credit card churn.
* **Requirement 2:** Spot early warning signs in cardholder spending and activity, focusing on transaction counts (`Total_Trans_Ct`), spend totals (`Total_Trans_Amt`), revolving balance (`Total_Revolving_Bal`), and length of tenure (`Months_on_book`).
* **Requirement 3:** Measure how holding multiple bank products (`Total_Relationship_Count`) affects overall credit card retention.
* **Requirement 4:** Turn these insights into sensible, practical actions the bank can take before customers close their credit card accounts.

## Hypothesis and how to validate?

* 1. **Hypothesis 1:** Customers who have held their credit card longer (`Months_on_book`) are less likely to leave.
   * *Validation:* Plot `Months_on_book` distributions for active vs. churned customers using box plots and check the Pearson correlation coefficient.
   * *Outcome:* **False.** Credit card tenure length shows almost zero correlation with churn. Long-term cardholders walk away at the same rate as newer ones if they stop using their cards.
2. **Hypothesis 2:** Low transaction counts (`Total_Trans_Ct`) and low annual card spend (`Total_Trans_Amt`) are the main signs that a credit card customer is about to leave.
   * *Validation:* Use scatter plots mapping spend against transaction counts, colored by churn status.
   * *Outcome:* **True.** Activity level is the clearest indicator of account health. Most cancellations happen when a customer makes fewer than 50 transactions and spends less than $2,500 in a year on their card.
3. **Hypothesis 3:** Customers with more bank products (`Total_Relationship_Count`) stick around longer.
   * *Validation:* Compare credit card churn percentages across product counts using bar charts.
   * *Outcome:* **True.** Cardholders with only 1 or 2 total bank products leave at rates between 25% and 30%, while those with 5 or 6 products rarely leave (~10%).

## Project Plan
* **Data Setup:** Loaded the raw CSV, checked column types, verified missing entries, and reviewed the balance of active vs. churned credit card accounts.
* **Cleaning & Adjustments:** Cleaned up spacing issues in column headers, handled unexpected string formatting, mapped the target variable `churn`, and dropped unnecessary benchmark columns.
* **Exploratory Data Analysis:** Worked through two separate notebooks:
  * *Notebook 01:* Focused on data cleaning
  * *Notebook 02:* Looked at the target split and demographic variables and spending patterns (`Total_Trans_Amt`, `Total_Trans_Ct`, `Total_Revolving_Bal`, `Months_on_book`) and generated correlation matrix heatmaps.
* **Reporting:** Translated technical visual patterns into simple business insights for the credit card operations team.

* I used a [GitHub Project Board](https://github.com/users/NUDJAGANA/projects/8) to plan, structure, and track my progress throughout the development of this project.

## The rationale to map the business requirements to the Data Visualisations
* BR1 (Demographic Analysis): Used Countplots to compare churn distribution across demographic features like gender, marital status, and income levels.

* BR2 (Behavioral Signals): Used Scatter Plots and Box Plots (Total_Trans_Amt, Total_Trans_Ct, and Total_Revolving_Bal) to pinpoint exact activity levels where churn risk rises.

* BR3 (Tenure Impact): Used a Scatter Plot (Total_Trans_Amt vs Months_on_book) to evaluate whether account longevity protects against attrition.

* BR4 (Product Depth): Used Bar Charts to measure churn rates by Total_Relationship_Count and quantify the value of cross-selling.

* BR5 (Feature Relationships): Used a Correlation Heatmap to visualize overall linear associations between numerical features and the churn target.

## Analysis techniques used
* **Descriptive Statistics:** Calculated summary metrics (`mean`, `median`, `std`, `IQR`) to establish baselines for spending, balances, and customer activity.
  * **Bivariate and Multivariate Visualizations:** Built scatter plots, box plots, countplots, and bar charts using `Matplotlib` and `Seaborn` to analyze relationships between cardholder features and churn.
  * **Pearson Correlation Analysis:** Evaluated linear relationships between numerical columns and `churn` to identify which attributes move together.
* **Methodology Justification & Structure:**  
  The analysis followed a logical progression: starting with univariate distributions to understand individual features, moving to bivariate visualizations to compare active vs. churned customers, and concluding with multivariate checks and correlation analysis. This step-by-step structure ensured patterns were verified across multiple feature combinations before drawing conclusions.
* **Data Limitations & Solutions:**  
  The raw dataset contained minor column formatting inconsistencies (such as hidden trailing spaces and case-sensitivity differences like `Months_on_book`). These were addressed by stripping header whitespace (`df.columns.str.strip()`) and verifying exact column strings prior to plotting, avoiding unnecessary data dropping or heavy transformations.
* **Generative AI Usage (Gemini):**  
  All core Python, Pandas, and Seaborn code was written independently. Gemini was used as a targeted assistant to:
  * Troubleshoot Seaborn plot formatting issues and visual layout styling.
  * Verify exact column name alignment across code cells to resolve `KeyError` exceptions.
  * Assist with setting up the correlation matrix syntax and interpreting coefficient values.
  * Refine technical notes and observations into concise, plain-language business points.

## Technologies used
 * Visual Studio Code
 * Python
 * Jupyter notebook
 * Gemini

## Unfixed Bugs

* **`FutureWarning` in Seaborn:** Early visual steps printed warnings about palette assignments without explicit `hue` values. Fixed by adding `hue` parameters and setting `legend=False`.
* **Column Name Sensitivity (`KeyError`):** Plotted charts initially failed on `'Months_on_Book'` due to uppercase letters. Resolved by correcting the code to match the raw dataset name: `'Months_on_book'`.
* No unresolved errors remain in the final notebook code.

## Development Roadmap

### Challenges Overcome:
* **Inconsistent Header Names:** Stripped out hidden spaces using `df.columns.str.strip()` early in the work.
* **Metric Clarification:** Separated real balance dollars (`Total_Revolving_Bal`) from percentage utilization rates (`Avg_Utilization_Ratio`) to make findings clearer.

### Next Steps:
* **Predictive Modeling:** Build classification algorithms (like Random Forest or XGBoost) to score credit card churn risk on incoming accounts.
* **Interactive Tooling:** Move these visual charts into a simple Streamlit dashboard for team viewing.

## Main Data Analysis Libraries
* **Pandas:** Main tool for reading files, cleaning text columns, changing data types, and running correlation matrices.
  ```python
  numeric_df = df.select_dtypes(include=['int64', 'float64'])
  corr_matrix = numeric_df.corr()

* NumPy: Handled numerical arrays and helper calculations behind the scenes.

* Matplotlib: Set figure boundaries, adjusted layout spacing, and configured titles.

plt.figure(figsize=(8, 5))
plt.tight_layout()
plt.show()

* Seaborn: Used for fast statistical plots like scatter charts, heatmaps, and box plots.

sns.scatterplot(data=df, x='Months_on_book', y='Total_Trans_Amt', hue='churn')
sns.heatmap(corr_matrix, cmap='coolwarm', annot=False)

* Plotly

## Credits
This project references open-source tools, learning materials, public code repositories, and structural templates to support the analysis and presentation.
Gemini used for assistance with code generation, debugging, and formatting.
The Code Institute Learning Management System modules on Pandas and Data Visualisations with Matplotlib, Seaborn, and Plotly.

### Content
* Raw credit card dataset provided by Kaggle: [Credit Card Customers Churn Dataset](https://www.kaggle.com/).
* Reference project data repository: [Jane Weightman's Credit Card Churn Analysis on GitHub](https://github.com/Janeweightman/Credit-card-churn-analysis/tree/main/data).
* Formatting layout adapted from the official [Code Institute](https://codeinstitute.net/) template.
* Seaborn tutorials and documentation referenced for plotting techniques:
  * [Official Seaborn Introduction & Tutorial](https://seaborn.pydata.org/tutorial/introduction.html)
  * [GeeksforGeeks Guide on Data Visualization with Python Seaborn](https://www.geeksforgeeks.org/data-visualization/data-visualization-with-python-seaborn/)

### Media
* Code Institute brand logo retrieved from [Code Institute AWS S3](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png).


## Acknowledgements (optional)

* Thanks to Code Institute mentors, tutors, and community members for reviewing project steps, sharing feedback, and providing structural guidance.