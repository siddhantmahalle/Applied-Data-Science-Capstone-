# Data

This data section is divided in two parts:
1. Venues and Location data obtained from FourSquare
2. Open source Chicago crime data 

## Data description

### Part 1

This include following steps:
1. Query the FourSqaure website for the top sites in Chicago
2. Use the FourSquare API to get supplemental geographical data about the top sites
3. Use the FourSquare API to get top restaurent recommendations closest to each of the top site

Although FourSquare provides a comprehensive API, one of the things that API does not easily support is a mechanism to directly extract the top N sites / venues in a given city. This data, however, is easily available directly from the FourSquare Website. To do this simply go to www.foursquare.com, enter the city of your choise and select Top Picks from I'm Looking For selection field.

Using BeautifulSoup and Requests the results of the Top Pick for Chicago can retrieved. From this HTML the following data can be extracted:
* Venue Name
* Venue Score
* Venue Category
* Venue HREF
* Venue ID [Extracted from the HREF]

Here is a screenshot of extracted data:

![Extracted data](/Images/Data_refrence.png)

### Part 2
Use open source Chicago Crime data to provide the user with additional crime data