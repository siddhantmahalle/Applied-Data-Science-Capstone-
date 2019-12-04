# Introduction

Imagine visiting a new city for the first time. You want to visit all the top sites and the best restaurants there. But you have no one to show you around or to suggest these places. You can use numerous travel sites or forums on the internet, but all of those gives different ideas, suggestions and directions. You want to visit these places, but you want to be cautious of crime-riddled neighbourhoods and avoid such routes. There is no single site that tells you this. So, what's the solution?

## My idea

I want to combine the venue and location data from FourSquare along with open source crime data to provide the traveller with a list of attractions and restaurants along with a graphical representation of crime statistics in those areas.

## My Approach

My approach to the problem is as follows:

1. The traveller decides on a city location [in this case, Chicago].
2. The Foursquare website is scrapped for the top venues in the city
3. From this, a list of top venues is augmented with additional geographical data
4. Using this data the top nearby restaurants are selected.
5. The historical crime statistics within a predetermined distance of all venues is obtained.
5. A map is presented to the traveller showing the selected venues and crime statistics of the area.
6. The future probability of a crime happening near or around the selected top sites is also presented to the user.

