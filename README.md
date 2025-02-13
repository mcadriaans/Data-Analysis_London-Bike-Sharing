
# London Bike Share Analysis (2015-2017)

![image](https://github.com/user-attachments/assets/edb90b1e-203d-439f-8a0d-b12def24bba3)

Welcome to the London Bike Share Analysis repository. This project aims to analyze bike share data to uncover insights and answer key business questions. The repository includes an interactive Tableau dashboard, a Python notebook for Exploratory Data Analysis (EDA), and a markdown file with SQL business questions and answers.

## What is bike sharing?
Bike sharing is a transportation service in which bicycles are made available for shared use to individuals on a short-term basis, typically for a small fee or for free in some cases. It offers a convenient and eco-friendly way to navigate urban areas, providing an alternative to traditional modes of transport like cars and public transit.


## Project Overview
This project explores the London Bike Share dataset from 2015 to 2017. The analysis encompasses data cleaning, visualization, and statistical analysis to understand bike-sharing usage patterns in London.

## Repository Contents
* Exploratory Data Analysis Notebook (EDA.ipynb): Jupyter Notebook containing data exploration, cleaning, and initial analysis.
* Tableau Dashboard: Provides interactive visualizations of bike-sharing data + Guide to navigating the dashboard.
* SQL markdown which documents questions and answers to key business questions about the bike share data.

## Dataset 
*The London bike sharing dataset provides information on bike-sharing activity in London, capturing details such as the number of bike shares, weather conditions, temperature, humidity, wind speed, holidays, weekends, and meteorological seasons. This dataset helps analyze and understand factors affecting bike-sharing trends and patterns over time.*

### Source: 
The data was acquired from 3 sources:
>* https://cycling.data.tfl.gov.uk/ 'Contains OS data © Crown copyright and database rights 2016' and Geomni UK Map data © and database rights [2019] 'Powered by TfL Open Data'
>* freemeteo.com - weather data
>* https://www.gov.uk/bank-holidays



### Column details

| Column         | Description                               | Additional Information                              |
|----------------|-------------------------------------------|-----------------------------------------------------|
|**timestamp**   | Date and time data was grouped            |                                                     |
|**cnt**         | Count of new bike shares                  |                                                     |
|**t1**          | Actual temperature in Celsius             |                                                     |
|**t2**          |"Feels like" temperature in Celsius        |                                                     |
|**hum**         | Humidity in percentage                    |                                                     |
|**wind_speed**  | Wind speed in kilometers per hour         |                                                     |
|**weather_code**| Weather condition category                |1:clear, 2:scattered clouds, 3:broken clouds, 4:cloudy, 7:rain, 10:thunderstorm, 26:snowfall, 94:freezing fog |     
|**is_holiday**  | Boolean indicating if the day is a holiday| 1 for holiday, 0 for non-holiday                    |
|**is_weekend**  | Boolean indicating if the day is a weekend|1 for weekend, 0 for weekday                         |
|**season**      | Meteorological season                     | 0 for spring, 1 for summer, 2 for fall, 3 for winter|

## Technologies Used

*   Python (with libraries like Pandas, NumPy, Matplotlib, Seaborn)
*   SQL (PostgreSQL)
*   Tableau
*   Markdown

## Key Findings 

> *   Peak usage times are during weekdays, particularly during commute hours.
> *   Members tend to take longer trips than casual users.
> *   Certain stations are consistently more popular than others.
--------------------------------------------------------------------------------------------------------------------------------------------------------

