## Problem Statement

Using voting results and voter-registration and demographics from Orange County in 2018 general election, this study will create a classification model that will predict vote for Congress based on key demographic inputs. 

## Executive Summary:  Shifts in Political Sentiment in Orange County, CA

The state of California is known as a solidly Democratic state.  However, it wasn't always that way.  Recall, this is the state that gave us notable Republican presidents Richard Nixon and Ronald Reagan, not to mention the Republican "Governator", Arnold Schwatzeneggar.

Orange County, south of Los Angeles, is a historically a solid Republican county.  However, in 2018, the county elected a slate of Democrats to represent them in Congress.  

<a id = problem> </a>
Problem Statement:

This study examines the connection between demographic and economic factors and voting results in Orange County in 2018, seeking to identify predictive factors in election outcomes.   

We will map these factors onto a street map of Orange County to help individual voters understand the magntitude of the changes happening in on their block, in their community, and in the surrounding areas.  Our intent is to make politics more accessible to the individual, and less "just something that's discussed on TV".

This creates a framework that could be applied to other counties in California, as well as other states.  


## Data:
1. Census Data:  economic data
2. Statewidedatabase.org:  voting data, conversion file between voting precinct and census-tract, shape files for mapping

**Census Economic Data from table DP03 for 2018 from American Community Survey 5-Year Estimate**
| Item | Description |
| --- | --- |
| tract | census tract |
| employed | Estimate EMPLOYMENT STATUS Population 16 years and over In labor force - Civilian labor force Employed |
| unemployed | Estimate EMPLOYMENT STATUS Population 16 years and over In labor force - Civilian labor force Unemployed | empl_military | Estimate EMPLOYMENT STATUS Population 16 years and over In labor force - Armed Forces |
| not_inlaborforce | Estimate EMPLOYMENT STATUS Population 16 years and over Not in labor force |
| working_women | Estimate EMPLOYMENT STATUS Females 16 years and over In labor force Civilian labor force Employed |
| parents_work_under6 | Estimate EMPLOYMENT STATUS Own children of the householder under 6 years All parents in family in labor force |
| parents_work_0617 | Estimate EMPLOYMENT STATUS Own children of the householder 6 to 17 years All parents in family in labor force |
| occ_mgmt_sci_art | Estimate OCCUPATION Civilian employed population 16 years and over Management, business, science, and arts occupations |
| occ_service_sector | Estimate OCCUPATION Civilian employed population 16 years and over Service occupations |
| occ_sales_gen_office | Estimate OCCUPATION Civilian employed population 16 years and over Sales and office occupations |
| occ_constr_maintc | Estimate OCCUPATION Civilian employed population 16 years and over Natural resources, construction, and maintenance occupations |
| occ_manuf_transpo | Estimate OCCUPATION Civilian employed population 16 years and over Production, transportation, and material moving occupations |
| hh_med_income | Estimate INCOME AND BENEFITS (IN 2018 INFLATION-ADJUSTED DOLLARS) Total households Median household income (dollars) |
| hlthins_priv | Estimate HEALTH INSURANCE COVERAGE Civilian noninstitutionalized population With health insurance coverage With private health insurance |
| hlthins_public | Estimate HEALTH INSURANCE COVERAGE Civilian noninstitutionalized population With health insurance coverage With public coverage |
| hlthins_none | Estimate HEALTH INSURANCE COVERAGE Civilian noninstitutionalized population No health insurance coverage |
| _ wtd | temporary suffix to signify census tract data weighted by the percent of the precint that it represents |

**Voting Data**
| Item | Description |
| --- | --- |
| county | county |
| srprec | voting precinct |
| cddist | congressional district |
| TOTREG | total registered voters by precinct|
| TOTVOTE | total voted within precinct |
| CNGDEM01 | votes for congressional representative - democrat |
| CNGREP01  | votes for congressional representative - republican |
| dem | registered democrats |
| rep | registered republicans |
| dcl | registered voters - no party affiliation| 
| male | male voters |
| female | femail voters |
| hispdem | hispanic voters - registered democrat | 
| hisprep | hispanic voters - registered repubican |
| hispdcl | hispanic voters - no party affiliation|
| hispoth | hispanic voters - registered for other parties 

**Converter File**
| Item | Description |
| --- | --- |
| srprec | voting precint |
| tract | census tract |  
| block | census block |
| blkreg | # registered voters in the block for the given precinct |
| srtotreg | # registered voters in the precinct |
| pctsrprec | % of precinct represented by the block |
| blktotreg | # registered voters in the block |
| pctblk | % of block voters represented by the precinct |
| pctsrprec_tract | % of precinct represented by the tract (calculated via aggregation) |


## Cleaning and Exploratory Data Analysis (EDA):

Several cleaning steps were performed to prepare data for modeling:
1. Download Census data, and header names.  Add header names to data file, in place of data codes.
2. Download voter registration data and vote results data.  Merge data frames on 'srprec' (precinct).
3. Download conversion file for precinct-to-tract conversion.  Aggregate to tract-level.
4. Merge Census data onto conversion file on 'tract' to create `combo` dataframe.
5. Calculate weighted Census data:  multiply each census column by 'pctsrprec_tract'

EDA shed light on the fact that Orange County contains part of 7 congressional districts.  However only 4 districts are majority located in Orange County (39, 45, 46, 48).  Comparing 2012 adn 2018 results shows that all 4 of the major districts voted for Democrat Congressional representatives in 2018, vs. only one major district in 2012.  

Surprisingly, household median income did not appear in the top 5 drivers.  Mapping household income per precinct shows that the majority of precincts earn between #50-#150k per year, with few pockets of poverty.  This may explain why it did not feature prominently as a driver of voting preference.


## Mapping:
Shapefiles for voting precints were downloaded from Statewidedatabase.org and loaded into Tableau Public.  Joined to that information was 'hh_med_inc' data for the precinct to generate a geo-heatmap of income levels across Orange County. 
https://public.tableau.com/profile/neva7752#!/vizhome/OCHHMedianIncomebyPrecinct/Sheet1?publish=yes


## Modeling:

1. First pass:  A quick first pass of a logistic regression was created on a small set of data.  The `y` dataset was defined as voting for the Democrat Congress candidate (1 = Dem, 0 = Rep).  Classweights were 60% Dem and 40% Rep, while not completely evenly balanced, there were plenty of observations available for the minority class to perform modeling.  
2. Extended modeling:  Using an extended dataset, more detailed modeling was performed.  Logistic regression with no regularization delivered an accuracy score of 85.3%.  The model results did not improve by adding in polynomial features and then reducing features with Select K Best.  Gradient Boost regression delivered almost identical accuracy, 85.0%

3. The results of Logistic Regression in #2 also revealed feature importances, with health insurance featuring prominently in the top 5 drivers of vote results in 2018.  


## Conclusions:

This project provides a blueprint for adding additional data from the Census and converting it to preceinct-level data for analysis.  It is also a blueprint for creating similar datasets for additional years (e.g., 2012, 2014, 2016) for trend comparison.

Future work should include adding additional Census data (race data, in particular).  And then to conduct additional feature selection with correlation analysis between features, and then PCA for feature engineering/elimination to improve model results.
