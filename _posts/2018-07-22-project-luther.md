---
layout: post
title: Metis Project 2
---

Summary: 1-3 page PDF summarizing your project scope, results, and any areas that you tried that didn't work out. Throughout this document it should also cover your project design, data, algorithm and tools.

# Introduction
For the second project at the Metis, the assignment was to use web-scraping with BeautifulSoup and Selenium in order to get data to build a multiple linear regression to make a quantitative prediction, regarding any topic of our choice. The example topic in the project assignment was predicting the gross of a movie based on different predictors, e.g. movie budget, which actors or directors were involved, etc.

I thought than an interesting topic to look into would be the opioid crisis; I think that the opioid epidemic is going to turn out to be the defining public health crisis of this generation, the way that AIDS and tobacco were for previous generations. I had a suspicion that a decent amount of the variance in which areas of the country have been most affected by the crisis could probably be explained by demographic or economic factors, but I was actually more curious about whether or not other predictors which were more modifiable would turn out to be significant. For example, the common narrative is that the opioid crisis started when physicians started prescribing opioid painkillers much more liberally in the 1990s, in part due to pharmaceutical companies reassuring physicians that these painkillers had a low incidence of addiction and few side effects, neither of which was true. But was opioid prescribing rate still a main driver of opioid overdose deaths? Or could it be that the volume of illegal opioids e.g. heroin, fentanyl, etc. were a stronger predictor?

## Project 2

### Design
The goal of the project was to predict a quantitative target variable using a multiple linear regression model. The design of the project was fairly straightforward: identify an appropriate target variable, then subsequently appropriate independent variables/predictors as well. Then, use these variables to build a multiple linear regression, and perform feature selection in order to see which predictors were the most important. Finally, test the model on a holdout test data set to see how well the model performed.

### Data
After exploring the CDC's description of their public databases, I decided to use the CDC WONDER database to scrape my target variable, which was the crude mortality rate due to drug overdose per county in 2016. A few comments on the decision to use this as a target variable: I initially thought about predicting mortality rate per state, but that would only give me 50 records. The CDC MCD (multiple causes of death) database actually does allow you to query for deaths specifically due to opioid overdose (and you can be even more specific, e.g. querying for the # of deaths due to heroin vs opioid analgesics vs other types of opioids), but the numbers became so small for individual categories that it was easier to get actual numbers for overall mortality rate due to drug overdose, without specifying what type of drug. This is because when the number of total deaths per county is between 10-20, the CDC will give you the # of deaths but won't calculate a crude or age-adjusted mortality rate, because they state that this small number results in 'unreliable' statistics. If the number of total deaths is between 0-9, then they won't give a number at all and will instead state that the result is 'suppressed', because with a small number of deaths in a small county, individual patients could potentially be identified.

Therefore, it was easiest to get data for crude mortality rate per county due to drug overdose, and the most recent dataset available was 2016. Statistically speaking, it would have been more accurate to compare age-adjusted mortality rates, however the CDC did not provide age-adjusted mortality rates for any counties where it gave a 'Unreliable' result (total deaths between 10-20), and without the specific breakdown of how many of these deaths were in each age bracket, I couldn't calculate the age-adjusted mortality rate directly. It does look like there are ways to indirectly calculate the age-adjusted mortality rate, but I decided to go ahead and use the crude mortality rate and then to use median age per county as a predictor as hacky way to sort of account for this.

For my independent variables, broadly speaking they fell into 4 categories:

Demographic
* % Caucasian
* % High school graduate or more (meaning the percent of people who at least graduated high school)
* Median age

Economic
* Median household income
* % Poverty
* % Unemployment

Medical
* Age of PDMP (prescription drug monitoring program) in the state
* Opioid prescribing rate per 100 people

Geographic
* US Census regional division

The demographic and economic data were all obtained using the US Census API. It's definitely a bit of a learning curve to figure out which US Census dataset to query, and then after that how to figure out how to structure a query. The US Census offers so much information that it looks like it's possible to get extremely granular query for the exact, specific records that you want, but the downside is that figuring out how to pull even simple data out is pretty difficult at first! Anyways, what I realized after looking at the pairplot of my predictors is that the economic data that I got has relatively high correlation with each other, e.g. % poverty and % unemployment, although they aren't measuring exactly the same thing, they clearly do correlate with each other. I thought that this might be a big problem in causing collinearity, but in retrospect I think that it was actually okay to have all these variables - when I get to the results section, I'll discuss that I think that engineering a variable that combines economic information might be even more useful for building a better model

The opioid prescribing rate per 100 people was pulled from the CDC, which provides [tables](https://data.cdc.gov/NCHS/NCHS-Drug-Poisoning-Mortality-by-County-United-Sta/p56q-jrxg) with the annual opioid prescribing rate per 100 people per county for more than the past decade. Some of the numbers were pretty eye-popping; in Norton County, VA, there were 563 opioid prescriptions per 100 people in 2014. That's right, more than 5 opioid prescriptions per person for that county!

A prescription drug monitoring program is 

### Algorithm

### Tools

## Results

## Conclusions

# Reflections
