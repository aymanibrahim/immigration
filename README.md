# Summary

- Analysis of the immigration data using the US I94 immigration dataset that enriched with airport data, US city demographics and temperature data.
- Perform ETL operations on the datasets to generate star schema in parquet file format.


## [I94 Immigration Data](https://travel.trade.gov/research/reports/i94/historical/2016.html)
- comes from the US National Tourism and Trade Office. 
- includes information on visa category, age, and port of entry 

## [World Temperature Data](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data)
- comes from Kaggle.
- includes temperature data

## [U.S. City Demographic Data](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data)
- comes from OpenSoft.
- includes U.S. city demographic data

## [Airport Code Table](https://datahub.io/core/airport-codes#data)
- table of airport codes and corresponding cities. 


# Schema 
- Star schema that contains **1** fact table (**immigration**) and **3** dimension tables (**tempratures**, **demographics**, and **airports**)

## Fact Table
### immigration
> immigration data enriched by avarage temprature

| Column | Type |
| ------ | ----- |
| year | integer |
| month| integer|
| origin_city| string|
| destionation_city| string |
| travel_mode| integer |
| age| integer |
| arrival_date| date |
| departure_date| date |
| visa_category| integer |
| avgtemp| integer |

- partitioned by **destionation_city**.


## Dimension Tables

### temperatures
> city code, name and average temperature

| Column | Type |
| ------ | ----- |
| city_code | string|
| city_name| string|
| avgtemp| integer |

### demographics 
> city demographics including median age, Total population and number of foreign born.

| Column | Type |
| ------ | ----- |
| city | string|
| state| string|
| median_age| double|
| total_population| integer |
| foreign_born| integer|

- partitioned by: **state**.


### airports
> airport data including type, region and IATA code.

| Column | Type |
| ------ | ----- |
| airport_id | string|
| airport_type| string |
| airport_name| string |
| region| string| 
| municipality| string| 
| iata_code| string |

- partitioned by: **region** 
