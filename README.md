# CBC Digital Content Consumption Analysis

The purpose of this project is to gain insights into how Canadians consume digital media.

The events analyzed in this write up occurred within the 23rd hour of 2018-04-01.  Prior to analyzing the data, the raw data was processed and cleaned.  Details around this process can be found in the [Data Import & Cleaning notebook]([insert link])

The steps to creating the data visualizations found within this write up are detailed in the [Data Insights](f) notebook.  

This is an initial look at the data and is by no means intended to be an exhaustive analysis of the dataset.


## 1. Event Descriptions
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

![events per minute]()

## 2. Content Consumption By Location
*Note: The following analysis was performed with the assumption that the data column named 'amplitude_id' represents a unique user identifier.*  

Even though we are analyzing a small window of time, we find that content is being consumed by users spanning 108 countries.  

Canada was not surprisingly at the top of this list with 40,448 active users.  Looking beyond Canada, it was found that the US, France and Australia also had significant active users.

[inser graph of users per country]
![active users per country]()

Focusing on Canada, we can see that the majority of users come from Ontario, British Columbia, and Alberta.  

[insert graph users per provicne]
![active users per province]()

Based on city population alone, one would assume that Montreal, Vancouver and Toronto would top the charts when it comes to active users in Canadian cities.  The graph below shows otherwise.  Montreal is not even in the top 10 cities.  Surprisingly, Calgary edges out Vancouver for the second spot.  

[insert graph of Canadian city by active user]
![active users per Canadian city]()

The above results come with a disclaimer, as we are looking at a single hour that falls in the late night for some Canadians.    

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

## 3. Content Consumption By Device
The raw data provided event information related to device manufacturer, family, model, and type.  Although there was a wealth of information, the data itself required a large amount of manual work to properly classify and dissect device usage.  

In an effort to perform a quick analysis of device type, a new column named 'device_class' was created.  It simply classified a device as:

1. Desktop/Laptop
2. Phone
3. Tablet
4. Unknown  

Using this classification, we looked at the breakdown of device class for the top 6 countries (ranking based on active users).

The results below are surprising. Canadian users appear to consume content primarily on their phones.  Whereas users from other countries tend to use desktop/laptops and tablets more.  

Also, we find that an error must have occurred in capturing device type from users in France, as the majority of events do not contain valid device information.

![consumption by device]()

## 4. Content Consumption By Content Area
Finally we look at the consumption by content area, again focusing on the top 6 countries (ranking based on active users).

News by far is the most popular amongst the top 6 countries.  Radio also appears to be within the top 3 content areas for each country.  

Examining Canada, it appears that users are more likely to access the homepage - which might indicate that users in other countries access content through direct links or bookmarks.  This is interesting as it indicates that content on the homepage is more likely to be missed by users outside of Canada.

![active users by content area]()


## 5. Conclusion
In this analysis we reviewed digital consumption trends for users  where users accessed content from

Understanding how users consume digital content allows us to better serve customers - focusing on the different trends of how, when, and where users are consuming content.  

Within this short analysis, we saw how consumption trends varied based on the country of origin.  

We also saw how a city population does not necessarily correlate to the number of active users.  This might mean Canadians within these cities are consuming digital content primarily from other sources - opening a door for growth in user base.   

#### Looking Forward
* Expanding this analysis to include a wider time range of data allows for broader data trends to emerge and allows for a more accurate representation of the user base.

* Since we were performing a brief data analysis, null data values where neither corrected or removed from the dataset.  If this dataset was to be utilized in a machine learning experiment, a suitable process for managing null data would be required on a column to column basis.
