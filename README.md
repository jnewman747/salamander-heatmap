# Kentucky Salamander Heatmap



## Background Information
Salamanders are a group of amphibians categorized by elongate, slender bodies, blunt snouts, and the presence of a tail. They are typically associated with aquatic habitats (wetlands, seeps, rivers, etc.) but can also be terrestrial.

Salamanders are important because they represent the largest biomass of all vertebrates in the forest. Also, salamanders help control insect populations (particularly insects that humans consider pests like mosquitos). Further, salamanders can be used as “bioindicators” of ecosystem health due to their permeable skin.

The International Union for Conservation of Nature (IUCN) suggests that 41% of amphibians are threatened with extinction. Kentucky has over 30 species of salamanders occurring within its borders. However, one major threat to amphibians in Kentucky is coal mining (mountain top removal).
 
I am using species occurrence data from a database contributed to by predominantly citizen scientists. The purpose of this map is to create a heatmap of salamanders for the state of Kentucky. 



## Linking to the Digital Map
Please use this link to view the finished Kentucky Salamander Heatmap
(https://jnewman747.github.io/salamander-heatmap/) 



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
The GBIF website exports data in .csv files. When exported into the text file, the data becomes very messy and disorganized. Use the “Text to columns” in the Data Tab of Excel to split text into proper columns. Sort the data by "stateProvince" column to find records in Kentucky. Remove unnecessary characters (e.g. rogue parenthesis following numeric values).

Keep the following fields: gbifID, datasetKey, species, countryCode, locality, stateProvince, occurrenceStatus, decimalLatitude, decimalLongitude, coordinateUncertaintyInMeters, day, month, year. Feel free to keep any other fields of interest. 

Merge all data into one master .csv file for simplicity and save in the *downloaded-data* folder.



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

Change the CRS of the projection to be a Kentucky projection by clicking on 'Project' - Properties - CRS - EPSG 3089 (CRS for Kentucky). Double check all layers are in this projection. Layers can be edited individually by right-clicking them and changing their CRS. Save the salamander and coal layers as GeoJsons by right-clicking each layer individually and clicking Export > Save Feature As > Select "GeoJSON" as the format and select EPSG 3089 as the CRS.

![image](https://user-images.githubusercontent.com/115514033/206876367-25b97899-d351-416f-805f-9376468908ec.png)                                                
*Example of a filtered and clipped map of Kentucky with occurrence and coal mine data*



## Make a Heat Map
Create a hexagonal grid to cover area of interest. Click the MMQGIS plugin > Create > Create Grid Layer. For Units choose "Layer Units", Extent choose "Layer Extent" and for Layer choose the Kentucky state border layer. In the Y spacing field, I am using 5 miles (5 x 5280 = 26400) for this particular hexgrid.

![image](https://user-images.githubusercontent.com/115514033/206881821-7cdf81b9-ddaf-406c-9dcc-07b1cbda3e35.png)
*Creating a hexgrid of 5 miles*

To spatial join the species occurrence data, use the Join attributes by location (summary) tool. This tool is accessed by clicking on the Processing Toolbox > Vector General > Join attributes by location (summary). Select the Hexgrid layer in the "Join to features in" field and the Salamander data in the "By comparing to" field. Check "intersect". For fields to summarise, choose "species" and for fields to calculate choose "sum" and "count."

![image](https://user-images.githubusercontent.com/115514033/206886632-3ae4476f-9e11-428e-8c60-45cd24e7cec7.png)                                                  
*Using the Join attributes tool*


![image](https://user-images.githubusercontent.com/115514033/206882825-905e36c0-f353-47f1-9814-7493b1698113.png)                                                                        
*Example of the salamander species occurrence data hexbin data prior to being classified*


Classify the new hexbin layer by right-clicking the layer (called "Joined layer"), going into its properties and clicking on Symbology. Select "Graduated" for the classification field and then "species count for Value. Select "Natural Breaks (Jenks)" as the Mode. Make sure there are 5 classes. Click "Classify". Choose a color ramp to best describe the heat map. I selected a "cold" color ramp in this scenario due to the smaller categories being highly represented on this map. 

![image](https://user-images.githubusercontent.com/115514033/206884744-d1f69f21-b95b-4927-b3ac-1b37bb357a1a.png)                                                                       
*Choosing the symbology for the heatmap*

Also, edit the stroke style of the hexagons so they don't have lines around them. This can be done in the symbology tab by selecting "no pen" for the stroke style.

Next, change the color of the background screen by clicking on Project > Properties > Background color. In this map, I made it a dark gray.

Then, change the color of the coal mine layer and edit the stroke style ("no pen").

Place the coal mine layer above the county layer in the Layers window. Place the newly classified hexbin heatmap layer above the coal layer in the Layers window.


![image](https://user-images.githubusercontent.com/115514033/206885044-fd5e60c8-5135-4ff0-9a69-5343a719e94a.png)                                                                        
*Example of a final map layout for salamander occurrence data in Kentucky*



## Print Layout
•	Add a title, scale bar, North arrow, legend

•	Add text: Author, QGIS version, NewMaps, Sources, Tools used, Hexbin size, Projection, Map Scale

•	Edit fonts and sizes to make more readable

•	Be sure to lock layers

•	Save in two resolutions: 1) width of 1,200 px and 2) width of 8,000 px



## Conclusions and Takeaways
A general takeaway from this map is that salamanders tend to be more abundant away from coal mines. 

However, this should be received with some caution. It's important to remember that the species occurrence data in this map was collected predominantly by citizen scientists and should be treated as such. For example, many of the entries in the Global Biodiversity Information Facility lack spatial information and therefore don't appear on this map. Additionally, when I filtered the data to Kentucky in Excel, some data still displayed in other states when mapped in QGIS. This could have been an example of user error with inputting incorrect coordinates into the Global Biodiversity Information Facility database or selecting the incorrect state. Further, the error surrounding the coordinates within the database was high, with a maximum error of 2817774m. This could be a result of a number of things such as human error, purposefully obscuring data, lack of up-to-date scientific equipment, etc.

It's also important to remember that this is not a comprehensive list of occurrence data. For example, the Global Biodiversity Information Facility had no records for hellbenders or three-toed amphiumas which are known to occur in the state of Kentucky. It is likely that citizen scientists may not have full access to coal mine sites. Many naturalists, researchers, academics, and state agencies may not even use this website to enter data, but instead monitor the site for species occurrence data.

Future maps could consider using data from iNaturalist (https://www.inaturalist.org/), although the data is often obscured to protect threatened and endangered species. Published papers (e.g. peer review manuscripts, theses, and disertations) could also be considered. Another data source that could be considered is a state agency, however, mappers should be aware that they will likely have to sign data-sharing agreements and may have restrictions on where they can publish their maps. 

For the coal mining data, future maps could consider using earlier data as this data set only includes data as far back as 2004. 
