# Canopy gap fraction estimation from ICESat-2 ATL08 product
This repository is to share code I used to produce results for my MSc thesis in Delft Technological University. The topic of the thesis is "Canopy gap fraction
estimation from ICESat-2 ATL08 product" and it was completed in April 2023.

The the full thesis is available at https://repository.tudelft.nl/islandora/object/uuid%3A4c44f0fb-bd69-44d8-8ba9-6ae0b9584828?collection=education 

## Introduction and motivation
The motivation behind my MSc research stems from two things: the importance of forest ecosystems for the global climate, the carbon cycle and biodiversity; and the potential of using ICESat-2 altimetry data for estimating forest structure. It also allowed me to combine my background in 3D spatial data engineering and my passion for environmental studies. I focused my topic around canopy gap fraction which is a unitless measure from 0 to 1 where low values would indicate dense forest with no gaps in the canopy and 1 would indicate very sparse vegetation. It is an inverse of canopy cover as high values of canopy gap fraction indicate low values of canopy cover. It is an important indication of the light conditions on the forest floor, the biomass in the forest and gives insights about the growth state of the forest.

![gap_values_explained](https://github.com/Mschn-k/MSc_thesis/assets/58178795/2c4e3acf-c674-407b-aa37-bd27f293dfcc)

While writing this thesis, I was not aware of any studies that had attempted estimating forest structure from ICESat-2 ATL08 data and publish their results. However, there are plans to publish ATL18 raster product which holds canopy cover data. A study by Neuenschwander et al. 2022 proposed a theory for estimating canopy gap fraction from ATL08 data, but did not test it. The proposed method uses radiometric profiles to correct for the vegetation and ground reflectivity. With my thesis I test two methods for computing canopy gap fraction from ATL08. First I simply use the ratio of canopy to total photons. Then I use the radiometric profile to try to correct for the reflectivity.

My main research question is: To what extent can canopy gap fraction be estimated from ICESat-2 ATL08 product?

## Methods
To answer this question I downloaded openly available airborne lidar point clouds as a reference data as well as ICESat-2 ATL08 data of the entire mainland of Estonia. I filtered the data to only keep the segments with intact forest. I then clipped the airborne point clouds according to the 12 x 100 m segments of the ATL08 and computed canopy gap fraction from the airborne lidar data. Lastly, I computed canopy gap fraction for each segment from the ATL08 data using the two methods and compared the results with ALS data.

![workflow_short](https://github.com/Mschn-k/MSc_thesis/assets/58178795/42fbbf0f-f0b3-4ad0-ae20-8a0c3993022b)

## Results
The results I received were not as accurate as I had hoped. Comparing the canopy gap fraction computed from the ALS data with the results from ATL08 data showed a lot of noise and with the timeframe I had for this project, I was not able to improve the results.
![als_dnsgap_phoratio_all_scatter](https://github.com/Mschn-k/MSc_thesis/assets/58178795/f270c309-e7f2-4466-a796-9dc624d469fa)

However, it was clear that ICESat-2 can capture the annual changes in canopy gap fraction as overall the winter months showed much higher canopy gap fraction than the summer months which could be explained by the absence of leaves in the winter. 
![ices_gap_months_violin](https://github.com/Mschn-k/MSc_thesis/assets/58178795/36a05de9-9e81-4fbd-8bae-7bf981b860d2)

I also noticed that different tree species had some differences in the canopy gap fraction estimated from the ATL08. The tree species reflect the dominant tree species estimated for the segment. Normally in Estonia spruce forest would be considered quite dense forest while pine forests are sparse and can have a lot of light. At least this trend is visible in the violin graph below as well.
![atl08_gap_species_violin](https://github.com/Mschn-k/MSc_thesis/assets/58178795/d48eb260-3c7f-4f7f-b4b2-51fdb4484d44)

Overall I think using ICESat-2 to better understand our forest ecosystem has a lot of potential as it provides continuous data throughout the year and has global coverage. This is something that cannot be achieved by ALS as although the spatial resolution of airborne lidar is most likely higher, its temporal and spatial coverage is much lower.

## Take note
I hope the code here helps somebody - feel free to reach out if you have any questions. Keep in mind that this was a MSc project completed in 2023 with limited time available, therefore it is not a complete and perfect project. I share the code in Jupyter notebooks as it is easier to add notes and explain my thinking process.

# Resources
I would consider the following paper to be the most important one for this thesis:
Neuenschwander, A., Magruder, L., Guenther, E., Hancock, S., and Purslow, M. (2022a).
Radiometric assessment of icesat-2 over vegetated surfaces. Remote Sensing, 14(3):787.
https://doi.org/10.3390/rs14030787

I downloaded the ICESat-2 ATL08 version 5 data from https://nsidc.org/data/atl08/versions/5 but using their API. Please keep in mind that version 5 has some errors in it, therefore if a newer version is available, please use the updated version of ATL08.
The most useful resource to get started with ICESat-2 was the ICESat-2 Hackweek repository: https://github.com/ICESAT-2HackWeek

I dowloaded the ALS point clouds from Estonian Land Board's website: https://geoportaal.maaamet.ee/est/Ruumiandmed/Korgusandmed/Laadi-korgusandmed-alla-p614.html
However, I used their API as well - you should see from the code how I did it. It was a slow process!
The point clouds can be downloaded in 1:2000 map squares. In order to know the which map square and which year I needed, I downloaded the file from this link: 
https://geoportaal.maaamet.ee/est/Ruumiandmed/Kaardilehtede-susteemid/Kaardiruudustikud-allalaadimiseks-p488.html
Once I had the file with map squares, I opened it in QGIS, removed all the squares I did not need and exported it as csv file. Using the csv I was able to download the point clouds automatically.

The article for how the map of dominant tree species in Estonia was created can be found here: https://www.researchgate.net/publication/329655291_Construction_of_tree_species_composition_map_of_Estonia_using_multispectral_satellite_images_soil_map_and_a_random_forest_algorithm
