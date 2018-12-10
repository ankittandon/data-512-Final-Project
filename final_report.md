This is a R markdown notebook for my final project for the class HCDE 511 taught at UW by Jonathan Morgan in the autumn quarter of 2018. More information about this class can be found here: https://wiki.communitydata.cc/Human_Centered_Data_Science_(Fall_2018) 

# Introduction

Every year in the US, the flu or influenza kills about 40,000 and hopitalizes some 470,000. Last year's influenze was one of the deadliest, resulting in a decade high 80,000 deaths according to the CDC - those are startling numbers. Yet, despite these startling figures, most Americans decide to skip the flu shot. Last season, the CDC estimates that only 37% of adults recieved the influenza vaccination.[1](#myfootnote1)

In the 2018-2019 season the CDC estimates that between 163 to 168 million doses of flu vaccine were distributed in the United States 1. This accounts for big business and generates billions of dollars in revenue each season for private Pharmaceutical firms. According to the World Health Organization, the influenza market is estimated to gross 3.8 billion in sales in 2018 with the the drug Fluzone (manufactured by Pharmaceutical company Sanofi Pasteur) topping the list of highest sold drugs. Fluzone generated 1.2 billion USD in sales in 2010 [2](#myfootnote2). While the flu vaccine certainly generates considerable revenue for private pharma companies, the influenza disease has a huge impact on the US economy annually. Researchers from the CDC have estimated that "in 2003, the total economic burden of annual influenza epidemics using projected statistical life values amounted to $87.1 billion."[3](#myfootnote3)

There is some discussion on the effectiveness and perhaps the need for the influenza vaccine. The CDC conducts annual vaccination effectiveness trials to judge the VE (vaccine effectiveness) percentage of the influenza vaccine. The results of these trials show that in the 2017-2018 season, the influenza vaccine has a VE% score of 40 4. This implies that the vaccination reduced the risk of flu illness in the population by 40% [4](#myfootnote4). The vaccine does have some potential side effects such as headaches, fainting, muscle aches, and nausea as listed by the CDC 5. That said, my goal of this project is not to discuss the effectiveness of the vaccination or the potential harms but to focus my attention on methods that can be used to increase the utilization of the vaccine[5](#myfootnote5).

Research in the field of influenza vaccination has direct impacts to real problems that governments and health care providers face. The unsolved research question in this area is - how can vaccination rates be increased. The real problem with the influenza vaccination rates is that governments, such as the Canadian Government, has set lofty goals for themselves to achieve 80% vaccination rates in their population under the age of 65[6](#myfootnote6). Yet, their current vaccination rate is at 40% which leaves tremendous scope for improvement. If one studies and devises a plan to increase vaccination rates that can be highly lucrative and beneficial to meeting the government's public health initiative.

# Background

What inspired me on this project was to study the public health initiative of flu vaccination and why people do or don't get the vaccination. 
As such, I have set out to answer 4 research questions - 
1. Who is most likely to get infected by the flu?
2. What are reasons that people get or don't get the vaccine?
3. Where do people get their vaccination?
4. What can be done to drive higher vaccination rates?

Question number 4 has been explored by John Beshears, a professor of behavioral economics at The Harvard Business School. He designed a study at an 1800 employee company in 2011. The study tried 2 things - it placed a flu shot clinic in the lobby of a workplace such that employees would be forced to pass by the clinic during the workweek. The result led to an increase in vaccination rates by 6% (which in a company of 1800) is almost 100 people! [7](#myfootnote7)
A second thing the study found to be effective was making employees write down a date and time that they would be administrered the flu shot. Implementing this intention prompt enhanced vaccination rates by 4.2 percent.[8](#myfootnote8)

# Methods
My analytical methods for this project are straightforward exploratory analysis. I have 2 data sources - the CDC published data sets and the quarterly Nova Scotia survey on influenza vaccination. 

I had some initial ideas to create a predictive model to understand associations between flu infection and vaccination rates however there isn't a single ecompassing data source that can be used to answer my research questions. In fact, there are some data integrity considerations that ought to be made when interpreting my results - this will be discussed in more detail in the discussion/implications section. The data integrity issues lie in the fact that the data sources used in this project will be from 2 different populations of individuals making an 'apples to apples' comparison difficult

I did not design any studies in this project but I do reference John Beshear's study to judge the increase of vaccination coverage at the workplace through the use of intention prompts and placing flu shot clinics in the lobby of the workplace. There are some ethical considerations on this study. First, the incessant encouragement of getting the flu shot might be determiental and stressful to those with allergies or other medical conditions that prevent them from getting the flu shot. It would be unethical to inundate such people with prompts and environments encouraging flu shots. Second, one should consider using this research to make broad-based blanket statements because the sample size of the study consists of only 1 1800 employee firm. The the company studies is in the healthcare industry so the cross application of the result to other industries is questionable.

# Findings
Question 1: Who is likely to get the flu?
The CDC publishes influenza related statistics. One issue with these data is that it is presented in a clunky, flash based web application that is tough to query. Some very nice developers including one by the name of Bob Rudis have created an R tool that makes this data querable and the package is MIT licensed. [9](#myfootnote9)

Using the cdcfluview R package, i'll first query the dataset which contains flu related illness counts by age group. The age groups should be split into 4 categories based on the pre-defined buckets.

```r
library(cdcfluview)
distribution <- age_group_distribution()
level_one <- distribution[ which(distribution$age_label=='0-4 yr'),]
level_two <- distribution[ which(distribution$age_label=='5-24 yr'),]
level_three <- distribution[which(distribution$age_label=='25-64 yr'),]
level_four <- distribution[which(distribution$age_label=='65+ yr'),]
```

Now that I have the number of illnesses reported according to the 4 buckets, I need to normalize the values based on the 2010 census data since the bucket sizes and unequal. To do this, i'll use the 2010 census data published on census.gov[11](#myfootnote11)
The numbers will be hardcoded into an agecount list and the proportion list in the dataframe will be the number of illnesses divided by the population for a given bucket.

```r
agecount <- c(19175798,80261468,124574328,34991753)
df <- data.frame(age=c("0-4 yr","5-24 yr","25-64 yr","65+ yr"), flucount = c(sum(level_one$count),sum(level_two$count),sum(level_three$count),sum(level_four$count)),agecount = agecount,proportion = c(sum(level_one$count)/agecount[1],sum(level_two$count)/agecount[2],sum(level_three$count)/agecount[3],sum(level_four$count)/agecount[4]))
```

Let's visualize the flu count by age group using GGPlot histogram plots. 

```r
library(ggplot2)
p2 <- ggplot(data=df, aes(x=age, y=agecount)) + geom_bar(stat="identity", fill="steelblue") + scale_x_discrete(limits=c("0-4 yr", "5-24 yr", "25-64 yr", "65+ yr")) + ggtitle("Age distribution of flu infected population as reported by the CDC")
p2
```

![](final_report_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

Now let's look at the proportion of population within the age group buckets that are infected with influenza.

```r
p3 <- ggplot(data=df, aes(x=age, y=proportion)) + geom_bar(stat="identity",fill="steelblue") + scale_x_discrete(limits=c("0-4 yr", "5-24 yr", "25-64 yr", "65+ yr")) + ggtitle("Age distribution of population as reported by the census")
p3
```

![](final_report_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

Switching over to the second dataset - I will be exploring survey data conducted in Nova Scotia of 800 respondents over the telephone. Below are the questions that the survey asked.[10](#myfootnote10)

```r
survey <- read.csv('Atlantic_Quarterly_Autumn_2017_-_DHW__flu_shots.csv',encoding="UTF-8")
unique(survey$X.U.FEFF.TABLE)
```

```
##  [1] TABLE AD1:   Did you get the flu vaccination for the current flu season?                                                                                                     
##  [2] TABLE AD2:   [ASK IF YES IN AD1] And where did you receive your flu vaccination? Was it at:                                                                                  
##  [3] TABLE AD3:   [DO NOT ASK IF YES IN AD1] Are you planning on getting the flu vaccination for the current flu season?                                                          
##  [4] TABLE AD1/AD3:   [FULL-BASE] Are you planning on getting the flu vaccination for the current flu season?                                                                     
##  [5] TABLE AD1/AD3:   [FULL-BASE] Did you get the flu vaccination for the current flu season? / Are you planning on getting the flu vaccination for the current flu season?       
##  [6] TABLE AD4:   [ASK IF YES IN AD3] And where are you planning on getting the flu vaccination? Is it at:                                                                        
##  [7] TABLE AD2/AD4:   [ASK IF YES IN AD1 OR AD3] And where did you receive your flu vaccination? Was it at: / And where are you planning on getting the flu vaccination? Is it at:
##  [8] TABLE AD5: FIRST MENTION [ASK IF A DOCTORS OFFICE IN AD2/AD4] Why did you choose that location?                                                                              
##  [9] TABLE AD5: TOTAL MENTIONS [ASK IF A DOCTORS OFFICE IN AD2/AD4] Why did you choose that location?  Any other reasons?                                                         
## [10] TABLE AD5: FIRST MENTION [ASK IF A PHARMACY IN AD2/AD4] Why did you choose that location?                                                                                    
## [11] TABLE AD5: TOTAL MENTIONS [ASK IF A PHARMACY IN AD2/AD4] Why did you choose that location?  Any other reasons?                                                               
## [12] TABLE AD5: TOTAL MENTIONS [ASK IF YOUR WORKPLACE IN AD2/AD4] Why did you choose that location?  Any other reasons?                                                           
## [13] TABLE AD5: FIRST MENTION [ASK IF ANOTHER LOCATION IN AD2/AD4] Why did you choose that location?                                                                              
## [14] TABLE AD5: FIRST MENTION [ASK IF A PUBLIC HEALTH WALK-IN CLINIC IN AD2/AD4] Why did you choose that location?                                                                
## [15] TABLE AD5: TOTAL MENTIONS [ASK IF A PUBLIC HEALTH WALK-IN CLINIC IN AD2/AD4] Why did you choose that location?  Any other reasons?                                           
## [16] TABLE AD5: FIRST MENTION [ASK IF YOUR WORKPLACE IN AD2/AD4] Why did you choose that location?                                                                                
## [17] TABLE AD5: TOTAL MENTIONS [ASK IF ANOTHER LOCATION IN AD2/AD4] Why did you choose that location?  Any other reasons?                                                         
## [18] TABLE AD5: FIRST MENTION [ASK IF CODES 01, 02, 03, 04 or 97 in AD2/ ASK IF CODES 01, 02, 03, 04 or 97 in AD4] Why did you choose that location?                              
## [19] TABLE AD5: TOTAL MENTIONS [ASK IF CODES 01, 02, 03, 04 or 97 in AD2/ ASK IF CODES 01, 02, 03, 04 or 97 in AD4] Why did you choose that location?  Any other reasons?         
## [20] TABLE AD6: FIRST MENTION [ASK IF NO IN AD3] What is the main reason you are not getting the flu shot this season?                                                            
## [21] TABLE AD6: TOTAL MENTIONS [ASK IF NO IN AD3] What is the main reason you are not getting the flu shot this season?  Any other reasons?                                       
## 21 Levels: TABLE AD1/AD3:   [FULL-BASE] Are you planning on getting the flu vaccination for the current flu season? ...
```

I am interested in what the reason was for respondents to NOT get the flu vaccine. As such, i've filtered the dataset to that question. Below are the top reasons that a respondent did not get the flu vaccine ranked by most frequent to least.

```r
responses <- survey[which(survey['X.U.FEFF.TABLE']=="TABLE AD6: FIRST MENTION [ASK IF NO IN AD3] What is the main reason you are not getting the flu shot this season?"),]
agg <- aggregate(responses$GROUP.WEIGHTED...1,by=list(Category=responses$RESPONSE),FUN=sum)
agg[order(-agg$x),]
```

```
##                                                        Category          x
## 3       Do not believe they help/do not protect against the flu 445.748609
## 8                 Dont need it/Dont get sick/Never have the flu 440.943491
## 11                                 Have never gotten a flu shot 282.411060
## 10     Flu shots make people sick/have made me sick in the past 186.766795
## 1                                                Another reason 178.342170
## 7                                           Dont know/No answer  84.407294
## 6   Dont believe in vaccines/Dont want chemicals injected in me  63.454947
## 9                                          Flu shots have risks  52.720442
## 2  Causes allergic reaction/Allergic to ingredients in vaccines  46.369584
## 12                       Schedule/too busy/not convenient times  44.765757
## 5                                           Do not like needles  37.059614
## 13          Transportation/Unable to get to a flu shot location  15.934977
## 4                           Do not know where to get a flu shot   6.292671
```

Let's break down the responses for the most popular reason to not get a flu shot by demographic. Interestingly enough, one of the highest percentage of respondents has greater than post secondary school education.

```r
agg <- aggregate(responses$GROUP.WEIGHTED...1,by=list(Category=responses$RESPONSE,Group=responses$GROUP),FUN=mean)
agg <- agg[which(agg$Category == "Do not believe they help/do not protect against the flu"),]
agg[order(-agg$x),]
```

```
##                                                    Category
## 159 Do not believe they help/do not protect against the flu
## 94  Do not believe they help/do not protect against the flu
## 55  Do not believe they help/do not protect against the flu
## 198 Do not believe they help/do not protect against the flu
## 16  Do not believe they help/do not protect against the flu
## 107 Do not believe they help/do not protect against the flu
## 185 Do not believe they help/do not protect against the flu
## 133 Do not believe they help/do not protect against the flu
## 146 Do not believe they help/do not protect against the flu
## 3   Do not believe they help/do not protect against the flu
## 120 Do not believe they help/do not protect against the flu
## 42  Do not believe they help/do not protect against the flu
## 29  Do not believe they help/do not protect against the flu
## 68  Do not believe they help/do not protect against the flu
## 81  Do not believe they help/do not protect against the flu
## 172 Do not believe they help/do not protect against the flu
##                        Group         x
## 159            NOVA SCOTIA % 75.130107
## 94                 GENDER: F 41.703552
## 55      EDUCATION: Grad P.S. 37.512953
## 198 REGION: Rest of mainland 36.607403
## 16               AGE: 35- 54 36.312119
## 107                GENDER: M 33.426555
## 185          REGION: Halifax 29.796973
## 133   HH INCOME: $50- <$100K 27.701687
## 146     HH INCOME: L.T. $50K 25.557293
## 3                AGE: 18- 34 23.278549
## 120        HH INCOME: $100K+ 17.952813
## 42      EDUCATION: Grad H.S. 15.772454
## 29                  AGE: 55+ 15.539439
## 68      EDUCATION: L.T. H.S. 10.467725
## 81      EDUCATION: Some P.S. 10.263257
## 172      REGION: Cape Breton  8.725731
```

Shown below is the responses to the question "Where did you receive your flu vaccination?" sorted by magnitude of respondents to the question. The top 2 responses are expected as the doctor's office and pharmacy are both health facilities where people get vaccinated. What sticks out is the 3rd response which is the workplace which is unlike the rest of the responses in that it doesn't have anything to do explicitly do with providing health care procedures.

```r
responses <- survey[which(survey['X.U.FEFF.TABLE']=='TABLE AD2/AD4:   [ASK IF YES IN AD1 OR AD3] And where did you receive your flu vaccination? Was it at: / And where are you planning on getting the flu vaccination? Is it at:'),]
agg <- aggregate(responses$GROUP.WEIGHTED...1,by=list(Category=responses$RESPONSE),FUN=sum)
agg[order(-agg$x),]
```

```
##                         Category          x
## 1               A doctors office 1288.70935
## 2                     A pharmacy  948.16950
## 6                 Your workplace  223.43336
## 3 A public health walk-in clinic  136.67770
## 4               Another location  106.52646
## 5            Dont know/No answer   34.99246
```

Below are the unique responses to the question of why one chooses to get vaccinated at the workplace. Interesting to see the possible answers suggested to the respondents in the survey.

```r
responses <- survey[which(survey['X.U.FEFF.TABLE']=="TABLE AD5: FIRST MENTION [ASK IF 'YOUR WORKPLACE' IN AD2/AD4] Why did you choose that location?"),]
unique(responses$RESPONSE)
```

```
## factor(0)
## 35 Levels: A doctors office A pharmacy ... Your workplace
```

# Discussion/Implications
There are several limitations of the study both in the individual datasets and in the study overall.
One limitation of the CDC data is that the dataset is sourced from a select network of 3,500 enrolled health care providers across the 50 states. The issue with this approach is that the health care providers that do not enroll to share their data with the CDC for this purpose and who see patients with influenza or influenza related illnesses would not have their data counted in this dataset. Another limitation with the CDC data is that it only provides one piece of demographic information which is age. Furthermore, the age data is placed in pre-defined buckets which have varying sizes.

The survey data has limitations as well. Namely, that it could be influenced by survey bias such as response bias or underresponse bias. Response bias is the tendency of respondents to respond to surveys with innacurate information. Underresponse bias has to do with the population of respondents. The issue would lie in the underrepresentation of any particular demographic that would make comparing the surveyed population with the whole population. All the documentation says is that the respondents were selected and telephoned. No further details are provided on the coverage and selection criteria of the respondents.

Finally, there is a limitation in comparing the CDC dataset with the survey data in that the CDC data is around population in the US whereas the survey data is stictly of a province in Canada. It's hard to compare these 2 datasets and draw conclusions across the board.

# Conclusion
To restate my research questions with their respones - 
q1: Who is most likely to get the flu?
The most number of cases of influenza come from the 25 to 64 years age group but the highest proportion of people who are likely to contract the flu come from the 0 to 4 year age group.
q2: What are reasons that people get or don't get the vaccine?
The main reason that people don't get the flu is that they don't believe in the effectiveness of the flu, which the CDC reports at 40-60% in recent years as stated earlier.
q3: Where do people get their vaccination?
People get their vaccination mostly from the pharmacy or doctor's office but a large proportion also get their vaccination from their workplace.
4. What can be done to drive higher vaccination rates? 
John Beshear suggests a few options to increase the vaccination rates by making flu shot drives more effective in the workplace. Another way to increase vaccination rates would be to introduce vaccinations to parts of the demographic that are traditionally underrepresented in terms of flu vaccination.

This research should inform your understanding of human centered data science as it provides a scientific approach to testing a hypothesis with data but also carefully considering the data sources for possible biases. Recognizing the limitations of the overall analysis as well as the individual data sets is crucial to human centered data science. Finally, this notebook serves as a template to structure a data science project to be replicated by others.

# References
- 1 Why the CDC Estimates Burden https://www.cdc.gov/flu/about/burden/why-cdc-estimates.htm 
- 2 Global Vaccine Market Futures and Trends http://www.who.int/influenza_vaccines_plan/resources/session_10_kaddar.pdf
- 3 The annual impact of seasonal influenza in the US: Measuring disease burden and costs, Molinari et. al. http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.397.6523&rep=rep1&type=pdf
- 4 Preliminary Estimates of 2017–18 Seasonal Influenza Vaccine Effectiveness against Laboratory-Confirmed Influenza from the US Flu VE and HAIVEN Networks https://www.cdc.gov/vaccines/acip/meetings/downloads/slides-2018-06/flu-02-Flannery-508.pdf
- 5 Flu Vaccine Safety Information https://www.cdc.gov/flu/protect/vaccine/general.htm
- 6 Health at a glance - Flu Vaccination Rates in Canada https://www150.statcan.gc.ca/n1/pub/82-624-x/2015001/article/14218-eng.htm 
- 7 "Vaccination Rates are Associated With Functional Proximity But Not Base Proximity of Vaccination Clinics” By Beshears, John PhD; Choi, James J. PhD et. al. Medical Care: June 2016 - Volume 54 - Issue 6 - p 578–583 https://journals.lww.com/lww-medicalcare/toc/2016/06000
- 8 “Using implementation intentions prompts to enhance influenza vaccination rates” By Katherine L. Milkman, John Beshears, et. al. PNAS June 28, 2011 108 (26) 10415 10420; https://doi.org/10.1073/pnas.1103170108 
- 9 R package to Retrieve U.S. Flu Season Data from the CDC FluView Portal (WHO & ILINet) https://github.com/hrbrmstr/cdcfluview 
- 10 Atlantic Quarterly Autumn 2017 - DHW (flu shots) Survey results https://data.novascotia.ca/Public-Opinion-Research/Atlantic-Quarterly-Autumn-2017-DHW-flu-shots-/dcj6-kjxr 
- 11 https://www.census.gov/prod/cen2010/briefs/c2010br-03.pdf