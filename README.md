# Final Project: Wildfire Damage Extent Compared to Available Relief Resources. 
  Julia Behling, Remi Harazim, Alejandra Dahl, and Meareg Mamo.

<img width="941" alt="Capture" src="https://user-images.githubusercontent.com/90812456/152652437-a6ec29f5-b687-4943-b34b-613e16e51cd3.PNG">

# Presentation:
### Topic Selection:
Our selected topic the compares correlation between the size of California's wildfires to the quantity of available fire relief resources within each County. 

### Reason for Topic Selection:
The State of California has reached an unprecedented crisis in annual wildfire size and intensity. Decades of well-intended fire suppression techniques has led to an overabundance of combustible material throughout the natural landscape. Partnered with unparalleled high temperatures and drought, residents of California suffer from poor air quality, possibility of home loss, and risk to personal safety.  

California is divided into 58 counties of varying population size and socieconomic stature. We selected this topic to determine if increased quantity and availability of fire-relief resources per County assit in mitigating wildfire size. As wildfires continue to proliferate, and devestating events such as the Camp fire in Paradise California (An event which led to the loss of over 11,000 homes and 85 deaths); Prediction models such as this will need to be utilized for the sake of public safety.

### Description of Source Data:
We will be applying 2 different data sources for this analysis:

* #### Data Source 1: US Wildfire Data:
  * https://www.kaggle.com/ananthu017/california-wildfire-incidents-20132020
* #### Data Source 2: California Fire Stations:
  *   https://catalog.data.gov/dataset/cal-fire-facilities-for-wildland-fire-protection

### Questions We Hope to Answer:
1.	Which ecological factors are the best predictors of large, catastrophic fires?
2.	Is there a statistically significant correlation between wildfire size to precipitation, humidity, wind speeds, temperature? 
3.	Does the distance between wildfire and the nearest fire facilities determine the size of the wildfire?
4.	Does funding/availability of resources affect the ability of different counties to fight wildfires in California?
### Description of Machine Learning Models
#### Data Preprocessing Procedure
Using Pandas, filtered the data for only California wildfires with non-null ecological data. This left us with 1810 rows of data to work with that represent individual wildfire instances. We selected only the columns that contain relevant quantitative data such as  the fire size and the ecological factor measures (precipitation, humidity, wind, and temperature). For the Logistical Regression, we had to create a new column that transformed the fire_size_class column into a binary code, 1 translating to G and 0 being all other classes. 
#### Linear Regression Model
The dataset contains each fire's remoteness from the nearest city. We ran a linear regression to determine if there was a consistent linear correlation between the distance of fire prevention resources to the actual location of the fire and the total size of the fire. This model was limited by the presence of outliers within th data, so it proved to be less reliable than other methods for determining a factor's effect on fire size. 

>Image Here (scatter plot graph)

#### Logistical Regression Model
Fires given a class A, B, C, D, E, F or G determine by their size, A being the smallest and G the largest. Since we have these fire size classes, we wanted to see if a machine learning algorithm could predict the size class of a fire based solely on the other data within the dataset. Using a binary classifier in sklearn, we wanted to know whether the model could predict specifically G-class fires, the most destructive and catastrophic designation. Our goal was to make a model that could be fed current ecological data and determine the risk of a G-class fire so it could be addressed or even prevented before it even began. Kind of like that movie Minority Report, only in this movie, Tom Cruise would be a short firefighter instead of a short detective.

>Image Here (Confusion matrix)

#### Random Forest Feature Selection Model
We wanted to know which ecological factors were the most useful in predicting the size of a wildfire, so we ran the data through a Random Forest Feature Selection algorithm. Random Forest was selected because it can determine the weight of individual factors on the value of a selected column. A clean dataframe was made with all the non-null California wildfire data. The 'X' data was assigned to the dataframe minus the "fire_size", "fire_size_class", and "state" columns, while the 'y' data was assigned to the "fire_size" column because that is what we want to test the weight of other factors on. 

>Image Here (bar graph)

### Dashboard
Google Slides Link:https://docs.google.com/presentation/d/1YJOw8q1KYfBv2fAENZplOx05uxCUmpCh1kpV7dWSmP0/edit?usp=sharing
We will be creating a dashboard using Tableau's dashboard and storyboard features. There will be a clear progression through the dashboard that will tell the story of the project and the analysis we have done. We will include the visualizations created during the analysis portion of the project. Graphs will be interactive in that the user may hover over data points to see their individual data. Users will also be able to zoom into the maps that display each wildfire location. The map will also be able to switch from fire data points to fire station location points. 

# GitHub
## Description of Communication Protocols:
This team has a private group in slack as well as a group text to communicate. Additionally, we have met via zoom meeting to complete this deliverable. 
