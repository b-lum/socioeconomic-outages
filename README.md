# Socioeconomic and Infrastructure Factors in U.S. Power Outages

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



<h3>Temporal Features:</h3>
<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>OUTAGE.START</td>
      <td>Timestamp indicating when the power outage began</td>
    </tr>
    <tr>
      <td>OUTAGE.RESTORATION</td>
      <td>Timestamp indicating when power was restored</td>
    </tr>
    <tr>
      <td>YEAR</td>
      <td>Year in which the outage occurred</td>
    </tr>
    <tr>
      <td>MONTH</td>
      <td>Month in which the outage occurred</td>
    </tr>
  </tbody>
</table>
<sub>OUTAGE.START and OUTAGE.RESTORATION are engineered timestamp features created by combining the original date and time columns (OUTAGE.START.DATE + OUTAGE.START.TIME, and OUTAGE.RESTORATION.DATE + OUTAGE.RESTORATION.TIME).</sub>

<h3>Geographic & Regional Features:</h3>
<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>U.S._STATE</td>
      <td>U.S. state where the outage occurred</td>
    </tr>
    <tr>
      <td>POSTAL.CODE</td>
      <td>State postal abbreviation</td>
    </tr>
    <tr>
      <td>NERC.REGION</td>
      <td>North American Electric Reliability Corporation region</td>
    </tr>
    <tr>
      <td>CLIMATE.REGION</td>
      <td>Climate classification region of the state</td>
    </tr>
  </tbody>
</table>

<h3>Target Variable:</h3>
<sub>What we will eventually be predicting.</sub>

<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>OUTAGE.DURATION</td>
      <td>Duration of the outage in minutes</td>
    </tr>
  </tbody>
</table>

<h3>Outage Severity Features:</h3>
<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CUSTOMERS.AFFECTED</td>
      <td>Number of customers impacted by the outage</td>
    </tr>
    <tr>
      <td>DEMAND.LOSS.MW</td>
      <td>Megawatts of electricity demand lost during the outage</td>
    </tr>
  </tbody>
</table>

<h3>Socioeconomic & Urbanization Features:</h3>
<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POPULATION</td>
      <td>Total population of the state</td>
    </tr>
    <tr>
      <td>POPPCT_URBAN</td>
      <td>Percentage of the population living in urban areas</td>
    </tr>
    <tr>
      <td>POPDEN_URBAN</td>
      <td>Population density in urban areas</td>
    </tr>
    <tr>
      <td>POPDEN_RURAL</td>
      <td>Population density in rural areas</td>
    </tr>
  </tbody>
</table>

<h3>Infrastructure & Energy Market Features:</h3>
<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RES.PRICE</td>
      <td>Average residential electricity price (cents / kilowatt-hour)</td>
    </tr>
    <tr>
      <td>COM.PRICE</td>
      <td>Average commercial electricity price (cents / kilowatt-hour)</td>
    </tr>
    <tr>
      <td>IND.PRICE</td>
      <td>Average industrial electricity price (cents / kilowatt-hour)</td>
    </tr>
    <tr>
      <td>TOTAL.PRICE</td>
      <td>Average total electricity price (cents / kilowatt-hour)</td>
    </tr>
    <tr>
      <td>RES.SALES</td>
      <td>Residential electricity sales (Megawatt-hour)</td>
    </tr>
    <tr>
      <td>COM.SALES</td>
      <td>Commercial electricity sales (Megawatt-hour)</td>
    </tr>
    <tr>
      <td>IND.SALES</td>
      <td>Industrial electricity sales (Megawatt-hour)</td>
    </tr>
    <tr>
      <td>TOTAL.SALES</td>
      <td>Total electricity sales (Megawatt-hour)</td>
    </tr>
  </tbody>
</table>

## Data Cleaning & Exploratory Data Analysis