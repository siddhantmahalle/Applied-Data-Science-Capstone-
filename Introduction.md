# Introduction

Imagine going to a new city, you want to visit all the top sites and  the best restaurants there. But you have no one to show you around or to suggest these places. You can use numerous travel sites or forums on internet but all of those gives different ideas,suggestions and directions. You want to visit these places but you want to be causious of crime riddled neighbourhoods and advoid such routes. No single sites tells you this. So, whats the solution??

## My idea

I want to combine the venue and location data from FourSquare along with open source crime data to provide the traveller with a list of attractions and restaurants along with graphical representation of crime statistics in those areas.

## My Approach

My approach to the problem is as follows:

1. The travellers decides on a city location [in this case Chicago]
2. The ForeSquare website is scrapped for the top venues in the city
3. From this list of top venues the list is augmented with additional grographical data
4. Using this additional geographical data the top nearby restaurents are selects
5. The historical crime within a predetermined distance of all venues are obtained
5. A map is presented to the to the traveller showing the selected venues and crime statistics of the area.
6. The future probability of a crime happening near or around the selected top sites is also presented to the user.

