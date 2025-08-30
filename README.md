 # Outbound Tourism statistics II Quarter 2024-2025
---
 ### Overview
 - Distribution of expenditures in comparison with previous year's same quarter and all the neccessary measures. 
 - Distribution of travels by age group, gender and purpose of visits.
 - simple diagrams to illustrate outbound visited countries along with satisfaction level.

### Data Source
Data source was used from national statistics office of Georgia. files you can [Download Here](https://www.geostat.ge/en/modules/categories/578/outbound-tourism).

### Data Clearing and Preparation

For the cleaning purposes the following steps were applied in Power Query

1. Deleted *null* rows.
2. Use first row as headers.
3. Rounded to 2 decimals.
4. Filtered to 2024 and 2025 years.
5. **UNPIVOTED** some columns.
6. Created and marked as **DATE TABLE**.
7. Created table to map quarters as the source was in Roman letters.

### Exploratory Data Analysis

EDA involved exploring the data to answer the following questions. 

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/6f2f6c4f-e6a2-46d5-a0f2-0eeae243db14" /> 


- Top Expenditure categories.
- Previous quarter expenditures.
- Quarter Over Quarter expenditure growth.
- Previous Year expenditures.
- year over Year expenditure growth.
- AVG expenditure per category.
- Difference for travel volumes between 2024 and 2025 quarters.
- Distribution of Genders, Purpose of Visits, level of satisfaction and outbound visited countries.

### Data Analysis

List of DAX used for analysis

```DAX
Date = 
ADDCOLUMNS(CALENDARAUTO(),
            "Year", YEAR([Date]),
            "Quarter", QUARTER([Date])
            )
```

```DAX
AVG Expenditure = DIVIDE(
[Expenditures],SUM('Number of Visits'[Number of visits]))
```

```DAX
PQ Expenditure = 
IF(
    HASONEVALUE('Date'[Quarter]), 
    CALCULATE(
        [Expenditures],
        DATEADD('Date'[Date], -1, YEAR)
    ),
    BLANK()
)
```

```DAX
PY Expenditure = 
        IF(HASONEVALUE('Date'[Year]) && not HASONEVALUE('Date'[Quarter]),CALCULATE(Expenditure[Expenditures],
        DATEADD('Date'[Date],-1,YEAR)),blank())
```

```DAX
QoQ Growth = DIVIDE([Expenditures] - [PQ Expenditure],[PQ Expenditure])
```

```DAX
YoY Expenditure = CALCULATE([Expenditures],SAMEPERIODLASTYEAR('Date'[Date] ))
```

```DAX
YoY Growth = 
        DIVIDE([Expenditures] - [PY Expenditure],[PY Expenditure])
```




   
