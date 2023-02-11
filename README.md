# -EDA_Hotel_Booking_Analysis_Capstone_Project-JERUSALEM-19-
Project Type - EDA_Hotel_Booking_Analysis_Capstone_Project (JERUSALEM-19)
Contribution - Individual
Name - Aasheerwad sharma
Introduction -
So when ever we hear about hotel booking we always remember Ranveer Singh and Aliya Bhatt. Thanks to the Makemytrip for a big scale advertisement, even we can't get out of our head these advertisement. symply we can say Makemytrip is the main platform we use for hotel bookings. we usually consider prices per night, cleaness of hotel rooms, availability of free breakfast, main attraction distance from the hotel, and how far away hotel from the main market of city, we knows different types of bookings (Type of hotel & resort, duration of stay, types of hotel booking etc.)

Business Objective -
In this project I have got 2015 to 2017 (City Hotel & Resort Hotel) data where i am going to Analyse the data on bookings of City Hotel & Resort Hotel to check different factors which affect the booking. This is undertaken in this project, also i am going to indepth analysis to figure out the standard patterns of booking.

Data Information -
Hotel:

H1: Resort hotel
H2: City hotel

is_canceled:

1: Canceled 0: Not canceled

lead_time:

No of days that elapsed between entering date of booking into property management system and arrival date

arrival_date_year:
Year of arrival date (2015-2017)

arrival_date_month:
Month of arrival date (Jan - Dec)

arrival_date_week_number:
Week number of year for arrival date (1-53)

arrival_date_day_of_month:
Day of arrival date

stays_in_weekend_nights:
No of weekend nights (Sat/Sun) the guest stayed or booked to stay at the hotel

stays_in_week_nights:
No of week nights (Mon - Fri) the guest stayed or booked to stay at the hotel

Adults
Children
Babies
meal

Type of meal booked
Undefined/SC – no meal package
BB – Bed & Breakfast
HB – Half board (breakfast and one other meal – usually dinner)
FB – Full board (breakfast, lunch and dinner)

country:
market_segment (a group of people who share one or more common characteristics, lumped together for marketing purposes)

TA: Travel agents
TO: Tour operators

distribution_channel:
(A distribution channel is a chain of businesses or intermediaries through which a good or service passes until it reaches the final buyer or the end consumer)

TA: Travel agents TO: Tour operators

is_repeated_guest: (value indicating if the booking name was from repeated guest)

1: Yes
0: No

previous_cancellations:

Number of previous bookings that were cancelled by the customer prior to the current booking

previous_bookings_not_canceled:
Number of previous bookings not cancelled by the customer prior to the current booking

reserved_room_type:
Code of room type reserved. Code is presented instead of designation for anonymity reasons.

assigned_room_type:
Code for the type of room assigned to the booking. Sometimes the assigned room type differs from the reserved room type due to hotel operation reasons (e.g. overbooking) or by customer request. Code is presented instead of designation for anonymity reasons.

booking_changes:
Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation

deposit_type:
Indication on if the customer made a deposit to guarantee the booking. This variable can assume three categories: No Deposit – no deposit was made, Non Refund – a deposit was made in the value of the total stay cost, Refundable – a deposit was made with a value under the total cost of stay.

agent:
ID of the travel agency that made the booking.

company:
ID of the company/entity that made the booking or responsible for paying the booking. ID is presented instead of designation for anonymity reasons.

day_in_waiting_list:
Number of days the booking was in the waiting list before it was confirmed to the customer.

customer_type:
Contract - when the booking has an allotment or other type of contract associated to it.

Group – when the booking is associated to a group.

Transient – when the booking is not part of a group or contract, and is not associated to other transient booking.

Transient-party – when the booking is transient, but is associated to at least other transient booking.

adr (average daily rate):
average daily rate = Sum of all the Transaction/Total Number of Staying Night

required_car_parking_spaces:
Number of car parking spaces required by the customer.

total_of_special_requests:
Number of special requests like bed sharing (Twin or Double shring basis, or flor type )

reservation_status:

Canceled – To check booking was canceled by the customer,
Check-Out – When customer has checked out,
No-Show – Customer did not reach due to any reason on date of arrival.

reservation_status_date:
To check what was the last status to set. we use this to check when was booking cancel or when did the costumer checked out from hotel.

Importing required libraries for data manipulation, and visualisation
[ ]
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
Importing Hotel dataset to read data
[ ]
from google.colab import drive 
drive.mount('/content/drive')
Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).
[ ]
hotel_df = pd.read_csv('/content/drive/MyDrive/Hotel Bookings.csv')
Data Exploration
Given data set contaions information about City hotel & Resort hotel so let's check the data present in it.

[ ]
# Let's check the hotel data info 
hotel_df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 119390 entries, 0 to 119389
Data columns (total 32 columns):
 #   Column                          Non-Null Count   Dtype  
---  ------                          --------------   -----  
 0   hotel                           119390 non-null  object 
 1   is_canceled                     119390 non-null  int64  
 2   lead_time                       119390 non-null  int64  
 3   arrival_date_year               119390 non-null  int64  
 4   arrival_date_month              119390 non-null  object 
 5   arrival_date_week_number        119390 non-null  int64  
 6   arrival_date_day_of_month       119390 non-null  int64  
 7   stays_in_weekend_nights         119390 non-null  int64  
 8   stays_in_week_nights            119390 non-null  int64  
 9   adults                          119390 non-null  int64  
 10  children                        119386 non-null  float64
 11  babies                          119390 non-null  int64  
 12  meal                            119390 non-null  object 
 13  country                         118902 non-null  object 
 14  market_segment                  119390 non-null  object 
 15  distribution_channel            119390 non-null  object 
 16  is_repeated_guest               119390 non-null  int64  
 17  previous_cancellations          119390 non-null  int64  
 18  previous_bookings_not_canceled  119390 non-null  int64  
 19  reserved_room_type              119390 non-null  object 
 20  assigned_room_type              119390 non-null  object 
 21  booking_changes                 119390 non-null  int64  
 22  deposit_type                    119390 non-null  object 
 23  agent                           103050 non-null  float64
 24  company                         6797 non-null    float64
 25  days_in_waiting_list            119390 non-null  int64  
 26  customer_type                   119390 non-null  object 
 27  adr                             119390 non-null  float64
 28  required_car_parking_spaces     119390 non-null  int64  
 29  total_of_special_requests       119390 non-null  int64  
 30  reservation_status              119390 non-null  object 
 31  reservation_status_date         119390 non-null  object 
dtypes: float64(4), int64(16), object(12)
memory usage: 29.1+ MB
We can see out of 32 columns there are 04 columns which have missing values and some columns need to be conversion of datatypes, also need to add new columns to make analysis easier.

[ ]
#exploring the head of the data frame
hotel_df.head()

[ ]
#exploring the tail of the data frame
hotel_df.tail()

Let's find out how many number of rows and columns
[ ]
hotel_df.shape
(119390, 32)
[ ]
# let's check breif summary of dataframe
hotel_df.describe()

We can see that there are 32 columns in the dataframe but few columns 'Children','company','country', and 'agent' have NA and null values.

[ ]
#Let's creat a copy of dataframe so that our main data could not be change.
hotel_df1 = hotel_df.copy() 
Data Filtering and Cleaning unwanted data
[ ]
#Let's start first to removing duplicate rows in the data set.

# To check duplicate number of rows 
hotel_df1[hotel_df1.duplicated()].shape

#Droping duplicate values
hotel_df1.drop_duplicates(inplace = True)

# now let's check the shape
hotel_df1.shape

(87396, 32)
[ ]
#let's check how many NA and NULL values we have in data set 
hotel_df1.isnull().sum()
hotel                                 0
is_canceled                           0
lead_time                             0
arrival_date_year                     0
arrival_date_month                    0
arrival_date_week_number              0
arrival_date_day_of_month             0
stays_in_weekend_nights               0
stays_in_week_nights                  0
adults                                0
children                              4
babies                                0
meal                                  0
country                             452
market_segment                        0
distribution_channel                  0
is_repeated_guest                     0
previous_cancellations                0
previous_bookings_not_canceled        0
reserved_room_type                    0
assigned_room_type                    0
booking_changes                       0
deposit_type                          0
agent                             12193
company                           82137
days_in_waiting_list                  0
customer_type                         0
adr                                   0
required_car_parking_spaces           0
total_of_special_requests             0
reservation_status                    0
reservation_status_date               0
dtype: int64
As we can see there is lot of NULL values in agent and company. It's 100 % sure they can have impact on the analysis so for the better analysis We should remove these columns beacuse these columns are not much important.

[ ]
# let's remove agent and company column
hotel_df1.drop(['agent', 'company'], axis=1, inplace=True)
hotel_df1.head()


[ ]
# The number of missing valuse in country column is very low so we can the missing vale with a constant string 'Others'.

hotel_df1['country'].fillna(value = 'Others', inplace=True)
[ ]
#let's check number of missing values in column 'country'
hotel_df1.country.isnull().sum()
0
[ ]
#The number of missing values in column 'childern' is little as compare to the number of rows, so it will not affact much to analysis our data
#so here we can fill the missing value with the integer constant 0.

hotel_df1['children'].fillna(value = 0, inplace=True)

[ ]
# number of missing values in column 'children'

hotel_df1.children.isnull().sum()
0
Column Conversion of Data Type
Here we can see some columns require conversion to appropriate datatypes(float 64 to int 64) to make analysis easier

[ ]
hotel_df1.info()
<class 'pandas.core.frame.DataFrame'>
Int64Index: 87396 entries, 0 to 119389
Data columns (total 30 columns):
 #   Column                          Non-Null Count  Dtype  
---  ------                          --------------  -----  
 0   hotel                           87396 non-null  object 
 1   is_canceled                     87396 non-null  int64  
 2   lead_time                       87396 non-null  int64  
 3   arrival_date_year               87396 non-null  int64  
 4   arrival_date_month              87396 non-null  object 
 5   arrival_date_week_number        87396 non-null  int64  
 6   arrival_date_day_of_month       87396 non-null  int64  
 7   stays_in_weekend_nights         87396 non-null  int64  
 8   stays_in_week_nights            87396 non-null  int64  
 9   adults                          87396 non-null  int64  
 10  children                        87396 non-null  float64
 11  babies                          87396 non-null  int64  
 12  meal                            87396 non-null  object 
 13  country                         87396 non-null  object 
 14  market_segment                  87396 non-null  object 
 15  distribution_channel            87396 non-null  object 
 16  is_repeated_guest               87396 non-null  int64  
 17  previous_cancellations          87396 non-null  int64  
 18  previous_bookings_not_canceled  87396 non-null  int64  
 19  reserved_room_type              87396 non-null  object 
 20  assigned_room_type              87396 non-null  object 
 21  booking_changes                 87396 non-null  int64  
 22  deposit_type                    87396 non-null  object 
 23  days_in_waiting_list            87396 non-null  int64  
 24  customer_type                   87396 non-null  object 
 25  adr                             87396 non-null  float64
 26  required_car_parking_spaces     87396 non-null  int64  
 27  total_of_special_requests       87396 non-null  int64  
 28  reservation_status              87396 non-null  object 
 29  reservation_status_date         87396 non-null  object 
dtypes: float64(2), int64(16), object(12)
memory usage: 20.7+ MB
Datatype of children is given as float64. it need to be convert to int64.

[ ]
# converting the datatype of children int64
hotel_df1[['children',]] = hotel_df1[['children',]].astype('int64')
Datatype of reservation_status_date is given as object. it need to be convert into date format.

[ ]
# converting the datatype of reservation_status_date into date
hotel_df1['reservation_status_date'] = pd.to_datetime(hotel_df['reservation_status_date'], format= '%Y-%m-%d')
Columns addition
We are going to add some extra columns which will help during analysis

[ ]
# Adding total stays in nights

hotel_df1['total_stays_in_nights'] = hotel_df1['stays_in_weekend_nights'] + hotel_df1['stays_in_week_nights']

# Adding total number of guests as column

hotel_df1['total_guests'] = hotel_df1['adults'] + hotel_df1['children'] + hotel_df1['babies']

# changing the bool data from int to string for easy representation

hotel_df1['is_canceled'] = hotel_df1['is_canceled'].replace([1, 0], ['cancelled', 'not cancelled'])
hotel_df1['is_repeated_guest'] = hotel_df1['is_repeated_guest'].replace([1, 0], ['repeated guest', 'not repeated guest'])
[ ]
hotel_df1.head()

Exploratory Data Analysis
Overview of type of hotel
As we knows there are only 02 Types(resort & city), so we can use barchart or pie chart to show

[ ]
# Enlarging the pie chart
plt.rcParams['figure.figsize'] = 8,8

# Indexing labels. tolist() will convert the index to list for easy manipulation
labels = hotel_df1['hotel'].value_counts().index.tolist()

# Convert value counts to list
sizes = hotel_df1['hotel'].value_counts().tolist()

# As the name suggest, explode will determine how much each section is separated from each other 
explode = (0, 0.05)

# Determine colour of pie chart
colors = ['palegreen','pink']

plt.pie(sizes, explode=explode, labels=labels, colors=colors, autopct='%1.1f%%',startangle=90, textprops={'fontsize': 14})

Number of bookings for city hotel is more than the resort hotel. City hotels seems to be in more demand in compersion resort hotels.

Let's see which hotel seems to make more revenue ?

[ ]
grouped_by_hotel = hotel_df1.groupby('hotel')
d3 = grouped_by_hotel['adr'].agg(np.mean).reset_index().rename(columns = {'adr':'avg_adr'})   # calculating average adr
plt.figure(figsize = (8,5))
sns.barplot(x = d3['hotel'], y = d3['avg_adr'] )
plt.show()


Now can say that City hotel is makeing more revenue than Resort hotel.

let's find which month has the most number of bookings

[ ]
order = ['January', 'February', 'March', 'April', 'May', 'June', 
         'July', 'August', 'September', 'October', 'November', 'December']
ordered_hotel_df = hotel_df1[hotel_df1['is_canceled'] == 'not cancelled']['arrival_date_month'].value_counts().reindex(order)

plt.figure(figsize=(12, 10))
plt.plot(ordered_hotel_df.index, ordered_hotel_df.values, marker='o')
plt.xlabel('months')
plt.ylabel('count')
plt.xticks(rotation='horizontal')
plt.show()

Here we can see that Auguest month has most number of booking.

let's check number of people who booked the hotel.

[ ]
# Looking into adults. 
# Using groupby to group according to hotel types only.
hotel_df1['adults'].groupby(hotel_df1['hotel']).describe()

[ ]
# Looking into children. 
# Using groupby to group according to hotel types only.
hotel_df1['children'].groupby(hotel_df1['hotel']).describe()

It seems that mean values for adults is almost same but if we talk about children it's showing that resort hotels are in more demand than city hotels. so this means that resort hotels are better choice for large families.

Let's find out how long do people stay at the hotels?

[ ]
stay = hotel_df1.groupby(['total_stays_in_nights', 'hotel']).agg('count').reset_index()
stay = stay.iloc[:, :3]
stay = stay.rename(columns={'is_canceled':'Number of stays'})
stay

[ ]
plt.figure(figsize = (10,5))
sns.barplot(x = 'total_stays_in_nights', y = 'Number of stays',data= stay,hue='hotel')

So here we can see for the short stay > 6 Nights people like to stay in City hotels. and for the long Stay < 5 Nights people like to stay in Resort hotels.

Let's check how many booking were made by repeated guests.

[ ]
# Enlarging the pie chart
plt.rcParams['figure.figsize'] = 8,8

# Indexing labels. tolist() will convert the index to list for easy manipulation
labels = hotel_df1['is_repeated_guest'].value_counts().index.tolist()

# Convert value counts to list
sizes = hotel_df1['is_repeated_guest'].value_counts().tolist()

# As the name suggest, explode will determine how much each section is separated from each other 
explode = (0, 0.2)

# Determine colour of pie chart
colors = ['palegreen','pink']

plt.pie(sizes, explode=explode, labels=labels, colors=colors, autopct='%1.1f%%',startangle=90, textprops={'fontsize': 14})

Wow a very small percentage (around 04%) of bookings are made by repeated guests.

Let's find out which platform got most number of booking.

[ ]
group_by_dc = hotel_df1.groupby('distribution_channel')
d2 = pd.DataFrame(round(group_by_dc['lead_time'].median(),2)).reset_index().rename(columns = {'lead_time': 'median_lead_time'})
plt.figure(figsize = (10,5))
sns.barplot(x = d2['distribution_channel'], y = d2['median_lead_time'])
plt.show()

Here we can see TA/TO got the most number of bookings.

Let's check the canceled bookings

[ ]
hotel_df1['is_canceled'] = hotel_df1.is_canceled.replace([1,0], ['canceled', 'not_canceled'])
canceled_data = hotel_df1['is_canceled']

# Enlarging the pie chart
plt.rcParams['figure.figsize'] = 8,8

# Indexing labels. tolist() will convert the index to list for easy manipulation
labels = hotel_df1['is_canceled'].value_counts().index.tolist()

# Convert value counts to list
sizes = hotel_df1['is_canceled'].value_counts().tolist()

# As the name suggest, explode will determine how much each section is separated from each other 
explode = (0, 0.05)

# Determine colour of pie chart
colors = ['palegreen','pink']

plt.pie(sizes, explode=explode, labels=labels, colors=colors, autopct='%1.1f%%',startangle=90, textprops={'fontsize': 14})

In our analysis we found that people booked their hotel booking throught travel agent and tour operator. and we knows that it's very easy to cancel booking if we have booking thru to agents.

Final Conclusion
1. In our analyzation we found that there are only 2 category City hotels and Resort hotels and we see that city hotels are in more demand than resort hotels.

2. Now we can say that city hotels are making more revenue than resort hotels.

3. We found that in the month of august we got the greatest number of booking than other months.

4. When we compared adults and children booking in city hotel and resort hotel than we found that most of the adults almost liked both city and resort hotel same way. But when we see children, they liked resort hotels more than city hotels.

5. When we checked people stay period, we found that for the short stay less than 06 nights people like to stay in city hotels and for the long stay more than 05 nights like to stay in resort hotels.

6. When we check repeated guest, we found that a very small percentage (around 04 %) made booking.

7. When we checked which platform got the greatest number of bookings, we found that most of the people booked their booking thru to travel agent or tour operator.

8. When we checked that how many people cancelled their booking, we found that 27 % booking were cancelled due to some reasons. In our analysis we found that people booked their hotel booking throught travel agent and tour operator. and we knows that it's very easy to cancel booking if we have booking thru to agents.

