# Kentucky Salamander Heatmap



## Background Information
Salamanders are a group of amphibians categorized by elongate, slender bodies, blunt snouts, and the presence of a tail. They are typically associated with aquatic habitats (wetlands, seeps, rivers, etc.) but can also be terrestrial.

Salamanders are important because they represent the largest biomass of all vertebrates in the forest. Also, salamanders help control insect populations (particularly insects that humans consider pests like mosquitos). Further, salamanders can be used as “bioindicators” of ecosystem health due to their permeable skin.

The International Union for Conservation of Nature (IUCN) suggests that 41% of amphibians are threatened with extinction. Kentucky has over 30 species of salamanders occurring within its borders. However, one major threat to amphibians in Kentucky is coal mining (mountain top removal).
 
I am using species occurrence data from a database contributed to by pre-dominently citizen scientists. The purpose of this map is to create a heatmap of salamanders for the state of Kentucky. 



## Data Management Suggestions
1) Clone GitHub repository. 

2) Please create a folder called *downloaded-data* in a directory (e.g. Desktop) outside repositories tracked by GitHub.

3) Download the MMQGIS plugin in QGIS if it hasn't already been installed.



## Download State and County Layers
Navigate to the Census Bureau website: https://www.census.gov/cgi-bin/geo/shapefiles/index.php 

![image](https://user-images.githubusercontent.com/115514033/205518902-45ed4b4b-58a6-4834-b0b2-fd2c57f3fa80.png)                                                      
*Tiger/Line shapefile main page one Census Bureau website*

For the year 2021, in the dropdown menu for “Select a layer type”, select **States (and equivalent)**. Download this file (tl_2021_us_state.zip) to your *downloaded-data* folder.

![image](https://user-images.githubusercontent.com/115514033/205518968-a403b600-e66d-4845-93b8-156b30ab895e.png)                                                  
*How to select the states shapefile on the Census Bureau website*


For the year 2021, in the dropdown menu for “Select a layer type”, select **Counties (and equivalent)**. Download this file (tl_2021_us_county.zip) to your *downloaded-data* folder.

![image](https://user-images.githubusercontent.com/115514033/205731497-8e837b9e-a2c5-4029-9377-a69fb89d9338.png)                                                    
*How to select the county shapefile on the Census Bureau website*


```
SOURCE: Census Bureau (https://www.census.gov/cgi-bin/geo/shapefiles/index.php)
```

## Download Coal Mining Layer 
Navigate to the Kentucky Mine Mapping website: http://minemaps.ky.gov/Maps/GISData. Download the MMIS Coal Mine Data and Locations file and save to the *downloaded-data* folder. 

![image](https://user-images.githubusercontent.com/115514033/205686332-1ae5664a-962d-40cb-bc5e-c310d8780212.png)                                              *Selecting coal mine data from Kentucky*

```
SOURCE: Kentucky Mine Maps (http://minemaps.ky.gov/Maps/GISData) 
```


## Download Species Data from Global Biodiversity Information Facility
First, visit the Kentucky Department of Fish and Wildlife Resources (KDFWR) amphibian website (https://fw.ky.gov/Wildlife/Pages/Amphibians.aspx) to get a comprehensive list of salamanders in the state. Note: You may need to reference Google for scientific names of these species ans this website only provides common names.

![image](https://user-images.githubusercontent.com/115514033/205519225-d5f1f120-1ae9-4411-b1a1-2b36bb7e3f46.png)                                                  
*KDFWR salamander species list*

Next, visit the Global Biodiversity Information Facility (GBIF) website (https://www.gbif.us/data/?view=DOWNLOAD) to download occurrence data for each of the individual salamander species.

![image](https://user-images.githubusercontent.com/115514033/205519273-82da93d8-279d-4bae-a706-554020716fff.png)                                                 
*Global Diversity Information Facility website main portal for downloading species occurrence data*


Type the scientific name of the salamander species in the search engine. Several options may show up, but for the purpose of this assignment, I am focusing on species and not subspecies.


![image](https://user-images.githubusercontent.com/115514033/205519335-ce485a08-6d41-416b-a878-14c8a5c904ff.png)                                                
*Example of entering in a scientific name of a salamander species to retrieve its occurrence data*


Click Continue and navigate to the Download options. There are three options available. Click the Simple option as it includes coordinates (when available).

![image](https://user-images.githubusercontent.com/115514033/205519381-b51be61f-7879-49eb-bdec-c8bacd3bbb94.png)                                              
*Selecting a download option that will give coordinates in a .csv file format*


Repeat these steps for all salamander species. Save all .csv files in *downloaded-data* folder.

```
SOURCE: Global Biodiversity Information Facility (https://www.gbif.us/data/?view=DOWNLOAD)
```

## Manipulation of Species Data 
The GBIF website exports data in .csv files. When exported into the text file, the data becomes very messy and disorganized. Use the “Text to columns” in the Data Tab of Excel to split text into proper columns. Sort the data by state (Column G) to find records in Kentucky. Remove unnecessary characters (e.g. rogue parenthesis following numeric values).

•	Kept the first XX fields, removed XX fields

•	Merge all data into one master file for simplicity and save in the *downloaded-data* folder



## Bring Layers into QGIS
Bring in state layer, county layer, and coal mine layer by clicking on 'Layer' > Add Layer > Add Vector Layer and then navigating to the specific shape file in the *downloaded-data* folder. 

Filter the state layer to Kentucky by right-clicking on the layer, click "Filter" 
![image](https://user-images.githubusercontent.com/115514033/205717495-90686063-b19f-4ef4-885c-58e8f1ede93e.png)                                                  
*Query Builder to filter the states layer to Kentucky*

Execute the following expression ("NAME" from Fields; "=" from Operators; and "Kentucky" from Values) to filter the states down to Kentucky:
```
"NAME" = 'KENTUCKY'
```

Similarly for the county layer, the query builder will be used to filter for counties in Kentucky. This time we will use the State's FIPS code (https://transition.fcc.gov/oet/info/maps/census/fips/fips.txt) for filtering. Kentucky's code is '21'. 

```
"STATEFP" = '21'
```



After adding and filtering the two files, the map should look like this:

![image](https://user-images.githubusercontent.com/115514033/205737687-235485ce-8db6-4f15-8aa6-00a197f58263.png)                                                
*Example of what the salamander occurrence data and coal data look like*


For the coal mine layer, use the newly filtered Kentucky border to clip to Kentucky.
![image](https://user-images.githubusercontent.com/115514033/205724658-d0e04b3e-4dad-4304-a4cf-8a2a769983d9.png)                                               
*Clipping the coal layer by the Kentucky boundary layer*


Bring in species data by clicking on 'Layer' > Add Layer > Add Delimited Text Layer and then navigating to the specific csv file in the *downloaded-data* folder. Clip the layer to the Kentucky state boundary (sometimes coordinates don't get entered into the GBIF database correctly).

![image](https://user-images.githubusercontent.com/115514033/205724318-67dab1be-5d8b-4448-92a3-466cc46da940.png)                                               
*Clipping the salamander occurrence data by the Kentucky boundary layer*

Bring in a basemap, for example Esri Terrain by double clicking on **Esri Terrain** in the XYZ Tiles drop down menu in the QGIS Browser.

Change the CRS of the projection to be a Kentucky projection by clicking on 'Project' - Properties - CRS - EPSG 3089 (CRS for Kentucky). Double check all layers are in this projection. Layers can be edited individually by right-clicking them and changing their CRS.

![image](https://user-images.githubusercontent.com/115514033/206876367-25b97899-d351-416f-805f-9376468908ec.png)                                                
*Example of a filtered and clipped map of Kentucky with occurrence and coal mine data*



## Make a Heat Map
Create a hexbin grid to cover area of interest

•MMQGIS

•Create > Create Grid Layer

Spatially join species data by hexagons

•Processing Toolbox > Vector General > Join attributes by location (summary)


## Print Layout
•	Name:

•	Add a title, scale bar, North arrow, legend

•	Add text: Author, QGIS version, NewMaps, Sources, Tools used, Projection, Map Scale

•	Edit fonts and sizes to make more readable

•	Be sure to lock layers

•	Save in two resolutions: 1) width of 1,200 px and 2) width of 8,000 px



## Linking to the Digital Map
Please use this link to view the Kentucky Salamander Heatmap
(https://github.com/jnewman747/salamander-heatmap) 
