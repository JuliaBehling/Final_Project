# Final Project: Wildfire Data Analysis 
  Julia Behling, Remi Harazim, Alejandra Dahl, and Meareg Mamo.

<img width="941" alt="Capture" src="https://user-images.githubusercontent.com/90812456/152652437-a6ec29f5-b687-4943-b34b-613e16e51cd3.PNG">

# Presentation:
### Topic Selection:
Our selected topic aims to predict what combined ecological factors best determine the likelihood of a G-Class Fire. G-Class fires are largescale burned areas, reaching a size greater than 5,000 square acres. Ecological factors include temperature, precipitation rates and availability of fire fighting resources. 

### Reason for Topic Selection:
The State of California has reached an unprecedented crisis in annual wildfire size and intensity. Decades of well-intended fire suppression techniques has led to an overabundance of combustible material throughout the natural landscape. Partnered with unparalleled high temperatures and drought, residents of California suffer from poor air quality, possibility of home loss, and risk to personal safety.  
California is a large mass with varying vegetation types, temperature, and moisture regimes. We selected this topic to determine if it is possible to predict wildfire size based on ecological factors. As wildfires continue to proliferate, and devastating events such as the Camp Fire in Paradise California (An event which led to the loss of over 11,000 homes and 85 deaths); Prediction models such as this will need to be utilized for the sake of public safety.

### Description of Source Data:
We will be applying the following data source for this analysis:

#### Data Source: 
* US Wildfire Data:
  * https://www.kaggle.com/capcloudcoder/us-wildfire-data-plus-other-attributes
  Contains U.S. wildfire data including date, cause, location, size, ecological factors and other identifiers.
* California Fire Facilities:
  * https://catalog.data.gov/dataset/cal-fire-facilities-for-wildland-fire-protection
  Contains geographical and contact information of California fire facilities

### Questions We Hope to Answer:
1.	Which ecological factors are the best predictors of large, catastrophic fires?
2.	Is there a statistically significant correlation between wildfire size to precipitation, humidity, wind speeds, temperature? 
3.	Does the distance between wildfire and the nearest fire facilities determine the size of the wildfire?
4.	Does funding/availability of resources affect the ability of different counties to fight wildfires in California?

### Description of Machine Learning Models
#### Data Preprocessing Procedure
Using Pandas, we filtered the data for only California wildfires with non-null ecological data. This left us with 1810 rows of data to work with that represent individual wildfire instances. We selected only the columns that contain relevant quantitative data such as  the fire size and the ecological factor measures (precipitation, humidity, wind, and temperature). For the Logistical Regression, we had to create a new column that transformed the fire_size_class column into a binary code, 1 translating to G and 0 being all other classes. 

#### Linear Regression Model
The dataset contains each fire's remoteness from the nearest city. We ran a linear regression to determine if there was a consistent linear correlation between the distance of fire prevention resources to the actual location of the fire and the total size of the fire. This model was limited by the presence of outliers within th data, so it proved to be less reliable than other methods for determining a factor's effect on fire size. Just looking at the scatter plot, we can see that there is probably not a clear correlation between remoteness and fire size. We measure the accuracy of this model by using Mean squared error and R squared. A good MSE score will be close to zero, while a good R2 score will be close to 1. Our model output a mean squared error (MSE) of 309628646.2035853, and a R squared of 0.1790542079474. We can determine from these measures that remoteness does not correlate linearly with fire size. 

<img width="443" alt="LinearScatterPlot" src="https://user-images.githubusercontent.com/90812456/155905613-7ff25dd5-c306-41ae-8b35-6053668e6039.png">

#### Logistic Regression Model
Fires given a class 'A', 'B', 'C', 'D', 'E', 'F' or 'G' determine by their size, 'A' being the smallest and 'G' the largest. Since we have these fire size classes, we wanted to see if a machine learning algorithm could predict the size class of a fire based solely on the weather readings and location data within the dataset. Originally, we used a binary classifier in sklearn to specifically predict G-class fires, the largest and most destructive class. Our goal was to make a model that could be fed current ecological data and determine the risk of a G-class fire so it could be addressed or even prevented before it even began. Then we adapted this model so that instead of a binary classification, it could predict each individual class, 'B' through 'G'. We had to change the solver from 'lbfgs' to 'newton-cg' so that it could handle a multi-class classification. After optimizing the model using GridSearch, our model reached a balanced accuracy score of 75%. This was somewhat lower than the score for the binary classifier, which output a balanced accuracy score greater than 90%. This model is relatively accurate in predicting either G-class or B-class fires because these are the two most common. It was less useful in predicting the fire size classes in between.

<img width="491" alt="LogisticRegressionScore" src="https://user-images.githubusercontent.com/90812456/155905212-8a295dea-acaa-4e57-8f25-0210afaa1d2a.png">

#### Random Forest Feature Selection Model
We wanted to know which ecological factors were the most useful in predicting the size of a wildfire, so we ran the data through a Random Forest Feature Selection algorithm. Random Forest was selected because it can determine the weight of individual factors on the value of a selected column. A clean dataframe was made with all the non-null California wildfire data. The 'X' data was assigned to the dataframe minus the "fire_size", "fire_size_class", and "state" columns, while the 'y' data was assigned to the "fire_size" column because that is what we want to test the weight of other factors on. The feature that had the most effect on determining fire size class was remoteness with a weight of 31%. The next highest was 'Humidity_cont' (the humidity at the time of containment) at 6% with 'Temp_cont' at 5%. Many of the weather measurements are similar in their weight, but the least useful was, surprisingly, precipitation. We believe this is due to the fact that precipitation can be 0 more than often.

<img width="429" alt="RandomForestFeatures" src="https://user-images.githubusercontent.com/90812456/155905234-4ecc952b-86b4-4529-8715-c1570094e78d.png">

### Dashboard

Google Slides Link:https://docs.google.com/presentation/d/1YJOw8q1KYfBv2fAENZplOx05uxCUmpCh1kpV7dWSmP0/edit?usp=sharing
Tableau Dashboard Link: https://public.tableau.com/app/profile/julia.behling/viz/California_Wildfires_16457586485670/FinalStory?publish=yes
We created our dashboard using Tableau's dashboard and storyboard features. There is a clear progression through the dashboard that tells the story of the project and the analysis we have done. We used Tableau to create maps of wildfires and wildfire prevention resources to compare. Maps and graphs are interactive in that the user may highlight or click on data points to see their individual data (e.g. fire size, fire facilities per county). The dashboard progresses from maps to graphs that give further context and analysis points.

