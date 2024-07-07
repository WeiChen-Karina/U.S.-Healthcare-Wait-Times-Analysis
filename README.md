# U.S.-Healthcare-Wait-Times-Analysis
# 📌 Project Background 

One of the main reasons driving our decision in focusing on US Healthcare wait times was noticing the growing trend of how long it takes to get an appointment now compared to just a few years ago. Waiting for an extended period of time is something no one enjoys going through, but looking into the data collected by OECD we can see that just over the course of 6 years (2010-2016) patients waiting more than 1 month grew from 17 to 27 percent (OECD). Of course this could just be due to the fact that there are more people in the United States and as such waiting for an appointment would take longer, but we wanted to dive deeper to see what specific specialities may be more impacted and what age groups of patients wait longer.

Our project questions include:
- Is there a specific type of patient waiting a long time?
- How long do the patients wait before the doctor can see them?
- What type of staff do the hospital need?
- What days of the year are the busiest?
- How can we fix it?
- 
This project uses the datasets from [dataset](https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset/data).

<i>In collaboration with Fazil Ahmed, Richa Kapuskari, Shri Hari Sekar, Ziyue Zhang.</i>  

# 📊 Data Pre-Processing  
- Merging all dataset files:
  Combining all the four inpatient data files into one and outpatient data files into the other to make the analysis easier when running the machine learning algorithms. Below the code for combining the dataset files can be seen.
  
- Missing Values:
  The next step involved searching the rows to locate and determine if there were any null values. The search results yielded that there were no missing null values in any rows. However, the unnamed column was entirely empty and as such it was better to drop  that column in the analysis. The search results for this entire search can be seen below.
  
- Handling Categorical Data:
  The Age_Profile column had a range of ages divided into 0-16, 16-64, and 65+. This reflects the US methodology of categorizing people into working and non-working age populations. To make the analysis of the categorical data easier the decision was made to convert it to a dummy variable. Time_Bands was another variable which had a range of months for the wait time, so it was converted into numerical data. And finally, we dropped the Adult_Child column during implementation of the machine learning model because the Age_Profile is sufficient enough to tell if the person is an adult or child. The final code for our changes is shown below.


   <br>  
- The variables bed, bath, and house_size are positively correlated to price, meaning that the property price tends to increase as these features increase, as shown in the heat map below. (The redder the square, the weaker the correlation. The darker the gray or black, the stronger the correlation.)  
   <br>
      <img src="Images/img-02.png" width="500">
   <br>  
- In this dataset, New York appears to be the state with the highest average property price at over $1.4 million, whereas West Virginia appears to be the state with the lowest average property price, averaging around $62,000 per property. Additionally, the property price seems to increase in high-density urban areas such as New York City and parts of Boston, as shown in the map below.  
   <br>
      <img src="Images/img-03.png" width="500">
   <br>  
- Though New York and Massachusetts share similarities with their high average listing price, the features of these properties differ significantly. On a city-by-city comparison, the average house size in Massachusetts is much larger than that of New York. The smaller property size combined with the high price makes New York the state with the highest average price per square foot in this dataset.  
   <br>
      <img src="Images/img-04.png" width="500">
   <br>
- Georgia, West Virginia, and the Virgin Islands seem to have the highest average number of bedrooms and bathrooms per property.
   <br>
      <img src="Images/img-05.png" width="500">
   <br>

Highlighting these relationships helped us gain a deeper understanding of the data which offered valuable insight as we continued our analysis through machine learning models.  

# 👣 Model Selection and Training  
Naive Bayes, Logistic Regression, and Decision Tree are all three machine learning algorithms that can be used to deduce and determine a distribution of inputs based on a specific factor. This would test how correlated the input of information is and if we can make assumptions on the dataset at hand. The specific factor we wanted to use as our target value for testing was Time_Bands as that is the determining factor of how long a single patient ends up waiting for an appointment after they schedule it. Lastly, for our visualizations we chose to utilize Power BI as it effectively shows all the ins and outs of the patient data and allows us to utilize various graphs and charts to get a better idea of showing the information that has been collected.

- Naive Bayes:
  It is a simple, effective model and easy to implement. It also works well with large and categorical datasets. This perfectly suited our needs as most of the healthcare data was categorical. Below we have pasted the code we used as well as its associated confusion matrix.

- Logistic Regression:
  Logistic regression can scale effectively to large datasets and is less prone to overfitting. It tends to work better with smaller training sets too, which is beneficial considering the size of this dataset was not too large. As a result the test set itself would not be large either. Below is the code we used for the logistic regression model.

- Decision Tree:
  Decision trees are a versatile and generally a powerful machine learning algorithm. It works well with large datasets and can be combined into ensemble methods and  provide a measure of feature importance, indicating which features are more influential in making predictions. Below is our code & confusion matrix for the model.

#### Model Evaluation:


The final results for each machine learning model can be seen in the chart above. There are a few key takeaways from the overall accuracy and what we learned from it after cleaning up the data.
- The dataset is not made for machine learning models. This is a known issue within the medical industry as “the lack of clean, structured data is an overarching problem for organizations across every industry, but training and deploying value-adding machine learning models at scale requires companies to reimagine their approaches to data governance. Given that datasets from one organization rarely suffice for model training, engineers typically resort to obtaining patient data from other healthcare organizations. The problem is that the majority of these datasets are incompatible with each other” (Koptelov).
- Our target variable in the dataset contains multi-level classification (target variable has 7 classes), and as such it was more likely to generate a model with lower accuracy.
- The parameters recorded by the hospital do not provide a deep level of insight. For example, adding a column that indicates which doctors may or may not be at the hospital might provide more information as to why some departments are more impacted than others.
- Decision Tree with pruning having the highest accuracy level does show that even though our target variable had multi-level classification that the other points of data do provide a somewhat significant level of information gain that helps provide insight into why some may have longer wait times than others.
- There is always the possibility that data is simply random, and as such cannot be discerned. However, we will still utilize visualizations to see if this does hold true.

# 🧽 Data Cleaning  
1. We discretized the dependent variable.   
   <br>
      <img src="Images/img-06.png" width="600">
   <br>  
2. Then, we filled in the missing values with the mean and median values. Specifically, we used the median for the missing values in the acre_lot, house_size, and price columns. Additionally, rows with missing values in the city and zip_code columns were removed. Lastly, the records for Tennessee, South Carolina, and Virginia listings were removed because they contained a substantial amount of missing data.  
   <br>
      <img src="Images/img-07.png" width="600">
   <br>

This "cleaned" dataset served as our initial benchmark for subsequent machine learning experiments.  

# 🔍 Machine Learning Models  
### Random Forest Classifier    
- Without any pre-processing techniques, the results are as follows:  
   <br>
      <img src="Images/img-08.png" width="400">
   <br>  
The model predicts approximately 92% of instances correctly. The precision and recall of the model are relatively high, at 0.92, indicating a low rate of false positives and negatives. Additionally, the high F1-score implies that this model performs well. Overall, the initial benchmark for the Random Forest algorithm on this dataset demonstrates strong performance with high accuracy.  
- We attempted to enhance the model with random sampling, dummy variables for the state attribute, feature selection, binning, min-max scaling, and standardization pre-processing techniques. Random sampling reduced the dataset for additional features while maintaining a similar model accuracy. Implementing dummy variables for the state attribute did not change the accuracy. Since the number of attributes in the original dataset is not extremely large, feature selection was not useful. Binning underscored the nature of the data which decreased its accuracy. Standardization improved the previous pre-processing, but it had minimal effect on improving the accuracy.  
   <br>
      <img src="Images/img-09.png" width="400">
   <br>  
Overall, the Random Forest model that performed the best was the benchmark model (with no pre-processing). Many of the additional pre-processing techniques either worsened or had no impact relative to the original accuracy. However, a finding that was gained from the pre-processing was that price is likely to be influenced by location since adding the dummy variables for the state attribute improved the randomly sampled model.

### K-Nearest Neighbors Classifier  
- Without any pre-processing techniques, the results are as follows:  
   <br>
      <img src="Images/img-10.png" width="400">
   <br>  
This model predicts approximately 88% of instances correctly. The model's precision and recall are commendably high, at 0.87, suggesting a low frequency of false positives and negatives. The high F1-score further confirms the model's effectiveness. However, this model appears to be less accurate than the Random Forest model with a 92% overall accuracy.
- The pre-processing techniques that we employed were random sampling, an introduction of dunny variables for the states attribute, feature selection, binning, min-max scaling, and standardization. Most of the techniques were moderately effective, but they tended to distort the true nature of the data, leading to less accurate predictions. Standardization offered some improvement over the other pre-processing techniques. However, the impact it had on the overall accuracy was insignificant.     
   <br>
      <img src="Images/img-11.png" width="400">
   <br>  
Overall, the KNN model achieved optimal results when applied to the standardization of the bed, bath, acre_lot, and house_size attributes. The standardized KNN model achieved an 88.5% accuracy. a slight increase of 0.1% from the benchmark model.  

### Logistic Regression  
- Without any pre-processing techniques, the results are as follows:  
   <br>
      <img src="Images/img-12.png" width="400">
   <br>  
This model predicts approximately 70% of instances correctly. The model's precision and recall contained mixed results. As noted by the F1-score of 0.65 for the "high" class and 0.74 for the "low" class, this seems to suggest that the model is better at identifying the "low" class data points. Overall, this Logistic Regression model has room for improvement, particularly in capturing the "high" class data points.
- Similar to the Random Forest and KNN models, the pre-processing techniques that we employed were random sampling, an introduction of dunny variables for the states attribute, feature selection, binning, min-max scaling, and standardization. Implementing dummy variables for the states attribute increased the model's accuracy to 72%. Standardization and binning on the house_size attribute improved the model's accuracy to 75%.  
   <br>
      <img src="Images/img-13.png" width="400">
   <br>  
Overall, the Logistic Regression approach had better performance in two separate instances, binning on the house_size attribute and a combination of random sampling, dummy variables, and standardization. Both models achieved an accuracy of around 75%, an improvement of approximately 5% from the benchmark model.

# 🔑 Key Takeaways    
We implemented three machine learning models to predict whether a real estate listing could be classified as a "high" or "low" price listing. From our analysis, we concluded how different models reacted to a variety of pre-processing techniques. From our choice of pre-processing techniques, the best techniques seemed to involve a combination of random sampling, standardization, and dummy variables for the state attribute. The binning technique improved the Logistic Regression model significantly. However, binning also led to a significant decrease in the performance of the Random Forest and KNN models, suggesting the importance of retaining the original granularity for some features.  

For this dataset, the best model seemed to be the Random Forest algorithm with no pre-processing. This model had the highest accuracy of 92%. Property location also seemed to be the attribute that plays a significant role in price.  

# ☁️ Project Improvements  
This project was for the first machine learning class that I took, and it was also the first project where I applied machine learning algorithms. Knowing what I know now if I were to improve this project, I would focus on improving the Random Forest model using different boosting methods, such as Adaptive Boosting and Gradient Boosting.  
