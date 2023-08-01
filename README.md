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
