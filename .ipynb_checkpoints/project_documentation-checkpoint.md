## Problem Statement

## Using voting results and voter-registration and demographics from Orange County in 2018 general election, this study will create a classification model that will predict vote for Congress based on key demographic inputs. 

# Executive Summary:  Shifts in Political Sentiment in Orange County, CA

The state of California is known as a solidly Democratic state.  However, it wasn't always that way.  Recall, this is the state that gave us notable Republican presidents Richard Nixon and Ronald Reagan, not to mention the Republican "Governator", Arnold Schwatzeneggar.

Orange County, south of Los Angeles, is a historically a solid Republican county.  However, in 2018, the county elected a slate of Democrats to represent them in Congress.  

<a id = problem> </a>
Problem Statement:

This study examines the connection between demographic and economic factors and voting results in Orange County in 2018, seeking to identify predictive factors in election outcomes.   

We will map these factors onto a street map of Orange County to help individual voters understand the magntitude of the changes happening in on their block, in their community, and in the surrounding areas.  Our intent is to make politics more accessible to the individual, and less "just something that's discussed on TV".

This creates a framework that could be applied to other counties in California, as well as other states.  


#### Data:
1. Census Data:  economic data, shape files for mapping
2. Statewidedatabase.org:  voting data, conversion file between voting precinct and census-tract

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


#### Cleaning and Exploratory Data Analysis:

1. Find trends using Pandas/MatPlotLib/Seaborn & Tableau for past 10-20 years for
- Avg HH income
- Avg people/household
- Race
- Sexuality
- Both partners work outside the home
- Education
- Employment industry
- Voting history for national offices
- Voting history for state/local offices

2. Align geographies - this will be difficult
- Understand geographic outlines of MSA vs. voting districts
- Decide if/how to group voting districts into meta-districts

3. If any above factors are constant, note that in write up and do not include on the Map Viz

4. IWIK - I Wish I Knew:
- political campaign spend
- significant legislation:  school testing, abortion, police brutality, ICE raids, taxes (esp. housing)
- home prices (UC Irvine?)
- significant local events:  fires, school shootings, professional sports, 
- unemployment rate
- population moving out ... and to where?
- population moving in ... and from where?


#### Data Sources & Data Dictionary:
TBD

#### Findings of Exploratory Data Analysis:
TBD

#### Map Viz (on Tableau):
- Draw meta-districts on choropleth map
- Color code meta-districts with different factors
- Generate sliders to pick which factors visualize on map
??? 

#### Modeling Extravaganza:
1. First pass:  Logistic Regression on Census vs. Voting data to find strong features, get a rough predictive classification model. Akin to an "EDA" model ... gives me the lay of the land.  Also run RandomForest to gauge feature importance vs. voting.
2. Test LogReg vs. MultinomialNB and RandomForest and another model TBD.  Then tune.
>> Model measured on ROC AUC curve.
- Should I try GradientBoosting if classes are v. unbalanced?  
- Should I try Neural Network?
3. DBScan to find clusters within Census data (xval with KMeans) - overlay on map - for EDA mostly
4. PCA between Census Data and Voting Data to understand best features
5. Perform Random Forest on PCA features to quantify importance
6. Refined LogReg predictor model to be able to get to "as X increases, chances of vote going Dem increase/decrease by Y times"


### Risks and Assumptions of these data
- overwhelming number of variables from Census data ... will require extra time to study which variables to pull down, and ultimately which values to involve in analysis/modeling
- data format from statewidedatabase.org:  similarly, will require time to study variable names to understand which columns to prioritize.  
- will need time to assemble datasets for analysis.  data collecting and organization.  will start with 2019 first.
- nulls
- conflicting columns
- date mis-match
- geography mis-match ... may need to expand census tracts and voting districts to get to a roughly matching area
- need a framework of how macroecon and social factors interact to result in political outcomes ... I am using my own assumptions, not those of an expert, and will include any inherent biases of which I may not be aware
- I don't know the area and the local people, so there are in the trenches perceptions and cultural trends that I can't factor in.  on the other hand, my relative objectivity might be useful in this context


### Game Plan

Oct 16-21
- orientation to Census Data video, use API to pull Orange County 2019 Community Survey, Prioritize max 50 columns
- orientation to Statewidedatabase.org, pulldown 2019 precint voting data for Orange County, Prioritize max 50 columns
- understand geography boundaries from each dataset, decide how to align the two, which impacts how to aggregate data later on
- preliminary EDA:  data dictionary, describe data, find & convert any problem data, understand if many nulls

Oct 22-27
- pull down additional years of data (9 years x 2 data sources)
- organize, clean, EDA

Oct 28- Nov 3
- modelling for feature selection and feature importance & predictions
- construct framework for what dimensions to receive input for making predictions
- learn choropleth mapping, Tableau for viz

Nov 3-9
- mapping viz in choropleth
- flask webpage:  simple design of page flow and UX input/output, deploy

Nov 10-17
- write up and presentation


