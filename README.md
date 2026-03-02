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

I began by removing the column named "variables", which contained metadata describing each column header, as it was unnecessary and complicated the analysis. I also dropped the first row at index 0, which contained unit descriptions for the columns, since this information was redundant.

Next, I combined the "OUTAGE.START.DATE" and "OUTAGE.START.TIME" columns into a single "OUTAGE.START" column, represented as pandas datetime objects containing both the calendar date and timestamp for when the outage began. Similarly, I merged "OUTAGE.RESTORATION.DATE" and "OUTAGE.RESTORATION.TIME" into a single "OUTAGE.RESTORATION" column. These steps created clean, standardized timestamp features for subsequent analysis.

#### Cleaned DataFrame

<div style="overflow-x: auto; border: 0px; padding: 10px;">
  <table border="0" cellspacing="0" cellpadding="5">
    <thead>
      <tr>
        <th>OUTAGE.START</th>
        <th>OUTAGE.RESTORATION</th>
        <th>YEAR</th>
        <th>MONTH</th>
        <th>U.S._STATE</th>
        <th>POSTAL.CODE</th>
        <th>NERC.REGION</th>
        <th>CLIMATE.REGION</th>
        <th>OUTAGE.DURATION</th>
        <th>CUSTOMERS.AFFECTED</th>
        <th>DEMAND.LOSS.MW</th>
        <th>POPULATION</th>
        <th>POPPCT_URBAN</th>
        <th>POPDEN_URBAN</th>
        <th>POPDEN_RURAL</th>
        <th>RES.PRICE</th>
        <th>COM.PRICE</th>
        <th>IND.PRICE</th>
        <th>TOTAL.PRICE</th>
        <th>RES.SALES</th>
        <th>COM.SALES</th>
        <th>IND.SALES</th>
        <th>TOTAL.SALES</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>2011-07-01 17:00:00</td>
        <td>2011-07-03 20:00:00</td>
        <td>2011</td>
        <td>7</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>3060</td>
        <td>70000</td>
        <td>nan</td>
        <td>5.34812e+06</td>
        <td>73.27</td>
        <td>2279</td>
        <td>18.2</td>
        <td>11.6</td>
        <td>9.18</td>
        <td>6.81</td>
        <td>9.28</td>
        <td>2.33292e+06</td>
        <td>2.11477e+06</td>
        <td>2.11329e+06</td>
        <td>6.56252e+06</td>
      </tr>
      <tr>
        <td>2014-05-11 18:38:00</td>
        <td>2014-05-11 18:39:00</td>
        <td>2014</td>
        <td>5</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>1</td>
        <td>nan</td>
        <td>nan</td>
        <td>5.45712e+06</td>
        <td>73.27</td>
        <td>2279</td>
        <td>18.2</td>
        <td>12.12</td>
        <td>9.71</td>
        <td>6.49</td>
        <td>9.28</td>
        <td>1.58699e+06</td>
        <td>1.80776e+06</td>
        <td>1.88793e+06</td>
        <td>5.28423e+06</td>
      </tr>
      <tr>
        <td>2010-10-26 20:00:00</td>
        <td>2010-10-28 22:00:00</td>
        <td>2010</td>
        <td>10</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>3000</td>
        <td>70000</td>
        <td>nan</td>
        <td>5.3109e+06</td>
        <td>73.27</td>
        <td>2279</td>
        <td>18.2</td>
        <td>10.87</td>
        <td>8.19</td>
        <td>6.07</td>
        <td>8.15</td>
        <td>1.46729e+06</td>
        <td>1.80168e+06</td>
        <td>1.9513e+06</td>
        <td>5.22212e+06</td>
      </tr>
      <tr>
        <td>2012-06-19 04:30:00</td>
        <td>2012-06-20 23:00:00</td>
        <td>2012</td>
        <td>6</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>2550</td>
        <td>68200</td>
        <td>nan</td>
        <td>5.38044e+06</td>
        <td>73.27</td>
        <td>2279</td>
        <td>18.2</td>
        <td>11.79</td>
        <td>9.25</td>
        <td>6.71</td>
        <td>9.19</td>
        <td>1.85152e+06</td>
        <td>1.94117e+06</td>
        <td>1.99303e+06</td>
        <td>5.78706e+06</td>
      </tr>
      <tr>
        <td>2015-07-18 02:00:00</td>
        <td>2015-07-19 07:00:00</td>
        <td>2015</td>
        <td>7</td>
        <td>Minnesota</td>
        <td>MN</td>
        <td>MRO</td>
        <td>East North Central</td>
        <td>1740</td>
        <td>250000</td>
        <td>250</td>
        <td>5.48959e+06</td>
        <td>73.27</td>
        <td>2279</td>
        <td>18.2</td>
        <td>13.07</td>
        <td>10.16</td>
        <td>7.74</td>
        <td>10.43</td>
        <td>2.02888e+06</td>
        <td>2.16161e+06</td>
        <td>1.77794e+06</td>
        <td>5.97034e+06</td>
      </tr>
    </tbody>
  </table>
</div>


### Outage Duration Distribution

<iframe
  src="assets/html/duration_dist.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>

The distribution of OUTAGE.DURATION is right skewed. It has a max of 108653, minimum of 0, and a mean of roughly 2625.40.

### Customers Affected Distribution

<iframe
  src="assets/html/cust_affect.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>
The distribution of the amount of customers affected for each outage looks right skewed. It has a mean of 143456.22, minimum of 0, and a max of 3241437.0.