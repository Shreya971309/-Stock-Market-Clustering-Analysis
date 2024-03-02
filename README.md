# Stock Market Clustering Analysis

## Overview
This project aims to perform clustering analysis on stock market data to assist Trade&Ahead, a financial consultancy firm, in providing personalized investment strategies to its clients. The analysis involves grouping stocks based on various financial indicators and characteristics, ultimately offering insights and recommendations for portfolio diversification and investment decisions.

## Problem Statement
The stock market offers numerous investment opportunities, but analyzing individual stocks and building a diversified portfolio can be challenging. Trade&Ahead seeks to leverage data-driven approaches to cluster stocks based on their financial metrics and characteristics. The goal is to identify groups of stocks with similar performance and risk profiles, enabling more informed investment strategies.

## Data Description

| Column Name                | Description                                                                           |
|----------------------------|---------------------------------------------------------------------------------------|
| Ticker Symbol              | An abbreviation used to uniquely identify publicly traded shares of a particular stock on a particular stock market |
| Company                    | Name of the company                                                                   |
| GICS Sector                | The specific economic sector assigned to a company by the Global Industry Classification Standard (GICS) that best defines its business operations |
| GICS Sub Industry          | The specific sub-industry group assigned to a company by the Global Industry Classification Standard (GICS) that best defines its business operations |
| Current Price              | Current stock price in dollars                                                        |
| Price Change               | Percentage change in the stock price in 13 weeks                                       |
| Volatility                 | Standard deviation of the stock price over the past 13 weeks                           |
| ROE (Return on Equity)     | A measure of financial performance calculated by dividing net income by shareholders' equity (shareholders' equity is equal to a company's assets minus its debt) |
| Cash Ratio                 | The ratio of a company's total reserves of cash and cash equivalents to its total current liabilities |
| Net Cash Flow              | The difference between a company's cash inflows and outflows (in dollars)             |
| Net Income                 | Revenues minus expenses, interest, and taxes (in dollars)                               |
| Earnings Per Share (EPS)   | Company's net profit divided by the number of common shares it has outstanding (in dollars) |
| Estimated Shares Outstanding | Company's stock is currently held by all its shareholders                            |
| P/E Ratio                  | Ratio of the company's current stock price to the earnings per share                    |
| P/B Ratio                  | Ratio of the company's stock price per share by its book value per share (book value of a company is the net difference between that company's total assets and total liabilities) |

## Project Structure
(click to expand)
<details>
  <summary><strong>Exploratory Data Analysis (EDA) Findings</strong></summary>
  
## Exploratory Data Analysis (EDA) Findings

### Data Integrity
1. **Duplicate Rows**: 
   - No duplicate rows were found in the dataset.

2. **Missing Values**: 
   - The dataset is complete; there are no missing values.

### Distribution Analysis
3. **Price Change Distribution**: 
   - The distribution of price change follows an approximately normal distribution.
<center> 

  ![price change](https://github.com/Shreya971309/-Stock-Market-Clustering-Analysis/assets/156785157/25f8e671-6488-4cec-ab4f-6529c6e57d26)

 </center>

### Sector Analysis
4. **Sector Performance & Financial Metrics**:
   <br> Among the GICS sectors, Industrials has the highest number of securities in the dataset, followed Financials and Healthcare.
<center> 
  
  ![GICS sector](https://github.com/Shreya971309/-Stock-Market-Clustering-Analysis/assets/156785157/df892ebd-9c99-42e3-84e6-444e542f813e)

  </center>
  
   - **Healthcare Sector**: Demonstrated the highest average price increase.
   - **Information Technology Sector**: Exhibited the highest average Cash Ratio and P/E Ratio.
   - **Utility Sector**: Recorded the lowest average Cash Ratio.

 <img src="https://github.com/Shreya971309/-Stock-Market-Clustering-Analysis/assets/156785157/1fad2247-6911-4f7e-a473-4df2a900100d" width="400" height="300"> <img src="https://github.com/Shreya971309/-Stock-Market-Clustering-Analysis/assets/156785157/45762b02-31a4-4d2d-a6ec-78d77147ec23" width="400" height="300">

<img src="https://github.com/Shreya971309/-Stock-Market-Clustering-Analysis/assets/156785157/4ca0ab72-c1e8-4c08-bf6e-08ad244651f3" width="400" height="300">



### Correlation Analysis
5. **Correlation between Financial Metrics**:
   - Net Income shows a moderately high positive correlation with Earnings per Share and Estimated Shares Outstanding (0.56 and 0.59 respectively).
<center>   
  
![correlation](https://github.com/Shreya971309/-Stock-Market-Clustering-Analysis/assets/156785157/af74ecd0-455e-4410-9bae-d76c17879e03)


</center>


</details>

<details>
  <summary><strong>Data Preprocessing</strong></summary>

  <h2>Data Preprocessing</h2>
  
  - **Duplicate Rows and Missing Values**:
    - Since there are no duplicates and null values in the dataframe, it doesn't require any treatment for those.

  - **Outlier Treatment**:
    - In financial datasets, extreme values can sometimes be valid and represent exceptional events. For example, a sudden spike or drop in stock prices can be a legitimate outlier. Therefore, we do not treat the outliers in the dataset.

  - **Feature Scaling**:
    - We use StandardScaler to scale numerical columns excluding specified columns. This ensures that all numerical features are on the same scale, which is important for many machine learning algorithms.
  
</details>

<details>
  <summary><strong>Clustering Analysis</strong></summary>
  
# Clustering Analysis

Clustering is a technique utilized in unsupervised machine learning to group similar data points together based on specific features or characteristics. In this analysis, two clustering methods were employed: K-Means Clustering and Hierarchical Clustering.



  
## K-Means Clustering

**Introduction:**
K-Means is a partition-based clustering algorithm that divides the dataset into K distinct non-overlapping clusters. It aims to minimize within-cluster variance by assigning each data point to the nearest cluster centroid.

**Finding Optimal K Value:**
1. **Average Distortions:** Calculated the average distortions for different K values to identify the optimal number of clusters. Optimal K value: 4.
2. **Elbow Method:** Used the Elbow method by plotting the within-cluster sum of squares (WCSS) against the number of clusters.
3. **Silhouette Scores:** Calculated Silhouette scores for a range of K clusters to validate the optimal K value. Optimal K value: 4.

**Cluster Profiling:**

| Cluster | Characteristics |
|---------|-----------------|
| 0       | - Dominated by the Energy sector with the lowest current price and negative price change. <br> - Negative net income and earnings per share suggest loss-making companies. <br> - High ROE potentially inflated by negative net income and negative shareholders' equity. |
| 1       | - Represents a well-diversified cluster with representation from various sectors. <br> - Exhibits the highest current price and positive change in price, indicating stability with moderate volatility. <br> - Strong liquidity and financial health are observed with the highest cash ratio and net cash flow. |
| 2       | - Predominance of Financials with low but positive price change and the lowest volatility. <br> - Demonstrates the highest net income and moderately high earnings per share, indicating robust profitability. <br> - The cluster has the lowest P/E and negative P/B, signaling a cautious investment approach. |
| 3       | - High representation in Industrials, Financials, and Consumer Discretionary with stable profitability. <br> - Exhibits a high current price and moderate volatility, indicating stability with small gains. <br> - Moderate cash ratio and ROE suggest stable financial performance. |

## Hierarchical Clustering

**Introduction:**
Hierarchical Clustering builds a hierarchy of clusters by recursively merging or splitting clusters based on their proximity, offering a more flexible approach to clustering.

**Finding Optimal Distance Metric and Linkage Method:**
- **Cophenetic Correlation Coefficient:** Calculated for various combinations of distance metrics and linkage methods to determine the optimal combination. Obtained the highest coefficient (0.943) using Euclidean distance and average linkage.
- **Distance Metrics:** Evaluated metrics like Euclidean, Chebyshev, Mahalanobis, and Cityblock.
- **Linkage Methods:** Examined methods including single, complete, average, centroid, ward, and weighted, noting the Ward linkage method's distinct clusters.

**Cluster Profiling:**

| Cluster | Characteristics |
|---------|-----------------|
| 0       | - Dominated by the Energy sector with the lowest current price and negative price change. <br> - Negative net income and earnings per share suggest loss-making companies. <br> - High ROE potentially inflated by negative net income and negative shareholders' equity. |
| 1       | - Represents a well-diversified cluster with representation from various sectors. <br> - Exhibits the highest current price and positive change in price, indicating stability with moderate volatility. <br> - Strong liquidity and financial health are observed with the highest cash ratio and net cash flow. |
| 2       | - Predominance of Financials with low but positive price change and the lowest volatility. <br> - Demonstrates the highest net income and moderately high earnings per share, indicating robust profitability. <br> - The cluster has the lowest P/E and negative P/B, signaling a cautious investment approach. |
| 3       | - High representation in Industrials, Financials, and Consumer Discretionary with stable profitability. <br> - Exhibits a high current price and moderate volatility, indicating stability with small gains. <br> - Moderate cash ratio and ROE suggest stable financial performance. |



<details>
  <summary><strong>Key: Metrics Definitions</strong></summary>

  ### Key: Metrics Definitions

| Metric                       | Definition                                                                                                                                                  |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **K-Means Clustering Metrics** |                                                                                                                                                             |
| Average Distortions          | Average distortions represent the average squared distances between each data point and its corresponding centroid within a cluster.                        |
| Elbow Method                 | The Elbow method is used to determine the optimal number of clusters by plotting the within-cluster sum of squares (WCSS) against the number of clusters. |
| Silhouette Scores            | Silhouette scores measure how similar an object is to its own cluster compared to other clusters.                                                          |
| **Hierarchical Clustering Metrics**|                                                                                                                                                         |
| Cophenetic Correlation Coefficient | The cophenetic correlation coefficient measures how well a dendrogram preserves pairwise distances between the original data points.                 |
| Distance Metrics             | Distance metrics define the distance between two data points in a multidimensional space.                                                                   |
|                              | - Euclidean: Straight-line distance between two points in space.                                                                                           |
|                              | - Chebyshev: Maximum absolute difference between corresponding coordinates of points.                                                                       |
|                              | - Mahalanobis: Measure of the distance between a point and a distribution.                                                                                  |
|                              | - Cityblock: Sum of absolute differences of coordinates.                                                                                                    |
| Linkage Methods              | Linkage methods determine how the distance between clusters is calculated.                                                                                  |
|                              | - Single: Minimum distance between points in different clusters.                                                                                            |
|                              | - Complete: Maximum distance between points in different clusters.                                                                                          |
|                              | - Average: Average distance between points in different clusters.                                                                                          |
|                              | - Centroid: Distance between the centroids of clusters.                                                                                                     |
|                              | - Ward: Minimizes the variance when merging clusters.                                                                                                        |
|                              | - Weighted: Weighted average distance between points in different clusters.                                                                                  |

</details>

</details>


<details>
<summary><strong>K-means vs Hierarchical Clustering</strong></summary>

## K-means vs Hierarchical Clustering


#### Number of Distinct Clusters:
Both techniques produced similar clusters. In K-means Clustering, approximately 81.5% of the stocks were in Cluster 0, while in Agglomerative Clustering, around 80% were in Cluster 3. Cluster 3 in K-means corresponds to Cluster 1 in Agglomerative Clustering, and Cluster 2 in K-means aligns with Cluster 0 in Agglomerative Clustering.

#### Observations in Similar Clusters:
For K-means clustering:
- Cluster 0: 277 observations
- Cluster 1: 11 observations
- Cluster 2: 27 observations
- Cluster 3: 25 observations

For Hierarchical Clustering:
- Cluster 0: 32 observations
- Cluster 1: 27 observations
- Cluster 2: 9 observations
- Cluster 3: 272 observations

Clusters 0 in K-means and 3 in Hierarchical Clustering, each with around 277 observations, appear to be similar.

#### Appropriate Number of Clusters:
Both K-means and Hierarchical clustering methods identified 4 clusters as the optimal number.
</details>

<details>
  <summary><strong>Actionable Insights and Recommendations</strong></summary>

  
### Actionable Insights and Recommendations

| **Cluster** | **Risk Level** | **Insights** |
|-------------|----------------|--------------|
| Cluster 0   | High           | - Stocks in this cluster pose high risk due to negative earnings and inflated ROE. <br> - Tailored for investors seeking potentially high-risk, high-reward opportunities. <br> - Suitable for those with a higher risk tolerance aiming for substantial returns in a speculative market. |
| Cluster 1   | Moderate       | - Moderate risk with strong financial health. <br> - Exhibits strong financial health, positive metrics, and reliable liquidity. <br> - Recommended for investors looking for stability without compromising potential returns. |
| Cluster 2   | Low            | - Low risk with limited growth potential. <br> - Ideal for risk-averse investors prioritizing stability over high returns. <br> - Provides a secure and steady financial environment with modest returns. |
| Cluster 3   | Moderate       | - Moderate risk with stable profitability. <br> - Well-diversified cluster offering stability, moderate profitability, and a balanced risk profile. <br> - Recommended for those seeking reliable investments with moderate growth potential. |

#### Additional Insights:
- High-risk clusters, primarily influenced by the energy sector, suggest diversifying into other sectors for a balanced portfolio.
- Cluster 1's robust presence of Health Care and Information Technology stocks indicates innovation and growth potential, making investments in these sectors promising for substantial and stable returns.

### Conclusion:
- Understanding the risk profiles and financial health of clusters can guide investors in making informed decisions, aligning their investment strategies with their risk tolerance and financial goals.

</details>


<details>
  <summary><strong>TL;DR : Project Summary</strong></summary>
  
<h2>TL;DR : Project Summary</h2>
  
### Objective
Analyze stock market data using K-Means and Hierarchical clustering techniques to identify distinct clusters of stocks based on various financial metrics.

### Approach
- **Data Preprocessing:** Cleaned and prepared the dataset, handling missing values and scaling features.
- **K-Means Clustering:**
  - Determined the optimal number of clusters (K=4) using average distortions, elbow method, and silhouette scores.
  - Identified four clusters with distinct financial characteristics, including risk levels and sector compositions.
- **Hierarchical Clustering:**
  - Explored various distance metrics and linkage methods to find the optimal combination for clustering.
  - Utilized the obtained combination to perform hierarchical clustering and profiled the resulting clusters.
- **Comparison:** Compared execution time, cluster distinctiveness, number of observations in similar clusters, and appropriate number of clusters between K-Means and Hierarchical clustering.

### Actionable Insights and Recommendations
Provided actionable insights and recommendations for investors based on the risk levels and financial health of the identified clusters:
- **Cluster 0:** High-risk stocks, potential for high rewards, suited for risk-tolerant investors.
- **Cluster 1:** Stable performers, moderate risk, strong financial health, recommended for stability.
- **Clusters 2 & 3:** Moderate risk, strong financials, suitable for risk-averse investors seeking reliability.

### Conclusion
The clustering analysis offers valuable insights for investors to diversify their portfolios, mitigate risks, and make informed investment decisions tailored to their risk tolerance and financial goals.
</details>
