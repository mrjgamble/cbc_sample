# CBC Digital Content Consumption Analysis

The purpose of this project is to gain insights into how Canadians consume digital content.  

The events analyzed in this write up occurred within the 23rd hour of 2018-04-01.  Prior to analyzing the data, the raw data was processed and cleaned.  Details around this process can be found in the [Data Import & Cleaning notebook](https://github.com/mrjgamble/cbc_sample/blob/master/notebooks/01_data_import_and_cleaning.ipynb).

The cleaned data was then used to generate insights and data visualizations.  This process is documented in the [Data Insights notebook](https://github.com/mrjgamble/cbc_sample/blob/master/notebooks/02_data_insights.ipynb).  

The results below come with a disclaimer: The dataset spans a single hour for one day.  As a result, trends are hyper specific to this hour and may not represent the population correctly.  This is an initial look at the data and is by no means intended to be an exhaustive analysis of the data.

#### Data Assumptions
Prior to diving into the data, there are several assumptions made regarding the data that need to be stated.

a. `client_event_time` was assumed to represent the actual time for which when an event occurred on the client side.

b. It was assumed that `insert_id` uniquely represented an event.  Duplicate `insert_ids` were removed from the dataset in order to ensure data was uniquely represented.

c. It was assume that 'amplitude_id' uniquely identified a user - effectively becoming the user_id.  As a result, counting the number of unique `amplitude_id` in a given query would provide the number of active users.

## Event Details
In total, there are 19 types of events captured in this dataset.  Events are verbs that describe an action taken by a user while consuming digital content.  For example, an event is recorded each time a user LOADED a webpage, or STREAMED a video.  

The list of events are as follows:

| Event | Frequency |
| --- |---:|
| LOADED | 67664 |
| READ | 24876 |
| session_start | 2906 |
| OPENED | 1721 |
| STREAMED | 1640 |
| LOADED MORE | 554 |
| session_end | 388 |
| CLOSED | 278 |
| SEARCHED | 189 |
| NEXT | 116 |
| COMMENTED | 69 |
| SELECTED | 66 |
| PREVIOUS | 21 |
| SIGNED IN | 19 |
| SIGNED OUT | 5 |
| SCANNED | 5 |
| SUBMITTED |4 |  
| OPTED IN | 4 |
| SUBSCRIBED | 2 |

The average number of events captured per minute is 1,675, peaking at 1,825 events during the 40th minute.  The distribution of events per minute is shown below:

![events per minute](https://github.com/mrjgamble/cbc_sample/blob/master/figures/event_distribution.png)

## Content Consumption By Location
The events captured within this dataset are generated by users spanning 108 countries.  Canada was not surprisingly at the top of this list with 40,448 active users.  Looking beyond Canada, it was found that the US, France and Australia also had significant active users.

![active users per country](https://github.com/mrjgamble/cbc_sample/blob/master/figures/active_users_per_country.png)

Focusing on Canada, we can see that the majority of users come from Ontario, British Columbia, and Alberta.  

![active users per province](https://github.com/mrjgamble/cbc_sample/blob/master/figures/active_users_per_province.png)

Based on city population alone, one would assume that Montreal, Vancouver and Toronto would top the charts when it comes to active users in Canadian cities.  The graph below shows otherwise.  Montreal is not in the top 10 cities.  Surprisingly, Calgary edges out Vancouver for the second spot.  This could be due to the time for which this data is captured, as it would be in late night for users on the Eastern side of Canada.

![active users per Canadian city](https://github.com/mrjgamble/cbc_sample/blob/master/figures/active_users_per_canadian_city.png)

Finally, grouping users based on language, we find the top 10 languages by active users are as follows:

| Language | Active Users|
|--- |---:|
| English | 43934 |
| French | 249 |
| Chinese | 54 |
| Spanish | 40 |
| Portuguese | 40 |
| German | 21 |
| Japanese | 18 |
| Korean | 11 |
| Russian | 10 |
| Vietnamese | 7 |

## Content Consumption By Device
The raw data provided event information related to device manufacturer, family, model, and type.  In an effort to perform a quick analysis of devices, a new column named `device_class` was created.  It simply classified the provided `device_type` as:

1. Desktop/Laptop
2. Phone
3. Tablet
4. Unknown  

Using this classification, we looked at the breakdown of device class for the top 6 countries (ranking based on active users).

Canadian users appear to consume content primarily on their phones.  Users from other countries are more likely to utilize a desktop/laptop or tablet.  We also found that there is trouble capturing `device_type` from users in France, as the majority of events do not contain valid device information.

![consumption by device](https://github.com/mrjgamble/cbc_sample/blob/master/figures/device_consumption_per_country.png)

## Content Consumption By Content Area
Finally we look at the consumption by content area, again focusing on the top 6 countries (ranking based on active users).

News by far is the most popular amongst the top 6 countries.  Radio also appears to be within the top 3 content areas for each country.  

Examining Canada, it appears that users are more likely to access the homepage - which might indicate that users in other countries access content through direct links or bookmarks.  This might indicate that content placed on the homepage is more likely to be missed by users outside of Canada.

![active users by content area](https://github.com/mrjgamble/cbc_sample/blob/master/figures/content_area_per_country.png)


## Conclusion
Understanding how users consume digital content allows us to better serve customers - focusing on the different trends of how, when, and where users are consuming content.  

Within this short analysis, we saw how consumption trends varied based on the country of origin.  

We also saw how a city population does not necessarily correlate to the number of active users.  This might mean Canadians within these cities are consuming digital content primarily from other sources - opening a door for growth in user base.   

#### Looking Forward
* Expanding this analysis to include a wider time range of data allows for broader data trends to emerge and also provides a more accurate representation of the user base.

* Since we were performing a brief data analysis, null data values where neither corrected or removed from the dataset.  If this dataset was to be utilized in a machine learning experiment, a suitable process for managing null data would be required on a column to column basis.

* It should be noted that a handful of data columns were dropped due to incomplete data.  It appears that several versions of data capture are in progress (as identified by `version_name`).  Standardizing data collection versioning may allow for a more complete dataset overall.
