# Final Project Plan
Ankit Tandon

## Introduction
Each year when the Fall season begins, it's hard to not notice the ubiquitous encouragement to get a flu shot. Whether it is on social media, at work, on the radio, or at the grocery store there are signs everywhere telling us to get our flu shot. I often wonder about the effectiveness of such guerilla marketing and in this project I am interested in studying techniques that can be employed to increase population of individuals who receive a flu shot.

### The Economics of the Flu
In the 2018-2019 season the CDC estimates that between 163 to 168 million doses of flu vaccine were distributed in the United States <sup>[1](#myfootnote1)</sup>. This accounts for big business and generates billions of dollars in revenue each season for private Pharmaceutical firms. According to the World Health Organization, the influenza market is estimated to gross $3.8 billion in sales in 2018 with the the drug Fluzone (manufactured by Pharmaceutical company Sanofi Pasteur) topping the list of highest sold drugs. Fluzone generated $1.2 billion USD in sales in 2010 <sup>[2](#myfootnote2)</sup>. While the flu vaccine certainly generates considerable revenue for private pharma companies, the influenza disease has a huge impact on the US economy annually. Researchers from the CDC have estimated that "in 2003, the total economic burden of annual influenza epidemics using projected statistical life values amounted to $87.1 billion. The annual influenza epidemics result in 3.1 million hospitalized days, 31.4 million outpatient visits, and $10.4 billion in direct medical costs.<sup>[3](#myfootnote3)</sup>."

### The Effectiveness of the Flu Vaccine
There is some discussion on the effectiveness and perhaps the need for the influenza vaccine. The CDC conducts annual vaccination effectiveness trials to judge the VE (vaccine effectiveness) percentage of the influenza vaccine. The results of these trials show that in the 2017-2018 season, the influenza vaccine has a VE% score of 40 <sup>[4](#myfootnote4)</sup>. This implies that the vaccination reduced the risk of flu illness in the population by 40%. The vaccine does have some potential side effects such as headaches, fainting, muscle aches, and nausea as listed by the CDC <sup>[5](#myfootnote5)</sup>. That said, my goal of this project is not to discuss the effectiveness of the vaccination or the potential harms but to focus my attention on methods that can be used to increase the utilization of the vaccine.

### The Role of Corporations in Public Health
My motivation for this project is to understand if there is a role that a corporation can play in public health initiatives.
According to a study by the RAND Corporation, workplace wellness is a $6 billion industry in the United States. The study explains that "nearly half of employers with 50 or more employees offered a [workplace wellness] program." The ultimate ROI calcuations on workplace wellness programs is based on fees and costs of running the program minus the savings in medical care and absteeism of employees<sup>[6](#myfootnote6)</sup>. To make workplace wellness programs more effective, there needs to be an increase in the utilization of disease management programs and one way to do this is to increase the participation of employees in flu vaccination drives provided by companies. John Beshears, a professor from the Harvard Business School, has conducted an experiement where the design of a workplace flu shot drive increased vaccination rate by 4.2 percent by prompting employees to write down a specific date and time that they plan to receive the vaccination. Beshears also conducted an experiment where the proximity and chance of 'passing by' a flu vaccination clinic was increased. The study showed a 6.4% increase in the likelihood of getting vaccinated simply by increasing thel likelihood of employees to pass by the clinic location at their workplace <sup>[7](#myfootnote7)</sup>. My takeaway from this research is that current workplace wellness programs can become profitable for corporations if designed differently and can in turn help governments hit their public health initiative goals while helping companies reduce costs.

## Research Questions
Question 1: What are the demographics of people who obtain flu vaccine?

Question 2: Do people prefer receiving their vaccination in the workplace?

Question 3: What prevents people from receiving their vaccination in the workplace?

## Data
The data I will use for this project is licensed under the Nova Scotia Open Government License. The data summarizes the results of a survey conducted by the Nova Scotia government to judge the public opinion regarding "the annual flu shot (intent to get a flu shot, where and rational for location, reasons for not receiving flu shot).<sup>[8](#myfootnote8)</sup>"

The questions asked in the survey were as follows:
- Did you get the flu vaccination for the current flu season? / Are you planning to get the flu vaccination for the current season?
- If yes, where did you get the vaccination? Was it at:
	- A doctors office?
	- A Pharmacy?
	- A Public Health Walk-In Clinic?
	- Your Workplace?
	- Another location?
- A follow up question if yes, why did you choose that location? 

- If no, What was the main reason for not getting your flu shot this season? 

For each question there are a different number of respondents with no way of correlating results across a particular respondant. There is major demographic information associated with each respondant. The demographic information is bucketed in the following ways:
- Age:
	- 18 to 34 years old
	- 35 to 54 years old
	- 55+ years old
- Education:
	- Less than High School
	- Graduated High School
	- Some Post Secondary School
	- Graduated Post Secondary School
- Gender:
	- Male
	- Female
- Income:
	- Less than $50k
	- $50k to <$100k
	- $100k+
- Region:
	- Cape Breton
	- Halifax
	- Rest of Mainland

There are a variable number of respondents across questions where the max number for a question is 800.

The schema of the dataset is as follows:
- TABLE
- RESPONSE
- GROUP
- GROUP WEIGHTED % 
- GROUP WEIGHTED #
- WEIGHTED SAMPLE SIZE (#)
- UNWEIGHTED SAMPLE SIZE (#)

## Tools
I plan to use Python, R, Pandas, ggplot, and Microsoft Excel to conduct the analysis for this project. 

## Sources
- <a name="myfootnote1">1</a>: https://www.cdc.gov/flu/protect/keyfacts.htm
- <a name="myfootnote2">2</a>: http://www.who.int/influenza_vaccines_plan/resources/session_10_kaddar.pdf
- <a name="myfootnote3">3</a>: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.397.6523&rep=rep1&type=pdf
- <a name="myfootnote4">4</a>: https://www.cdc.gov/vaccines/acip/meetings/downloads/slides-2018-06/flu-02-Flannery-508.pdf
- <a name="myfootnote5">5</a>: https://www.cdc.gov/flu/protect/vaccine/general.htm
- <a name="myfootnote6">6</a>: https://data.novascotia.ca/Public-Opinion-Research/Atlantic-Quarterly-Autumn-2017-DHW-flu-shots-/dcj6-kjxr 
- <a name="myfootnote7">7</a>: https://www.rand.org/content/dam/rand/pubs/research_briefs/RB9700/RB9744/RAND_RB9744.pdf
- <a name="myfootnote8">8</a>: http://www.pnas.org/content/108/26/10415
- <a name="myfootnote9">9</a>: https://journals.lww.com/lww-medicalcare/Fulltext/2016/06000/Vaccination_Rates_are_Associated_With_Functional.5.aspx