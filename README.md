Socioeconomic and Infrastructure Factors in U.S. Power Outages

Modeling and predicting socioeconomic and infrastructure factors impact in U.S. Power Outages


## Introduction

Power outages disrupt homes, businesses, hospitals, and critical infrastructure across the United States. While extreme weather and equipment failures are often cited as the main causes, the duration of outages can also be influenced by structural factors such as population density, urbanization, and regional infrastructure characteristics.

This project investigates whether socioeconomic and infrastructure-related variables are meaningfully associated with outage duration. In particular, it examines whether differences in population structure, energy market characteristics, and regional context help explain variations in how long outages last.

The dataset comes from Purdue University's Laboratory for Advancing Sustainable Critical Infrastructure (LASCI) and includes 1,534 outage events with 57 variables across the U.S. From these, 23 features were selected for analysis based on their relevance to outage duration and regional infrastructure dynamics.


### Central Research Question
Do socioeconomic and infrastructure factors significantly influence power outage duration in the United States?

#### Why this matters:
<ul style="padding-left: 0; margin-left: 0; list-style-position: inside;">
  <li>Longer outages can disproportionately affect vulnerable communities.</li>
  <li>Identifying structural weaknesses can guide infrastructure prioritization.</li>
  <li>Urban and rural regions may experience systematically different recovery times.</li>
  <li>Policymakers need data-driven insights to improve grid resilience and equity.</li>
</ul>



### Temporal Features:
| Column Name        | Description                                      |
| ------------------ | ------------------------------------------------ |
| OUTAGE.START       | Timestamp indicating when the power outage began |
| OUTAGE.RESTORATION | Timestamp indicating when power was restored     |
| YEAR               | Year in which the outage occurred                |
| MONTH              | Month in which the outage occurred               |

<sub>OUTAGE.START and OUTAGE.RESTORATION are engineered timestamp features created by combining the original date and time columns (OUTAGE.START.DATE with OUTAGE.START.TIME, and OUTAGE.RESTORATION.DATE with OUTAGE.RESTORATION.TIME).</sub>

### Geographic & Regional Features
| Column Name    | Description                                            |
| -------------- | ------------------------------------------------------ |
| U.S._STATE     | U.S. state where the outage occurred                   |
| POSTAL.CODE    | State postal abbreviation                              |
| NERC.REGION    | North American Electric Reliability Corporation region |
| CLIMATE.REGION | Climate classification region of the state             |


### Target Variable
<sub>What we will eventually be predicting.</sub>
| Column Name     | Description                                           |
| --------------- | ----------------------------------------------------- |
| OUTAGE.DURATION | Duration of the outage in minutes                     |

### Outage Severity Features
| Column Name        | Description                                            |
| ------------------ | ------------------------------------------------------ |
| CUSTOMERS.AFFECTED | Number of customers impacted by the outage             |
| DEMAND.LOSS.MW     | Megawatts of electricity demand lost during the outage |

### Socioeconomic & Urbanization Features
| Column Name  | Description                                        |
| ------------ | -------------------------------------------------- |
| POPULATION   | Total population of the state                      |
| POPPCT_URBAN | Percentage of the population living in urban areas |
| POPDEN_URBAN | Population density in urban areas                  |
| POPDEN_RURAL | Population density in rural areas                  |


### Infastructure & Energy Market Features
| Column Name | Description                           |
| ----------- | ------------------------------------- |
| RES.PRICE   | Average residential electricity price (cents / kilowatt-hour)|
| COM.PRICE   | Average commercial electricity price  (cents / kilowatt-hour)|
| IND.PRICE   | Average industrial electricity price  (cents / kilowatt-hour)|
| TOTAL.PRICE | Average total electricity price       (cents / kilowatt-hour)|
| RES.SALES   | Residential electricity sales (Megawatt-hour) |
| COM.SALES   | Commercial electricity sales (Megawatt-hour)|
| IND.SALES   | Industrial electricity sales (Megawatt-hour)|
| TOTAL.SALES | Total electricity sales (Megawatt-hour)|


