# Johns Hopkins Univeristy Data Science Fellowship
# Predicting Flight Delays with Weather
Cameron Czerpak

# Background
Over 220,000 US flights were delayed in 2019 (Bureau of Transportation Statistics).
Delays cost airlines $30 billion a year in lost revenue (Cirium) and hamper roughly 20% of the 4.5 billion yearly airline passengers worldwide (ICAO).
Frequent fliers rely on 3rd party flight tracking apps like Flight Aware to get updates on their travel plans.

# Current Methods Flight Aware
When Booking - View average departure and arrival delay on FlightAware.
Day of flight - Check if the inbound flight is delayed Google/FlightAware.
Frequent fliers will notice trends between the weather and fligth dealys on the Flight Aware Misery Map https://flightaware.com/miserymap/. However, noticing these trends requires experience and intuition.

# Objective
Aim: To build a tool that predicts flight delays from historical flight and weather data.  
Schedule extra travel days before important events  
Fly into a different airport hub to make connection

# Methods
Data: Kaggle (Flights 2014-2018), National Centers for Environmental Information (Weather 2014-2018)  
Outcome: Arrival - On time/Delayed  
Model: Classification (XGBoost, Random Forest) (80% Training, 10% Validation, 10% Testing)  
Avoiding data leakage: 2014-17 Train, 2018 Half Test Half Validation

# Exploration
The data was biased to on time with 36% fewer delayed flights  
Southwest was overrepresented in the dataset with 50% more flights than American Airlines, the largest US carrier https://en.wikipedia.org/wiki/List_of_largest_airlines_in_North_America  
The average flight delay was under 15 minutes  
Weather data was simplified to the average percipitation and rainfall for 7 regions in the US (New England, Great Lakes, Southeast, Midwest, Texas, Northwest, and Southeast)

# Features and Cleaning
Airline, Origin, and Destination were the most valuable categories. However, using dummies (pandas.get_dummies) increased the dataset from 30 columns to 444 columns per year, with each year being >16GB.
The dataset was reduced to the major 4 US carriers (WN, DL, UA, AA) and top 30 US airports. The top 30 was chosen as it includes Midway, a Southwest focus airport in Chicago.

Airline (4x)  
Departure Time  
Arrival Time  
Distance  
Regional Temperature (7x)  
Regional Precipitation (7x)  
Day  
Month  
Holiday  
Origin airport  
Arrival airport  

# Outcomes
2014-17 Train, 2018 Test/Validation  
XGBoost - Training Accuracy 70.9%, Testing Accuracy 68.5%  
Random Forest - Training Accuracy 57.5%, Testing Accuracy 57.4%  
XGBoost with optimization - Training Accuracy 72.8%, Testing Accuracy 68.7%  
XGBoost All Airlines w/o Airport - Training Accuracy 65.7%, Testing Accuracy 65.7%  

# Day of Prediction
On the day of your flight, you can use Flight Aware to check if your incoming flight is delayed. The closest variable to represent this in the dataset is "Departure Delay".  
XGBoost - Training Accuracy 78.0%, Testing Accuracy 77.4%  
Note: Using a model with the Departure Delay feature dramatically reduces the scope of what the model can be used for.

# Conclusions
XGBoost best model 68.5% accuracy compared to Random Forest 57.4% accuracy  
Optimization with XGBoost <1%, but 3x training time (Google Colab)  
Dropping smaller airports and airlines +3% accuracy  
+8% higher prediction rate the day of the flight (when departure status is known)  

# Future Work
Higher accuracy is needed for the model to be deployed. Methods of improving the model include using the Flight Aware average delay data and including weather along the flight path as a feature. Longer term, I'd like to convert the model from binary classification to a set of outcomes (on time, small <15min, medium 15-30min, and large delay >30 min)
