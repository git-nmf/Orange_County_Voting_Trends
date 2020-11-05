## Data to be used to explore the trends, model interrelationships, and predict outcomes.

#### Data:

1. Census Data:  demographic data, income data
- ACS data 2011-2019
310	metropolitan statistical area/micropolitan statistical area	
312	metropolitan statistical area/micropolitan statistical area› state (or part)› principal city (or part)	
314	metropolitan statistical area/micropolitan statistical area› metropolitan division	
330	combined statistical area
400	urban area	
500	state› congressional district	
795	state› public use microdata area	
950	state› school district (elementary)	
960	state› school district (secondary)	
970	state› school district (unified)


2. Statewidedatabase.org:  voting data

3. Mapping ???

4. NewsAPI:  editorial data as a proxy for sentiment/NLP ???

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

#### Findings of Exploratory Data Analysis:

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
- nulls
- conflicting columns
- date mis-match
- geography mis-match ... may need to expand census tracts and voting districts to get to a roughly matching area
- need a framework of how macroecon and social factors interact to result in political outcomes ... I am using my own assumptions, not those of an expert, and will include any inherent biases of which I may not be aware
- I don't know the area and the local people, so there are in the trenches perceptions and cultural trends that I can't factor in.  on the other hand, my relative objectivity might be useful in this context



