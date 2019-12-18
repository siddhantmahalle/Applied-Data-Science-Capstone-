# Data

This data section is divided in two parts:
1. Venues and Location data obtained from FourSquare
2. Open source Chicago crime data 

## Data description

### Part 1 : FourSquare Data

This include following steps:
1. Query the FourSqaure website for the top sites in Chicago
2. Use the FourSquare API to get supplemental geographical data about the top sites
3. Use the FourSquare API to get top restaurent recommendations closest to each of the top site

#### Top Sites from FourSquare Website
Although FourSquare provides a comprehensive API, one of the things that API does not easily support is a mechanism to directly extract the top N sites / venues in a given city. This data, however, is easily available directly from the FourSquare Website. To do this simply go to www.foursquare.com, enter the city of your choise and select Top Picks from I'm Looking For selection field.

Using BeautifulSoup and Requests the results of the Top Pick for Chicago can retrieved. From this HTML the following data can be extracted:
* Venue Name
* Venue Score
* Venue Category
* Venue HREF
* Venue ID [Extracted from the HREF]

Here is a screenshot of extracted data:

![Extracted data](/Images/Data_refrence.png)

#### Supplemental Geographical Data

Using the id field extracted from the HTML it is then possible to get further supplemental geographical details about each of the top sites from FourSquare using the following sample API call:

```python
# Get the properly formatted address and the latitude and longitude
url = 'https://api.foursquare.com/v2/venues/{}?client_id={}&client_secret={}&v={}'.format(
    venue_id, 
    cfg['client_id'],
    cfg['client_secret'],
    cfg['version'])
    
result = requests.get(url).json()
result['response']['venue']['location']
```

The requests returns a JSON object which can then be queried for the details required. The last line in the sample code above returns the following sample JSON:

```json
{  
   "city":"Chicago",
   "lng":-87.62323915831546,
   "crossStreet":"btwn Columbus Dr & Michigan Ave",
   "neighborhood":"The Loop",
   "postalCode":"60601",
   "cc":"US",
   "formattedAddress":[  
      "201 E Randolph St (btwn Columbus Dr & Michigan Ave)",
      "Chicago, IL 60601",
      "United States"
   ],
   "state":"IL",
   "address":"201 E Randolph St",
   "lat":41.8826616030636,
   "country":"United States"
}
```

From this the following attributes are extracted:
* Venue Address
* Venue Postalcode
* Venue City
* Venue Latitude
* Venue Longitude

#### Final FourSquare Top Sites Data

A sample of the final FourSquare Top Sites data is shown below:

![Final Foursquare Data](/Images/final_data_ref.png)


### Part 2: Chicago Crime Data

In this part I will be using open source Chicago crime data to provide the user with additional crime data.

This dataset can be download from the [Chicago Data Portal](https://data.cityofchicago.org/) and reflects reported incidents of crime (with the exception of murders where data exists for each victim) that occurred in the City of Chicago in the last year, minus the most recent seven days. A full desription of the data is available on the site.

Data is extracted from the Chicago Police Department's CLEAR (Citizen Law Enforcement Analysis and Reporting) system. In order to protect the privacy of crime victims addresses are shown at the block level only and specific locations are not identified.

| Column Name   | Type          | Description                                            | 
| :------------ | :------------ | :----------------------------------------------------- | 
| Case Number    | Plain Text    | The Chicago Police Department RD Number (Records Division Number), which is unique to the incident. | 
| Date | Date & Time   | Date when the incident occurred. this is sometimes a best estimate. |
| Block	        | Plain Text    | The partially redacted address where the incident occurred, placing it on the same block as the actual address. |
| IUCR	        | Plain Text    | The Illinois Unifrom Crime Reporting code. This is directly linked to the Primary Type and Description. See the list of IUCR codes at https://data.cityofchicago.org/d/c7ck-438e. |
| Primary Type   | Plain Text    | The primary description of the IUCR code. |
| Description	| Plain Text    | The secondary description of the IUCR code, a subcategory of the primary description. |
| Location Description | Plain Text | Description of the location where the incident occurred. |
| Arrest        | Plain Text    | Indicates whether an arrest was made. |
| Domestic      | Plain Text    | Indicates whether the incident was domestic-related as defined by the Illinois Domestic Violence Act. |
| Beat          | Plain Text    | Indicates the beat where the incident occurred. A beat is the smallest police geographic area – each beat has a dedicated police beat car. Three to five beats make up a police sector, and three sectors make up a police district. The Chicago Police Department has 22 police districts. See the beats at https://data.cityofchicago.org/d/aerh-rz74. |
| Ward	        | Number        | The ward (City Council district) where the incident occurred. See the wards at https://data.cityofchicago.org/d/sp34-6z76. |
| FBI Code        | Plain Text    | Indicates the crime classification as outlined in the FBI's National Incident-Based Reporting System (NIBRS). See the Chicago Police Department listing of these classifications at http://gis.chicagopolice.org/clearmap_crime_sums/crime_types.html. |
| X Coordinate	| Plain Text    | The x coordinate of the location where the incident occurred in State Plane Illinois East NAD 1983 projection. This location is shifted from the actual location for partial redaction but falls on the same block. |
| Y Coordinate	| Plain Text    | The y coordinate of the location where the incident occurred in State Plane Illinois East NAD 1983 projection. This location is shifted from the actual location for partial redaction but falls on the same block. |
| Latitude	    | Number        | The latitude of the location where the incident occurred. This location is shifted from the actual location for partial redaction but falls on the same block. |
| Longitude	    | Number        | The longitude of the location where the incident occurred. This location is shifted from the actual location for partial redaction but falls on the same block. |
| Location	    | Location      | The location where the incident occurred in a format that allows for creation of maps and other geographic operations on this data portal. This location is shifted from the actual location for partial redaction but falls on the same block. |
	


Not all of the attributes are required so only the following data was imported:

* Date of Occurance
* Block
* Primary Description
* Ward
* Latitude
* Longitude

A sample of the imported data is shown.

![Chicago Crime Data](/Images/Chicago_data.png)

