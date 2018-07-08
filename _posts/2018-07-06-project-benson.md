---
layout: post
title: Metis Project 1
---

# Introduction

I'm writing this post as an assignment for Metis Data Science Bootcamp; I'm part of the 11th cohort for Metis's San Francisco campus. The first week of bootcamp just wrapped up, and we started off with an introduction to lots of different tools, many of which I'd dabbled with before but hadn't used on any sort of regular basis, e.g. Jupyter notebooks, bash, git, etc. But the main purpose of Metis is to train participants on how to analyze and interpret data, and we started off with a project analyzing MTA turnstile data in order to recommend which stations would be the best to hand out leaflets, in order to maximize the number of people to sign up for an email list for an organization aimed at promoting women in technology.

## Project 1

### Analysis
Figuring out how to approach the problem took some time. I was in a group of 6, which meant that figuring out who was going to work on what took some discussion as well. I will say that one of the best parts about this first week at Metis was meeting other bootcamp students and hearing about their backgrounds and how they decided to attend Metis. This cohort is apparently particularly large, and so I still haven't met everybody, but I anticipate that we'll all get to know each other fairly well by the end of the program.

In any case, we decided to split up the problem into a few parts. Auste, Billy, and Xu analyzed the MTA data, doing exploratory data analysis and cleaning the data, and then eventually using the data to select the top 20 busiest stations (we defined 'busiest' as meaning the most exits) over the month of June from the past 3 years.

Alan and I decided to work with the Google Places API to create maps of points of interest around these subways stations, to see if we could further prioritize which stations to target; these points of interests served as a proxy for the target audience that we were trying to find. I ended up scraping a web articles for lists of tech companies in New York City, and then for each subway station we calculated a 'tech company proximity' score which was essentially the reciprocal sum of distances for each subway station to each tech company. We also used Google Places to query for the locations of all Starbucks within a 300 m radius of each station, and again assigned a score to each station based on the # of Starbucks around each station, and also how close these Starbucks were to the station. Alan also used 2010 census data to calculate the % of women in each community district, and assigned a 'gender score' to each station, with a higher score for stations in community districts with a higher percentage of women.

Chelan worked on figuring out how to visualize these locations on a map, and also how to generate color-coded 'heat' maps to indicate which stations had higher scores.

### Results
Overall, we ended up with a way to assign different scores to each NYC station, based on 4 different criteria: MTA exits, tech company proximity, Starbucks proximity, and # of woman living within the community district where each station was located. To calculate a final score, we ended up taking a weighted sum of each of these scores, with the highest weight assigned to MTA traffic.

The list of the top 10 stations that we got after scoring each of the top 20 stations and then sorting are listed below:

!["Top 10 MTA stations"](https://jl56923.github.io/public/project_1_recommendations.png)

### Reflections
Looking at that top 10 list of stations, it mostly makes sense; Times Square, 34th St/Herald Square, 59th St/Columbus Circle are all really busy stations, and so I would certainly expect them on the list. Atlantic Ave/Barclays Center and Flushing were a little surprising to me, although I have to admit I'm not as familiar with Brooklyn or Flushing as I am with Manhattan.

In the end, working on this project was an interesting way to get all of us started analyzing and interpreting data. Hopefully as we all become more comfortable using the tools, the work will become faster, although I'm certainly aware that there's always more to learn. I'm looking forward to seeing what the next couple months will bring.
