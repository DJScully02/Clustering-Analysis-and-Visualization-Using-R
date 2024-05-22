# Clustering-Analysis-and-Visualization-Using-R

## Table of Contents

- [Project Goals](#project-goals)
- [K-Means Clustering Analysis](#k-means-clustering-analysis)
- [Hierarchical Clustering Analysis](#hierarchical-clustering-analysis)
- [Model Based Clustering](#model-based-clustering)
- [Variable Clustering](#variable-clustering)
- [Variable Selection](#variable-selection)

### Data Sources
Meter Data: The primary dataset use for this analysis is the "Meter Data.xlsx" specifically from worksheet D, containing information about the state of the meters.

### Project Goals

1. **K-Means Clustering Analysis**
   - Apply k-means clustering to the predictor variables.
   - Justify the chosen number of clusters.

2. **Hierarchical Clustering Analysis**
   - Apply hierarchical clustering to the predictor variables.
   - Justify the choice of distance metric and clustering method.

3. **Model-Based Clustering Analysis**
   - Apply model-based clustering to the predictor variables.
   - Justify the assumed model used.

4. **Variable Clustering Analysis**
   - Apply variable clustering to the predictor variables.
   - Justify the chosen method of clustering.

5. **Variable Selection**
   - Perform variable selection on the predictor variables.
   - Justify the selection methods used.
   - Use at least one variable statistic and at least one model-based selection method.

### Tools
- R programming language - Data Analysis and Data Visualization

### Libarary's Used 


### K-Means Clustering Analysis

Our goals with K-Means Clustering were to find out how many clusters there should be as well as visualize what each group looked like in order to ensure the groups are distinct.

<p align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/c9963bd6-175a-412b-99b6-5739b57ccc5f" alt="K-Means Scree Plot">
</p>
The scree plot indicates that three clusters are optimal as the elbow point is observed at k=3. This suggests that three clusters capture the majority of the explained variance, making them the most suitable choice.

![k_means_results](https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/8c87ce5b-05b5-4e10-b6b7-51b2855e5724)
![k_means_clusters_w_elip](https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/db9bacc6-26dc-4edf-b591-349769c27719)

The visualizations above illustrate the three clusters. These plots demonstrate a clear distinction among the groups. Additionally, the plot with the confidence ellipses further confirms that the clusters are well-separated and distinct.

### Hierarchical Clustering Analysis

#### Clustering Methods Comparison

|           | median | single | centroid | mcquitty | average | complete | ward.D2 | ward.D |
|-----------|--------|--------|----------|----------|---------|----------|---------|--------|
| maximum   | 0.936  | 0.943  | 0.943    | 0.940    | 0.942   | 0.950    | 0.961   | 0.991  |
| euclidean | 0.919  | 0.928  | 0.942    | 0.937    | 0.943   | 0.945    | 0.984   | 0.996  |
| minkowski | 0.919  | 0.928  | 0.942    | 0.937    | 0.943   | 0.945    | 0.984   | 0.996  |
| canberra  | 0.822  | 0.856  | 0.858    | 0.888    | 0.900   | 0.908    | 0.984   | 0.997  |
| manhattan | 0.938  | 0.930  | 0.932    | 0.957    | 0.959   | 0.969    | 0.992   | 0.998  |

It appears that the Euclidean, Minkowski, and Manhattan distance metrics generally perform very well. Additionally, we observe that the ward.D and ward.D2 methods consistently yield the highest coefficients across all distance metrics tested, indicating they provide the best clustering quality for our dataset.

As we continue examining hierarchical clustering, we will use the Euclidean distance. While the Euclidean distance does not achieve the highest performance as seen in the table above, it is the most straightforward for most stakeholders to understand. As data scientists and analysts, we aim to make our methods and results easily comprehensible for all stakeholders.

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/5a63a9fa-896c-4efe-ba1d-5519a0681ef0" alt="Silhouette k = 2" style="width: 45%; margin: 10px;">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/69ab1fa5-c3db-4feb-9e1b-2975a5295859" alt="Silhouette k = 3" style="width: 45%; margin: 10px;">
   <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/563a29c5-bfb1-4e2b-a4ee-eadcae2ab854" alt="Silhouette k = 4" style="width: 45%; margin: 10px;">
   <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/3c4bc7ae-4630-43b0-8355-a5f111a2e994" alt="Silhouette k = 5" style="width: 45%; margin: 10px;">
</div>

With k = 4, we found the best silhouette width of 0.59, which indicates fairly good clustering quality. The principal component plot visually demonstrates how the hierarchical clustering categorizes the data into four distinct groups. This visualization helps to understand the distribution and separation of the clusters in the data set.


<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/336ed03d-1c8b-4e60-ba48-0f967694f2e8" alt="Dendrogram Euclidean Ward.D" style="width: 45%; margin: 10px;">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/3b9760a8-c0d2-44cf-83df-4461d60b6fc7" alt="Dendrogram Euclidean Single" style="width: 45%; margin: 10px;">
   <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/06794d56-846d-4bc7-a043-84d88a56860c" alt="Dendrogram Euclidean Average" style="width: 45%; margin: 10px;">
</div>



As mentioned earlier, we opted to use the widely recognized Euclidean distance. Additionally, we examined both Single Linkage, Average Linkage, and Ward's D methods. Upon reviewing the Single Linkage and Average Linkage dendrograms, it appears that observation 170 may be an outlier in the dataset. This observation should be reviewed in detail with domain experts to determine whether it should be excluded from the analysis. The Silhouette score for Ward's D method is particularly high, indicating good clustering quality. Therefore, after addressing the potential outlier, Ward's D method would be the preferred choice for clustering.

### Model Based Clustering
Here we will be using the Mclust library, 

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/17582408-ebaf-4058-915a-0c06dd2fb746" alt="Mclust BIC" style="width: 80%; margin: 20px;">
</div>

The BIC plot above compares the Bayesian Information Criterion values for various clustering models with three components. The model represented by the green circle (EII) has the lowest BIC value, indicating the best fit among the models tested. Other models, represented by different symbols, show higher BIC values, suggesting less optimal fits.

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/d4876ed3-389f-4bfa-89b2-57af05a8e22a" alt="EII Dendrogram" style="width: 45%; margin: 10px;">
</div>

### Variable Clustering

#### Transpose Method

| Distance Metric | single | mcquitty | average | complete | ward.D2 | ward.D | median | centroid |
|-----------------|--------|----------|---------|----------|---------|--------|--------|----------|
| binary          | 0.50   | 0.50     | 0.50    | 0.50     | 0.50    | 0.50   | 0.50   | 0.50     |
| manhattan       | 0.63   | 0.63     | 0.63    | 0.63     | 0.64    | 0.65   | 0.63   | 0.63     |
| maximum         | 0.60   | 0.60     | 0.60    | 0.61     | 0.61    | 0.63   |   NA   |   NA     |
| euclidean       | 0.62   | 0.62     | 0.62    | 0.62     | 0.63    | 0.64   |   NA   |   NA     |
| minkowski       | 0.62   | 0.62     | 0.62    | 0.62     | 0.63    | 0.64   |   NA   |   NA     |
| canberra        | 0.66   | 0.67     | 0.67    | 0.67     | 0.68    | 0.68   |   NA   |   NA     |

It appears that the Manhattan and Canberra distance metrics generally perform very well across most clustering methods. Additionally, we observe that the Ward.D and Ward.D2 methods consistently yield the highest coefficients across all distance metrics tested, indicating they provide the best clustering quality for our dataset. Notably, the maximum, Euclidean, and Minkowski distance metrics do not have values for the median and centroid methods, suggesting these methods may not be applicable or optimal for these distances in this context.
<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/3e6a6ad3-cc0b-4dce-88f2-ca46f9b1dd3c" alt="Transpose Method Dendrogram" style="width: 60%; margin: 15px;">
</div>

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/452210dc-022b-48d8-a4f0-eaac6ec05f45" alt="Transpose clusters" style="width: 60%; margin: 15px;">
</div>
While the table doesn't look like it provided the best results they do seem to have separated into clear groups.

#### ClusofVar


<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/35fe7fef-7406-4df0-8a49-59a99ff218c2" alt="ClustofVar Dendrogram" style="width: 60%; margin: 15px;">
</div>

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/5d52bb5f-1889-4c36-9018-3feb4075099c" alt="Stability Chart" style="width: 60%; margin: 15px;">
</div>

#### Hmisc::varclus()

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/a4ba4d70-4303-4e63-a5eb-ed18fd4d8fba" alt="Hmisc varclus" style="width: 60%; margin: 15px;">
</div>

##### Results

Based on the three methods analyzed above, we recommend the ClustOfVar method. Specifically, cutting into 3 or 8 groups appears optimal according to the stability graph, which suggests these cluster numbers provide the best results. The Transpose method is not recommended, as the resulting clusters appear too disordered and lack clear separation.

### Variable Selection

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/2ed78cdc-bef8-49c4-89ec-b59049f0f243" alt="Scree Variable Selection" style="width: 60%; margin: 15px;">
</div>

The Scree Plot shows the first 2 or 3 dimensions capture the majority of the explained variance and are therefore the best to utilize.

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/b61f2983-1314-45f6-ac31-a1f8d4588552" alt="Variable Selection Full Columns" style="width: 90%; margin: 15px;">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/472c6ab7-ba8a-42c6-8453-7561f9405cc6" alt="Variable Selection Individual Points" style="width: 60%; margin: 15px;">
</div>

<div align="center">
  <img src="https://github.com/DJScully02/Clustering-Analysis-and-Visualization-Using-R/assets/129353692/9ee28568-3b7d-401f-aa92-c9861755dea6" alt="Scree Variable Selection" style="width: 60%; margin: 15px;">
</div>
Above we seek to find what variables are most significant when compared with our target Health_State_of_Meter. We found that the variables that are likely to be the most strongly associated with the target variable Health_State_of_Meter.Are Gain5 and Gain6, with coefficients of 0.20, followed by Signal_Quality5, Signal_Strength2, and Signal_Strength1, all with coefficients of -0.20.
