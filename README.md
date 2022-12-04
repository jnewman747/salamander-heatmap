# Title: Salamander-heatmap

# Background Information
Salamanders are a group of amphibians categorized by elongate, slender bodies, blunt snouts and the presence of a tail. They are typically associated with aquatic habitats (wetlands, seeps, rivers, etc.) but can also be terrestrial.

Salamanders are important because they represent the largest biomass of all vertebrates in the forest. Also, salamanders help control insect populations (particularly insects that humans consider pests like mosquitos). Further, salamanders can be used as “bioindicators” of ecosystem health due to their permeable skin.

 The International Union for Conservation of Nature (IUCN) suggests that 41% of amphibians are threatened with extinction. Kentucky has over 30 species of salamanders occurring within its borders. However, one major threat to amphibians in Kentucky is coal mining (mountain top removal).
 
 I am using species occurrence data from a database contributed to by pre-dominently citizen scientists. The purpose of this map is to create a heatmap of salamanders for the state of Kentucky. 


# Data Management Suggestions
Clone GitHub repository 

Please create a folder called downloaded-data in a directory (e.g. Desktop) outside repositories tracked by GitHub

# Download State Layers
Navigate to the Census Bureau website: https://www.census.gov/cgi-bin/geo/shapefiles/index.php 

![image](https://user-images.githubusercontent.com/115514033/205518902-45ed4b4b-58a6-4834-b0b2-fd2c57f3fa80.png)
    *Tiger/Line shapefile main page one Census Bureau website * 

In the dropdown menu “Select a layer type”, select States (and equivalent). Download this layer tl_2021_us_state.zip to your downloaded-data folder.

![image](https://user-images.githubusercontent.com/115514033/205518968-a403b600-e66d-4845-93b8-156b30ab895e.png)
    *How to select the states shapefile on the Census Bureau website*

SOURCE: Census Bureau (https://www.census.gov/cgi-bin/geo/shapefiles/index.php)


# Download Coal Mining Layer 
Navigate to the Kentucky Mine Mapping website: http://minemaps.ky.gov/Maps/GISData. Download the MMIS Coal Mine Data and Locations file and save to the downloaded-data folder. 

![image](https://user-images.githubusercontent.com/115514033/205520720-6e9e9b06-b8cb-4a9a-8173-98c79e04ac14.png)
Selecting coal mine data from Kentucky

SOURCE: Kentucky Mine Maps (http://minemaps.ky.gov/Maps/GISData) 

# Download species data from Global Biodiversity Information Facility
First, visit the Kentucky Department of Fish and Wildlife Resources (KDFWR) amphibian website (https://fw.ky.gov/Wildlife/Pages/Amphibians.aspx) to get a comprehensive list of salamanders in the state

![image](https://user-images.githubusercontent.com/115514033/205519225-d5f1f120-1ae9-4411-b1a1-2b36bb7e3f46.png)
KDFWR salamander species list

Next, visit the Global Biodiversity Information Facility (GBIF) website (https://www.gbif.us/data/?view=DOWNLOAD) to download occurrence data for each of the individual salamander species.

![image](https://user-images.githubusercontent.com/115514033/205519273-82da93d8-279d-4bae-a706-554020716fff.png)
Global Diversity Information Facility website main portal for downloading species occurrence data


Type the scientific name of the salamander species in the search engine. Several options may show up, but for the purpose of this assignment, I am focusing on species and not subspecies.


![image](https://user-images.githubusercontent.com/115514033/205519335-ce485a08-6d41-416b-a878-14c8a5c904ff.png)
Entering in a scientific name of a salamander species to retrieve its occurrence data


Click Continue and navigate to the Download options. There are three options available. Click the Simple option as it includes coordinates (when available).

![image](https://user-images.githubusercontent.com/115514033/205519381-b51be61f-7879-49eb-bdec-c8bacd3bbb94.png)
Selecting a download option that will give coordinates in a csv file format


Repeat these steps for all salamander species. Save all csv files in downloaded-data folder.


# Species data will require manipulation prior to bringing into QGIS
The GBIF website exports data in csv files. When exported into the text file, the data becomes very messy and disorganized. Use the “Text to columns” in the Data Tab of Excel to split text into proper columns. Sort the data by state (Column G) to find records in Kentucky. 
•	Remove unnecessary characters (e.g. rogue parenthesis following numeric values)

•	Kept the first XX fields, removed XX fields

•	Merge all data into one master file for simplicity 



# Bring Layers into QGIS
•	Layer  Add Layer  Add Vector Layer
    o	Navigate to the specific shape file

•	After adding all the shape files, your map should look like this:
    o	IMAGE

•	Project  Properties  CRS  EPSG 3089 (CRS for Kentucky)
    o	Double check all layers are in this projection, can edit layers individually by right-clicking (XXX)

•	Clip to Kentucky/Filter



# Make a Heat Map


# Print Layout
•	Name:

•	Add a title, scale bar, North arrow, legend

•	Add text: Author, QGIS version, NewMaps, Sources, Projection, Map Scale

•	Edit fonts and sizes to make more readable

•	Be sure to lock layers


