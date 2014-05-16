Working with ACS Data
========================================================
author: Alex Shum
date: May 2014

Census Bureau
========================================================
- Agency responsible for collecting demographic data.
- Officially formed in 1903 under the department of commerce.
- Primary mission is to conduct the decennial census.

 ![logo](Census_Bureau_seal.svg)

Census Data
========================================================
- Decennial census
- American community survey
- American housing survey
- Survey of construction
- National longitudinal survey
- Consumer Expenditure survey
- Surveys for other agencies: NSF, SSA, BLS and many other agencies.
  
Decennial Census
========================================================
- Mandated by Article I, Section 2 of the Constitution
- First census taken in 1790.
- Determines the number of seats in House of Representatives and number of Electoral College votes.
- Prior to 2010, the census included a "long form" containing additional demographic questions.
- 2010 Census removed the long form.  These questions now on American Community Survey.

Decennial Census
========================================================
- Short: Name, age, gender, race, marital status.
- Long: Place of birth, military service, salary.
- 2000 Census - $6.5 billion.  
- 2010 Census - $11 billion. 

Long form:
http://www.census.gov/dmd/www/pdf/d02p.pdf
Short form:
http://www.census.gov/dmd/www/pdf/d61a.pdf

American Community Survey
========================================================
- Replaces the census long form.
- Collects demographic variables including income, education, healthcare and many other variables.
- Unlike census, this survey is a yearly survey.
- Data sampled among US households.  Survey sent to 3 million addresses per year.
- 97% response rate.

American Community Survey
========================================================
 ![acs](acsform.png) 
 ![acs2](acsquestion.png)
 
<!--- http://www.census.gov/acs/www/Downloads/questionnaires/2014/Quest14.pdf -->

How can we access this data?
========================================================
- Various tools provided by the Census Bureau: factfinder, dataferret, quickfacts.
- http://factfinder2.census.gov/
- http://quickfacts.census.gov/
- http://dataferrett.census.gov/

How can we access this data?
========================================================
- The Census Bureau also provides the entire dataset for download.
- Files are quite large.
![ftp](ftp.png)

Online API
========================================================
- Can be accessed at: http://api.census.gov
- Request data as an HTTP GET request.
- The basic structure of the request:
http://api.census.gov/data/[YEAR]/[DATASET]?key=[KEY]&get=[VARIABLES]&for=[GEOGRAPHY]
- [YEAR]: year of dataset.
- [DATASET]: Which dataset to access.
- [KEY]: developer's key.
- [VARIABLES]: demographic variables.
- [GEOGRAPHY]: geographic area.

Online API - key & datasets
========================================================
- Developer's key available at: http://api.census.gov/data/key_signup.html
- 1990, 2000 and 2010 census.
- ACS datasets available in 5-year, 3-year and 1-year summary.
- ACS data range from 2006 to 2012.  ACS datasets not available for every year.
- Economic Time Series indicators.

<!--- http://www.census.gov/developers/ -->

Variables
========================================================
- http://api.census.gov/data/2012/acs5/variables.json
- Available variables posted in JSON format.

![var](var.png)

- A concept is a combination of factors from different questions on the ACS.
- A label is a combination of different levels of factors.
- A universe is the total number of people involved with a concept.

Geography
========================================================
- http://api.census.gov/data/2012/acs5/geography.json
- Available geographic entities posted in JSON format.
- Geographic entities correspond to different "summary levels".
- A "summary level" is a code for a combination of regions and used to represent the hierarchical nature of geography.
- Geographic regions: State, county, subdivision, tract, place, school district, zip code region, congressional district.
- Many combinations of geographic regions cannot be used together; valid combinations of regions will have a summary level code.

Geography
========================================================
010  <br />
020 <br />
030 <br />
040  <br />
050 <br />
060 <br />
140 <br />
860 <br />
970 <br />
***
United States  <br />
Region  <br />
Division  <br />
State  <br />
State-County  <br />
State-County-Subdivision  <br />
State-County-Tract  <br />
Zip Code Area  <br />
State-School District unified  <br />

Geography
========================================================
![plot of chunk unnamed-chunk-1](slides-figure/unnamed-chunk-1.png) 


Geography
========================================================
![plot of chunk unnamed-chunk-2](slides-figure/unnamed-chunk-2.png) 


Formatting
========================================================
Median income by gender and hours worked.

```
           male_total male_full male_other
Alabama         29556     45667      14669
Alaska          39792     60673      19015
Arizona         31794     46774      17777
Arkansas        26978     40919      14622
California      32630     52364      16553
Colorado        36651     52889      17561
```

total = overall median  <br />
full = full time  <br />
other = not full time  <br />
<font size="4"> http://api.census.gov/data/2012/acs5?key=[KEY]&get=B19326_001E,B19326_002E,B19326_003E,B19326_004E,B19326_005E,B19326_006E,B19326_007E,NAME&for=state:* </font>

Formatting
========================================================
- Each concept has its own data table.
- Each column is a label.
- Each row is a location based on specified geography.
- Data not in tidy format.  Each row should be an observation and each column a variable.
- Column headers provide categorical information. <br />
<font size="4"> (See: Hadley Wickham. "Tidy Data". In: Under review by the Journal of Statistical Software (2014). url:
http://vita.had.co.nz/papers/tidy-data.pdf.)  </font>

Formatting
========================================================

```
       state gender part.full income
1    Alabama   male     total  29556
2     Alaska   male     total  39792
3    Arizona   male     total  31794
4   Arkansas   male     total  26978
5 California   male     total  32630
6   Colorado   male     total  36651
```

<font size="4"> http://api.census.gov/data/2012/acs5?key=[KEY]&get=B19326_001E,B19326_002E,B19326_003E,B19326_004E,B19326_005E,B19326_006E,B19326_007E,NAME&for=state:* </font>

Taking a chance in the Classroom
========================================================
- Article by Morgan, Cetinkaya-Rundel, Stangl with classroom exercises based on ACS data.

```
  Sex Age Married Income HoursWk  Race
1   0  31       0  60.00      40 white
2   1  31       0   0.36      12 black
3   1  75       0   0.00      NA white
4   0  80       0   0.00      NA white
5   1  64       1   0.00      NA white
6   1  14       0     NA      NA white
```

- We explore some of their exercises using the full ACS dataset. <br/>
<font size = "4"> (See: Dalene Stangl, Mine Cetinkaya Rundel, and Kari Lock Morgan. "Taking a Chance in the Classroom:
The American Community Survey". In: CHANCE 26.1 (2013), pp. 42-46. doi: 10.1080/09332480.
2013.772392. url: http://www.tandfonline.com/doi/abs/10.1080/09332480.2013.772392.) </font>

Taking a chance in the Classroom
========================================================

```
  Sex Age Married Income HoursWk  Race
1   0  31       0  60.00      40 white
2   1  31       0   0.36      12 black
3   1  75       0   0.00      NA white
4   0  80       0   0.00      NA white
5   1  64       1   0.00      NA white
6   1  14       0     NA      NA white
```

- This dataset is a 1000 person subset of the 2010 public use microsample.
- Each row is an individual, columns are demographic variables unlike from online API.

Taking a chance in the Classroom
========================================================
First exercise: <br/>
In our sample of 1000 people, 861 have health inusrance and 139 do not.  Generate a confidence interval for the proportion of U.S. residents who do not have health insurance.

```
  HoursWk  Race USCitizen HealthInsurance
1      40 white         1               1
2      12 black         1               1
3      NA white         1               1
4      NA white         1               1
5      NA white         1               1
6      NA white         1               1
```

```
[1] 139
```


Taking a chance in the Classroom
========================================================
95% Confidence interval for this exercise: <br/>
<br/>
$$
\hat{p} \pm Z^* \sqrt{\frac{\hat{p} (1 - \hat{p})}{n}}
$$

```
  HoursWk  Race USCitizen HealthInsurance
1      40 white         1               1
2      12 black         1               1
3      NA white         1               1
4      NA white         1               1
5      NA white         1               1
6      NA white         1               1
```

```
[1] 0.1176 0.1604
```



From ACS data:
========================================================
Individual level data not available. We use nation-wide estimates.<br/>
<br/>
Most relevant table from ACS: B27001 Health Insurance Coverage Status by Sex by Age

```
  gender            age coverage     freq
1   Male  Under.6.years     With 11567822
2   Male  Under.6.years       No   800800
3   Male  6.to.17.years     With 23123651
4   Male  6.to.17.years       No  2242804
5   Male 18.to.24.years     With 10395228
6   Male 18.to.24.years       No  4608837
7   Male 25.to.34.years     With 13478715
8   Male 25.to.34.years       No  6191777
```


From ACS data:
========================================================

```
  gender            age coverage     freq
1   Male  Under.6.years     With 11567822
2   Male  Under.6.years       No   800800
3   Male  6.to.17.years     With 23123651
4   Male  6.to.17.years       No  2242804
5   Male 18.to.24.years     With 10395228
6   Male 18.to.24.years       No  4608837
```


Using this data from the ACS here is our estimate of proportion of people without health insurance.

```
[1] 0.1487
```


Standard Errors
========================================================
- Data from the ACS is an estimated count; proportions require additional calculations.  
- Margin of error (MOE) is available for estimated counts.
- For the standard error of a sum of estimates:
$$
SE(A + B) = \sqrt{SE(A)^2 + SE(B)^2}
$$
- For a confidence interval for proportions:
$$
SE(A/B) = 1/B \sqrt{SE(A)^2 - (A/B)^2 SE(B)^2}
$$
- These are approximations and do not take into account covariances.

Standard Errors
========================================================
- We can calculate the confidence interval for the proportion of U.S. residents who do not have health insurance from full ACS 5-year dataset.
- This is done by combining the two formulas on the previous page:

```
[1] 0.1483 0.1492
```


Compare with confidence interval from 1000 person subset:<br/>

```
[1] 0.1176 0.1604
```



Standard Errors
========================================================
- This CI is a much smaller interval in part due to the increase in sample size.
- CI from full ACS 5-year does not take into account covariances.
- Data is given as estimates not proportions; not much we can do about standard errors.

Other issues
========================================================
- It is not possible to combine tables.
- The only variables available need to be from an existing concept.
- Difficult to get compare numbers over different time periods.

Examples
========================================================
- The ACS 5-year dataset provides information at the census tract level.
- For New York City census tracts are geographically small due to density.
- We can look at majority race for each census tract.

Examples
========================================================
![plot of chunk unnamed-chunk-14](slides-figure/unnamed-chunk-14.png) 


Conclusion
========================================================
- Data from online API in difficult to use format.
- Possible to recreate some of the exercises from "Taking a chance in the Classroom".
- Data from online API not great for hypothesis tests or confidence intervals.
- Online API more useful for application developers.

Questions
========================================================
Questions?

