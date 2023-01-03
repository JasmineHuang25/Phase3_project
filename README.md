# Choosing the right deductible - Auto Insurance bodywork claim prediction

## Business understanding and request
Progressive insurance company would like to launch an inquiry function on their website to help their customers with finding the right deductible 
for them when purchasing or renewing a new policy.

### Choosing your deductible wisely will save you money!
Higher deductible = Lower car insurance rate and higher out-of-pocket costs
Lower deductible = Higher car insurance rate and lower out-of-pocket costs

(insert rate table)

## Project goal
To comply with the business request, the project goal is to predict auto bodywork damage per accident based on given conditions/features.  which will allow their customers to decide what deductible works best for them considering the predicted damage and their personal risk appetite. 

## Datasets
There are 3 datasets used in this project and they are owned and published by Chicago Police Department.
1. Traffic Crashes - Crashes (insert link)
2. Traffic Crashes - Vehicles (insert link)
3. Traffic Crashes - People (insert link)

## Project assumptions and limitations

1. Location: Chicago
Since the data were collected in Chicago, the models established in this project will only suitable for Chicago area.

2. Number of people injured: 0
The project focuses on auto body damage so the models only take in the accidents with NO people injured. 

3. Vehicle use: personal
Because the business is requesting for Personal Auto Insurance use, the models only selects data where ‘vehicle use’ is ‘personal’.  

4. Data period: 12/20/2021 - 12/31/2021
The data convered date range from 01/01/2016 to 12/31/2021 which contained more than 1 million of observations.  However, I could only process 1 month of data
or even less than a month due to the computer memory usage allowance.

5. Model target: 'DAMAGE'
There are 3 outcomes in ‘DAMAGE’, OVER $1,500 (63.3%), $501 - $1,500 (28.1%) and $500 OR LESS (8.6%).  This is an imbalanced data.
Re-group these 3 outcomes into 2, OVER $501 and $500 OR LESS, as the models target (y).

## Initial Exploratory Data Analysis and data preparation
1. Find out what factors affect auto insurance premium generally:
- Driving record: Better driving record gets better insurance premium.
- How much you use your car: Someone who drives more miles gets a higher insurance premium.
- Location: Where you live and where you park your car overnight may affect your car insurance premium. Urban neighborhoods typically have higher rates 
  of accidents, theft and vandalism than more rural areas, which means premiums may be higher.
- Age: Insurers generally charge more if teenagers or young people below age 25 drive the car.
- Gender: Statistically, women tend to get into fewer accidents, have fewer driver-under-the-influence accidents (DUIs) and most importantly, have less 
  serious accidents than men. So all other things being equal, women often pay less for auto insurance than their male counterparts.
- The car insured: The cost of the car is a major factor in the cost to insure it. Other variables include the likelihood of theft, the cost of repairs, 
  its engine size and the overall safety record of the car. Automobiles with high quality safety equipment might qualify for premium discounts.
- Driver’s credit: Similar to credit score, the credit-based insurance score is a statistical tool that predicts the likelihood of your filing a claim 
  and the likely cost of that claim.
- The type and amount of auto insurance coverage: The limits on the basic auto insurance, the amount of your deductible, and the types and amounts of 
  policy options (such as collision) that are prudent for you to have all affect how much you'll pay for coverage.
- NEVER race or religion: It is illegal to use race or religion to set insurance rates.

2. Initial findings from 3 datasets:
- ‘CRASH_RECORD_ID’ is the primary key for merging 3 different datasets.
- df_crash:  681683 rows and 49 columns
- df_people: 1494816 rows and 30 columns
- df_vehicle: 1389220 rows and 72 columns

3. Based on project assumptions, adjust the DataFrames:
- From df_crash, select ‘INJURIES_TOTAL’ = ‘0’
- From df_people, select ‘PERSON_TYPE’ = ‘DRIVER’
- From df_vehicle, select ‘UNIT_TYPE’ = ‘DRIVER’
- From df_vehicle, select ‘VEHICLE_USE’ = ‘PERSONAL’

4. Explore each column and decide what to keep:
- From df_crash: 'CRASH_RECORD_ID', 'CRASH_DATE', 'DAMAGE', 'INJURIES_TOTAL'
- From df_people: 'PERSON_TYPE', 'CRASH_RECORD_ID', 'ZIPCODE', 'SEX', 'AGE'
- From df_vehicle: 'CRASH_RECORD_ID', 'UNIT_TYPE', 'MAKE', 'MODEL', 'VEHICLE_USE'

5. Merge all 3 DataFrames on ‘CRASH_RECORD_ID’, drop all null.
6. Convert 'AGE' and 'VEHICLE_YEAR' Dtype from float64 to int for smaller data size.
7. Save the cleaned DataFrame as ‘df.csv’: Because the size of the original datasets is too large to upload to GitHub, save the cleaned 
  DataFrame to a csv file for uploading later. 



