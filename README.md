# Helsinki city bikes: Analysing location data with Uber's hexagon system

## Purpose
The idea of this project is to demostrate how to use's Uber's h3 hexagons to analyse location data. In this project we will use station and journey data from Helsinki city bikes.

## Helsinki city bikes
Helsinki city bike trips are often short, for example moving from metro station to target location and they are meant for making public transport more appealing by offering a quick way to transit between two locations. A user can grab a city bike from any station they want and return it to any city bike station they want (including full stations). City bikes are available roughly from March until October and a full season costs 35 euros (less than 40 US dollars). With the fixed fee one can use the city bikes as much as they want as long as the trip lasts less than 30 minutes. If the trip goes beyond 30 minutes, the user must pay 1 euro per every next 30 minutes. The user can also pay one-time trips but the cost is higher than with the seasonal subsciption.

## Uber hexagons
We will use Uber's hexagon system to cluster location data into certain size areas. More info can be found fro example Uber's blog: https://www.uber.com/en-FI/blog/h3/. We will use H3 library to map location data to geospatial indeces and tutorial for the package can be found from: https://h3geo.org/docs/. We will use h3 version 3.7.6 and the changes to version 4.x can be found from here: https://h3geo.org/docs/library/migration-3.x/functions.


## About the data
Helsinki city bikes journey data is available from 2016 to 2021 and the data is owned by City Bike Finland. One full season of data can be downloaded from `dev.hsl.fi/citybikes/od-trips-[year]/od-trips-[year].zip` by selecting the desired year, so for example http://dev.hsl.fi/citybikes/od-trips-2021/od-trips-2021.zip.

The info on the city bike stations can be downloaded from https://public-transport-hslhrt.opendata.arcgis.com/datasets/HSLHRT::helsingin-ja-espoon-kaupunkipyöräasemat-avoin/about.

The data is stored under separate directory `bike_data`.


### Data cleaning
The data columns are mixture of Finnish, Swedish and English so we translate all the relevant data to English.

There are also NaNs in essential features (for example station id or date) that we need to remove. There also some issues with the journey length (distance in meters) and duration (in seconds) that we need to take care of.

The data is not consisted throughout 2016-2021 and some stations ids from journey data cannot be found from stations data table which causes issues when merging trip data with stations data. All in all, we need to remove ~3% of journeys due to bad data quality.

We also add additional features to our data, including features derived from a date (hour, day, month, year, etc.) and hexagon ids with resolution 6 to 9 (corresponding areas with radiuses ~4km to 200m).

## Notebooks
In this project we have the following relevant notebooks:
1. `City-bikes-data-cleaning.ipynb`: cleaning and merging the data and saving it to one csv file.
2. `City-bikes-data-analysis.ipynb`: data analysis of the Helsinki city bike data.
3. `City-bikes-data-analysis-with-folium-maps.ipynb`: using folium package to plot interactive maps (time consuming and stiff method to analyse the data.)

### Virtual environment
Create virtual environment:\
`python3 -m venv city-bike-env`

Activate virtual environment:\
`source city-bike-env/bin/activate`

Install required packages:\
`pip install -r requirements.txt`

