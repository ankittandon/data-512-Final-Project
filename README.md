## data-512-finalproject  
The materials in this repository describe the final project for a HCDE 511 taught at UW by Jonathan Morgan in the autumn quarter of 2018. More information about this class can be found here: https://wiki.communitydata.cc/Human_Centered_Data_Science_(Fall_2018) 

## Project Purpose
Answer the following 4 research questions:
1. Who is most likely to get the Flu
2. What are reasons people do not get the Flu vaccine
3. Where do people get the Flu vaccine
4. What are ways that Flu vaccination can be increased 
  
The project's purpose is to attempt to answer these questions using publically available datasets from the CDC and from the Atlantic Quarterly Survey on Flu Vaccination in Nova Scotia.

## About the Data  
The first dataset is from the CDC and the Public Health Service Act (section 308(d)) provides data collected by the National Center for Health Statistics (NCHS), Centers for Disease Control and Prevention (CDC), may be used only for the purpose of health statistical reporting and analysis. Users of this data are allowed to: 
1. Use the data in this dataset for statistical reporting and analysis only. \n
2. Make no use of the identity of any person or establishment discovered inadvertently and advise the Director, NCHS, of any such discovery.\n
3. Not link this dataset with individually identifiable data from other NCHS or non- NCHS datasets.\n

The second dataset is from the Nova Scotia Open Government and is licensed under the Nova Scotia Open Governement license. Users are allowed to "Copy, modify, publish, translate, adapt, distribute or otherwise use the Information in any medium, mode or format for any lawful purpose."
For more information please see - https://novascotia.ca/opendata/licence.asp
The questions asked in the survey were as follows:

Did you get the flu vaccination for the current flu season? / Are you planning to get the flu vaccination for the current season?

If yes, where did you get the vaccination? Was it at:

A doctors office?
A Pharmacy?
A Public Health Walk-In Clinic?
Your Workplace?
Another location?
A follow up question if yes, why did you choose that location?

If no, What was the main reason for not getting your flu shot this season?

For each question there are a different number of respondents with no way of correlating results across a particular respondant. There is major demographic information associated with each respondant. The demographic information is bucketed in the following ways:

Age:
18 to 34 years old
35 to 54 years old
55+ years old
Education:
Less than High School
Graduated High School
Some Post Secondary School
Graduated Post Secondary School
Gender:
Male
Female
Income:
Less than $50k
$50k to <$100k
$100k+
Region:
Cape Breton
Halifax
Rest of Mainland
There are a variable number of respondents across questions where the max number for a question is 800.

The schema of the dataset is as follows:

TABLE
RESPONSE
GROUP
GROUP WEIGHTED %
GROUP WEIGHTED #
WEIGHTED SAMPLE SIZE (#)
UNWEIGHTED SAMPLE SIZE (#)

## About this github repository
Atlantic_Quarterly_Autumn_2017_-_DHW__flu_shots.csv is a data file that contains the survey results data\
To Vaccinate Or Not To Vaccinate.pdf is a pdf of the final project presentation\
final_report.md is the markdown file generated from the R Markdown code\
final_report.html is the knit version of the RMD file\
flu infection distribution.png is a graph visualizing the age groups with significant flu infection rates\
flu proportion.png is a graph visualizing the proportion of population within age groups with the flu infection\