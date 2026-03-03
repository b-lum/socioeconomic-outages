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

### Univariate Analysis

#### Outage Duration Distribution

<iframe
  src="assets/html/duration_dist.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

The distribution of OUTAGE.DURATION is right skewed. It has a max of 108653, minimum of 0, and a mean of roughly 2625.40.

#### Customers Affected Distribution

<iframe
  src="assets/html/cust_affect.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>
The distribution of the amount of customers affected for each outage looks right skewed. It has a mean of 143456.22, minimum of 0, and a max of 3241437.0.

### Bivariate Analysis

#### Customers Affected and Outage Duration Scaterplot

<iframe
  src="assets/html/OD_CA.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

There is a moderate positive correlation between outage duration and customers affected. The spearman coefficient is 0.5707. We use the spearman coefficient because the data appears right skewed.

#### Outage Duration and Total Price Scatterplot

<iframe
  src="assets/html/OD_TP.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

There is a weak negative correlation between total price and outage duration. Spearman's coefficient came out to -0.2249. That is the higher the total price which is the average among RES.PRICE (price for residential customers), COM.PRICE (price for commerical customers), and IND.PRICE (price for industrial customers). So it looks like theres a chance that the higher you pay, the lower your outage duration will be.

#### Outage Duration and Residential Price Scatterplot

<iframe
  src="assets/html/OD_RP.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

In line with total price, there is a weak negative correlation between Outage Duration and Residential Price. The Spearman correlation coefficient comes out to about the same as Outage Duration with Total Price, at roughly -0.2250.

#### Outage Duration and Population Percent Urban

<iframe
  src="assets/html/OD_PCTURB.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

There is a weak negative correlation between Outage Duration and Population Percent Urban. That is theres a likelihood that more urban regions benefit from shorter outages, whether from better infastructure or prioritization. In addition, the correlation may be weak because it is also harder to service urban areas due to interlocking grids, more complicated infastructure, etc. The Spearman coefficient comes out to about -0.1048.

### Interesting Aggregates

#### Total Price and Outage Duration by NERC Regions

> Note: Certain regions are missing start date times for outages so some plots will be more sparse. The absence of this is also significant.

<iframe
  src="assets/html/NERC_TP.html"
  width="800"
  height="900"
  frameborder="0"
></iframe>

Many regions appear to have some positive correlation from the eye test, such NPCC, SERC, and potentially TRE. The next section will analyze the missingness of OUTAGE.DURATION.

#### Aggregated Dataframe


<div style="overflow-x: auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>OUTAGE.DURATION</th>
      <th>TOTAL.PRICE</th>
    </tr>
    <tr>
      <th>NERC.REGION</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ASCC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[nan]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[nan]</td>
    </tr>
    <tr>
      <th>ECAR</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[6510.0, 5820.0, 3051.0, 4200.0, 3120.0, 7530.0, 8160.0, 3300.0, 5700.0, 3360.0, 2694.0, 4560.0, 7800.0, 5700.0, 7620.0, 5840.0, 2939.0, 3600.0, 5250.0, nan, 15950.0, 4920.0, nan, 4920.0, 5040.0, 11640.0, 3137.0, 7920.0, 1440.0, 6480.0, 8054.0, 6240.0, 126.0, 6685.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[7.54, 6.52, 7.18, 6.52, 7.47, 7.47, 7.22, 7.01, 6.62, 6.96, 7.18, 6.62, 6.62, 6.52, 7.47, 6.96, 7.22, 6.98, 5.8, 5.39, 5.57, 6.87, 6.83, 6.87, 7.31, 6.71, 7.04, 6.85, 6.4, 6.85, 7.16, 8.39, 6.85, 7.45]</td>
    </tr>
    <tr>
      <th>FRCC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[nan, 17.0, 240.0, 17520.0, 8189.0, 182.0, 5820.0, 83.0, 2009.0, 720.0, 155.0, 4320.0, 4320.0, 480.0, 1005.0, 221.0, 13430.0, 4320.0, 91.0, 1419.0, 3600.0, 10080.0, 5071.0, 152.0, 6840.0, 221.0, 24780.0, 38.0, 61.0, 7560.0, 90.0, 10380.0, 396.0, 2040.0, 12060.0, 1080.0, 1680.0, 13920.0, 14101.0, 1099.0, 2460.0, 540.0, 52.0, 816.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[nan, 10.16, 10.53, 8.86, 8.89, 10.11, 11.23, 9.89, 10.54, 8.93, 10.11, 8.07, 8.07, 8.18, 8.49, 8.09, 8.86, 8.07, 10.11, 11.72, 8.2, 8.89, 11.23, 10.16, 8.2, 8.18, 8.93, 10.11, 10.11, 8.2, 10.22, 8.2, 10.68, 8.2, 8.2, 8.93, 8.2, 8.18, 8.86, 8.18, 8.2, 10.54, 10.56, 7.87]</td>
    </tr>
    <tr>
      <th>FRCC, SERC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[372.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[8.58]</td>
    </tr>
    <tr>
      <th>HECO</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[543.0, 237.0, 1906.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[20.54, 21.45, 20.54]</td>
    </tr>
    <tr>
      <th>HI</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[1367.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[25.78]</td>
    </tr>
    <tr>
      <th>MRO</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[3060.0, 1.0, 3000.0, 2550.0, 1740.0, 1860.0, 2970.0, 3960.0, 155.0, 3621.0, 7740.0, 8880.0, 0.0, 1322.0, 60.0, nan, 135.0, 32.0, 8468.0, 44.0, 1605.0, 388.0, 480.0, 1219.0, 90.0, 18660.0, 538.0, 104.0, 60.0, 1272.0, 60.0, 251.0, 347.0, 1637.0, 21360.0, 2161.0, 2880.0, 13.0, 60.0, 4.0, 9600.0, 2140.0, 13650.0, 720.0, nan, 181.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[9.28, 9.28, 8.15, 9.19, 10.43, 8.28, 9.12, 7.36, 9.03, 10.0, 10.0, 7.03, 9.28, 8.7, 10.02, 10.98, 10.28, 11.1, 10.39, 10.28, 10.79, 10.17, 9.63, 6.65, 10.28, 10.26, 10.98, 11.1, 10.28, 11.1, 10.28, 8.13, 6.56, 7.73, 8.13, 7.46, 8.13, 7.68, 7.2, 6.2, 5.78, 7.46, 6.25, 7.56, nan, 7.67]</td>
    </tr>
    <tr>
      <th>NPCC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[nan, 11337.0, 2089.0, 20280.0, 14639.0, 2880.0, 681.0, 494.0, 1.0, 5355.0, 0.0, 3943.0, 3300.0, 191.0, 0.0, 73.0, 4680.0, 17310.0, 10080.0, 10726.0, 1.0, 5.0, 2515.0, 25920.0, 2730.0, 9480.0, 5400.0, 30.0, 3584.0, 3600.0, 5850.0, 4710.0, 1.0, 1732.0, 0.0, 23040.0, 1800.0, 6074.0, nan, 49.0, 2299.0, 5760.0, 420.0, 7320.0, 2880.0, 448.0, 2520.0, 18717.0, 5513.0, 21.0, 2100.0, 3120.0, 8221.0, 3240.0, 2880.0, 255.0, 2355.0, 161.0, 50.0, 258.0, 13140.0, 8640.0, 15492.0, 8268.0, 0.0, 300.0, 14400.0, 7962.0, 2400.0, 11296.0, 48.0, 60480.0, 1.0, 1.0, 160.0, 20.0, 1.0, 1.0, 70.0, 50.0, 15.0, 0.0, 1.0, 1440.0, 4560.0, 1.0, 1.0, 110.0, 210.0, 120.0, 0.0, 4260.0, 76.0, 210.0, 3305.0, 5880.0, 145.0, 60.0, 2640.0, 480.0, ...]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[14.64, 12.9, 12.51, 15.21, 15.21, 17.11, 10.54, 11.46, 17.11, 15.79, 15.65, 14.74, 15.98, 13.8, 17.08, 13.8, 11.62, 16.43, 17.25, 14.76, 14.71, 14.23, 14.71, 17.81, 16.94, 15.29, 14.76, 15.65, 15.24, 15.49, 15.09, 17.98, 17.08, 13.42, 15.49, 17.11, 16.94, 15.79, 13.64, 15.92, 17.11, 15.29, 17.2, 15.76, 15.65, 14.91, 15.76, 13.8, 13.42, 17.33, 11.9, 11.62, 17.11, 13.96, 17.11, 15.93, 16.94, 15.81, 17.98, 16.64, 15.62, 17.11, 15.62, 15.21, 15.89, 16.24, 15.09, 15.79, 11.93, 16.33, 15.92, 17.81, 14.79, 14.46, 14.78, 14.16, 14.7, 13.76, 14.04, 13.77, 14.12, 16.34, 15.95, 16.17, 18.22, 15.47, 16.35, 17.85, 15.5, 15.67, 16.11, 16.53, 17.44, 16.11, 17.5, 9.68, 14.82, 15.88, 18.33, 14.04, ...]</td>
    </tr>
    <tr>
      <th>PR</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[174.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[31.29]</td>
    </tr>
    <tr>
      <th>RFC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[3000.0, 108653.0, 960.0, 4410.0, 1.0, 1000.0, 17339.0, 9576.0, 3090.0, 1078.0, 1513.0, 4830.0, 2085.0, 5730.0, 4290.0, 2670.0, 3540.0, 3637.0, 1710.0, 4320.0, 3915.0, 4590.0, 5034.0, 4320.0, 1770.0, 9857.0, 4080.0, 5670.0, 1995.0, 300.0, 5115.0, 2670.0, 7650.0, 4338.0, 761.0, 5760.0, 2820.0, 4110.0, 3015.0, 232.0, 11525.0, 6420.0, 46080.0, 5700.0, 5610.0, 78377.0, 270.0, 4050.0, 5865.0, 1.0, 2325.0, 4170.0, 4485.0, 168.0, 5580.0, 705.0, 11850.0, 3494.0, 2760.0, 5760.0, 8922.0, 6030.0, 4242.0, 3120.0, 900.0, 1046.0, 3630.0, 1260.0, 5790.0, 2820.0, 600.0, 4259.0, 7080.0, 1588.0, 4260.0, 2700.0, 200.0, 8430.0, 85.0, 9150.0, 1019.0, 420.0, 1140.0, 7440.0, 4458.0, 1060.0, 12240.0, 4320.0, 120.0, 233.0, 65.0, 2120.0, 96.0, 3.0, 4320.0, 65.0, 2146.0, 96.0, 4032.0, 2580.0, ...]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[7.5, 10.28, 6.96, 7.69, 8.02, 7.65, 8.1, 8.0, 10.36, 11.04, 10.88, 8.76, 10.36, 10.25, 10.84, 10.56, 8.6, 8.38, 10.72, 8.76, 9.32, 9.89, 10.93, 10.21, 9.9, 11.09, 10.68, 8.6, 11.51, nan, 9.01, 12.15, 9.01, 10.95, 6.74, 10.93, 9.54, 8.51, 9.64, 10.81, 9.95, 7.62, 6.67, 10.09, 10.59, 8.84, 9.14, 10.56, 11.04, 10.56, 10.84, 9.54, 10.79, 8.19, 9.8, 9.01, 9.14, 10.27, 11.42, 11.05, 9.14, 10.51, 11.09, 8.46, 11.95, 10.5, 10.84, 11.04, 9.03, 11.51, 10.25, 9.89, 8.65, 10.09, 10.51, 10.83, 10.36, 11.04, 11.04, 8.38, 10.13, 11.7, 9.8, 10.12, 11.24, 9.11, 7.58, 8.74, 8.79, 6.89, 7.58, 7.28, 7.03, 8.88, 8.74, 8.74, 8.31, 8.16, 8.74, 8.88, ...]</td>
    </tr>
    <tr>
      <th>SERC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[19.0, 0.0, 21.0, 196.0, 840.0, 935.0, 1260.0, nan, 619.0, 150.0, 762.0, 0.0, 660.0, 1.0, 2700.0, 1.0, 4921.0, 95.0, 251.0, 4125.0, 2550.0, nan, 1200.0, 310.0, 2818.0, 5054.0, 136.0, 528.0, 150.0, 46.0, 1.0, 1920.0, nan, 32.0, 1.0, 1282.0, 390.0, nan, 3264.0, 1230.0, 803.0, 77.0, 30.0, 300.0, 1.0, 5.0, nan, 659.0, nan, 360.0, 120.0, 1200.0, 960.0, 120.0, 9230.0, 1440.0, 1579.0, 652.0, 108.0, 1020.0, 6492.0, 11280.0, 1440.0, 180.0, 1574.0, 45.0, 563.0, 388.0, 373.0, 4510.0, 290.0, 1950.0, 270.0, 1355.0, 1318.0, 2490.0, 1265.0, 195.0, 3120.0, 3388.0, 1025.0, 990.0, 240.0, 1485.0, 129.0, 0.0, 1528.0, 1890.0, 2551.0, 985.0, 405.0, 1698.0, 167.0, 1460.0, 182.0, 4113.0, nan, 885.0, 15.0, 42.0, ...]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[9.59, 9.47, 9.59, 8.91, 7.23, 9.18, 9.67, 9.7, 8.78, 9.13, 8.59, 9.47, 8.91, 9.93, 9.55, 9.93, 8.91, 9.02, 9.2, 9.93, 8.91, nan, 9.13, 9.03, 9.23, 8.91, 8.87, 9.65, 9.13, 8.91, 9.93, 9.13, 8.8, 9.16, 8.97, 8.31, 9.75, nan, 5.51, 6.24, 9.91, 8.56, 9.95, 8.81, 9.44, 9.61, 6.94, 9.28, nan, 7.61, 8.78, 7.52, 7.61, 9.43, 9.25, 7.62, 7.6, 6.42, 7.95, 5.72, 6.55, 6.19, 7.47, 7.46, 8.27, 8.94, 9.04, 8.71, 9.68, 9.59, 8.97, 9.17, 9.68, nan, 7.46, 6.79, 9.13, 8.93, 9.1, 6.7, 8.29, 7.99, 6.98, 9.31, 8.97, 8.51, 7.21, 7.28, 8.93, 9.32, 9.47, 9.31, nan, 8.29, 9.13, 8.93, nan, 8.29, 7.21, 8.68, ...]</td>
    </tr>
    <tr>
      <th>SPP</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[2340.0, 600.0, 181.0, 2159.0, 63.0, 1320.0, 394.0, 0.0, 12652.0, 15420.0, 300.0, 2775.0, 2160.0, 2100.0, 1440.0, 1755.0, 692.0, 557.0, 300.0, 3067.0, 430.0, 300.0, nan, 18804.0, 1690.0, 3.0, 30.0, 2806.0, 1226.0, 270.0, 2880.0, 8160.0, 3314.0, 110.0, 62.0, 159.0, 76.0, 1042.0, 110.0, 11880.0, 2245.0, 984.0, 7200.0, 1381.0, 148.0, 13972.0, nan, 796.0, nan, 2612.0, 3000.0, 431.0, 5310.0, 1732.0, 0.0, 3300.0, 280.0, 117.0, 2895.0, nan, 187.0, 1406.0, 348.0, 90.0, 913.0, nan, 14040.0]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[10.3, 8.85, 8.78, 6.23, 8.84, 8.55, 9.28, 10.7, 8.56, 5.42, 6.98, 8.13, 8.4, 7.32, 8.23, 7.38, 8.4, 7.56, 6.98, 6.86, 7.56, 6.98, 6.13, 8.39, 7.48, 6.77, 7.88, 7.11, 8.78, 8.17, 7.88, 5.14, 7.88, 7.7, 8.15, 8.47, 8.65, 7.01, 7.2, 4.7, 7.47, 8.52, 6.67, 8.52, 6.77, 6.94, 7.01, nan, 7.25, 8.52, 7.97, 8.52, 7.97, 8.43, 8.42, 7.25, 7.01, 7.2, 7.57, nan, 9.88, 9.93, 10.03, 9.93, 9.45, 10.48, 5.88]</td>
    </tr>
    <tr>
      <th>TRE</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[373.0, 1203.0, 868.0, 1455.0, 1195.0, 1559.0, 900.0, 2690.0, 5115.0, 5.0, 189.0, 2142.0, 360.0, 225.0, 480.0, 9486.0, 480.0, 3000.0, 300.0, 3020.0, nan, 1335.0, 197.0, 245.0, 3255.0, 12180.0, 1077.0, 186.0, 690.0, 27698.0, 402.0, 2420.0, 327.0, 1860.0, 220.0, 455.0, 318.0, 757.0, 847.0, 410.0, 215.0, 5.0, 570.0, 12124.0, 2655.0, 20160.0, 1440.0, 600.0, 1185.0, 1500.0, 0.0, 271.0, 1860.0, 1200.0, 6300.0, nan, 1620.0, 224.0, 70.0, 1697.0, 95.0, 2220.0, 7809.0, 1200.0, 121.0, 5595.0, 1.0, 557.0, 240.0, 3360.0, 685.0, 2280.0, 210.0, 167.0, 1920.0, 3569.0, 3300.0, 1560.0, 840.0, 240.0, 990.0, 6000.0, 17865.0, 1080.0, 7540.0, 1110.0, 27698.0, 130.0, 3040.0, 10140.0, 20160.0, 21540.0, 45.0, 1.0, 1200.0, 550.0, 900.0, 940.0, nan, 3050.0, ...]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[8.84, 8.94, 8.94, nan, 8.85, 8.75, 7.76, 8.38, 8.55, 9.2, 10.06, 9.57, 9.57, 8.9, 9.34, 8.38, 6.23, 8.75, 8.31, 8.38, 8.55, 9.62, 9.62, 10.06, 8.08, 10.13, 8.75, 7.26, 10.1, 11.33, 8.85, 8.28, 8.94, 8.38, 8.85, 8.28, 10.3, 7.62, 11.9, 8.56, 9.85, 7.74, 10.41, 12.22, nan, 8.67, 8.27, 9.85, 7.74, 9.85, 8.56, 10.22, 9.0, 9.28, 9.49, 9.2, 10.13, 10.27, 5.91, 8.94, 10.06, 8.71, 8.67, 7.52, 10.06, 10.52, 8.88, 8.59, 9.28, 11.33, 9.35, 8.79, 10.02, 7.9, 9.74, 11.92, 8.38, 10.02, 8.26, 9.85, 8.85, 9.62, 7.27, 8.63, 9.62, 8.51, 11.33, 10.06, 8.55, 7.9, 8.67, 11.33, 8.75, 9.2, 8.55, 8.84, 10.06, 9.63, 8.2, 7.74, ...]</td>
    </tr>
    <tr>
      <th>WECC</th>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[206.0, nan, 766.0, 39.0, 10.0, 885.0, 1240.0, 465.0, 0.0, 2460.0, 1183.0, 8880.0, 394.0, 219.0, 487.0, 19.0, 28.0, 0.0, 1.0, 5340.0, 8940.0, 467.0, 0.0, 1920.0, 0.0, 25.0, 420.0, 2040.0, 0.0, 1.0, 1423.0, 60.0, 1620.0, 3300.0, 385.0, 663.0, 123.0, 1276.0, 1919.0, nan, 440.0, 6690.0, nan, 0.0, nan, 717.0, 1204.0, 292.0, 313.0, 1.0, 5.0, 6276.0, 0.0, 74.0, 0.0, nan, 248.0, 1.0, 2700.0, 25.0, 126.0, 1.0, 255.0, 1207.0, 0.0, 0.0, 245.0, 476.0, nan, nan, nan, 1.0, 2639.0, 502.0, 548.0, 369.0, 6480.0, 15.0, 5.0, nan, 1.0, 0.0, 432.0, 21.0, 1697.0, 0.0, 2615.0, 9630.0, 3507.0, 2820.0, 314.0, 5855.0, 0.0, 0.0, 1.0, 22769.0, 70.0, 4285.0, 355.0, 0.0, ...]</td>
      <td style="max-width: 420px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">[8.87, 10.3, 10.41, 7.27, 8.7, 10.02, 7.09, 7.07, 7.09, 6.97, 7.29, 7.42, 6.69, 6.94, 6.94, 7.17, 7.08, 6.4, 6.89, 5.96, 6.61, 6.74, 7.07, 7.06, 7.08, 7.52, 7.79, 6.43, 7.08, nan, 6.74, 6.94, 7.07, 7.22, 6.69, 7.28, 6.7, 6.74, 7.74, 7.74, 6.65, 6.17, 7.74, 6.65, 7.42, 7.09, 6.55, 6.94, 7.57, 7.03, 7.08, 6.51, 6.89, 7.19, 7.06, 7.75, 6.49, 6.65, 6.86, 7.09, 6.89, 7.01, 6.88, 6.74, 6.4, 6.4, 6.74, 6.73, 7.74, 7.75, 7.52, 6.81, 6.74, 6.94, 6.8, 6.69, 5.89, 6.73, 7.03, 7.48, 7.07, 7.06, 7.07, 7.45, 6.74, 6.4, 6.94, 6.74, 6.17, 6.74, 6.65, 6.61, 6.4, 7.06, 7.29, 6.74, 6.73, 5.72, 6.69, 7.06, ...]</td>
    </tr>
  </tbody>
</table>
</div>

## Assessment of Missingness

### MNAR Analysis

I think the OUTAGE.DURATION column is MNAR. My reasoning for this is that missingnes might depend on the actual length of outages. An example of this is that companies with longer outages might be less likely to report them. While factor such as customers affected or customer type might account for some discrepancy, the dependence on the value itself suggests MNAR.

```python
# testing if missingness depends on other columns
def permutation_test_missingness(df, missing_col, test_col, N=10000):

   obs_stat = df.loc[df[missing_col] == 1, test_col].mean() - df.loc[df[missing_col] == 0, test_col].mean()
    
   p_values = []
   values = df[test_col].to_numpy() 
   mask = df[missing_col].to_numpy() == 1
    
   for _ in range(N) :
      shuffled = np.random.permutation(values)
      p_values.append(shuffled[mask].mean() - shuffled[~mask].mean())
    
   p_values = np.array(p_values)
   p_value = (np.sum(np.abs(p_values) >= np.abs(obs_stat)) + 1) / (N + 1)
    
   return obs_stat, p_value


# testing on only the numeric columns
numeric_cols = numeric_df.columns.tolist()

missing_res = {}

for numeric_col in numeric_cols :
   missing_res[numeric_col] = permutation_test_missingness(df, "OUTAGE.DURATION.MISSING", numeric_col)

print(missing_res)
```
#### Output
<pre>
{'YEAR': (-0.24941594243523468, 0.6363363663633637),
 'MONTH': (-0.5377468060394888, 9.999000099990002e-05),
 'OUTAGE.DURATION': (nan, 9.999000099990002e-05),
 'CUSTOMERS.AFFECTED': (-20599.732900432893, 9.999000099990002e-05),
 'DEMAND.LOSS.MW': (-235.83925373134326, 9.999000099990002e-05),
 'POPULATION': (1232916.8633538932, 0.42725727427257276),
 'POPPCT_URBAN': (0.5656543780954877, 0.7227277272272773),
 'POPDEN_URBAN': (85.61378375852837, 0.5548445155484452),
 'POPDEN_RURAL': (-12.103071929246838, 9.999000099990002e-05),
 'RES.PRICE': (-0.08158811475409955, 9.999000099990002e-05),
 'COM.PRICE': (0.03932035519125776, 9.999000099990002e-05),
 'IND.PRICE': (-0.10974385245901708, 9.999000099990002e-05),
 'TOTAL.PRICE': (-0.1156898907103816, 9.999000099990002e-05),
 'RES.SALES': (-64529.97916666698, 9.999000099990002e-05),
 'COM.SALES': (477396.71413934417, 9.999000099990002e-05),
 'IND.SALES': (272345.3487021858, 9.999000099990002e-05),
 'TOTAL.SALES': (738758.5939207654, 9.999000099990002e-05)}
</pre>

The missingness of OUTAGE.DURATION appears to be significantly associated with several observed variables, including CUSTOMERS.AFFECTED, MONTH, and multiple electricity price and sales measurements. However, it does not appear to depend on demographic variables such as POPULATION or POPPCT_URBAN.

These results suggest  missingness is likely Missing At Random (MAR), since whether outage duration is missing depends on other observed features in the dataset. The data therefore do not appear to be Missing Completely At Random (MCAR).

That said, we cannot rule out Missing Not At Random (MNAR), because it is still possible that the probability of missingness depends on the true (unobserved) outage duration values themselves — something that cannot be directly tested with the available data.

#### Customers Affected by OUTAGE.DURATION Missingness

<iframe
  src="assets/html/CA_OD_MISS.html"
  width="800"
  height="900"
  frameborder="0"
></iframe>