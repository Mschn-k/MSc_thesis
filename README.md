# Canopy gap fraction estimation from ICESat-2 ATL08 product
This repository is to share code I used to produce results for my MSc thesis in Delft Technological University. The topic of the thesis is "Canopy gap fraction
estimation from ICESat-2 ATL08 product" and it was completed in April 2023.

The the full thesis is available at https://repository.tudelft.nl/islandora/object/uuid%3A4c44f0fb-bd69-44d8-8ba9-6ae0b9584828?collection=education 

## Introduction and motivation
The motivation behind my MSc research stems from two things: the importance of forest ecosystems for the global climate, the carbon cycle and biodiversity; and the potential of using ICESat-2 altimetry data for estimating forest structure. It also allowed me to combine my background in 3D spatial data engineering and my passion for environmental studies. I focused my topic around canopy gap fraction which is a unitless measure from 0 to 1 where low values would indicate dense forest with no gaps in the canopy and 1 would indicate very sparse vegetation. It is an inverse of canopy cover as high values of canopy gap fraction indicate low values of canopy cover. It is an important indication of the light conditions on the forest floor, the biomass in the forest and gives insights about the growth state of the forest.

While writing this thesis, I was not aware of any studies that had attempted estimating forest structure from ICESat-2 ATL08 data and publish their results. However, there are plans to publish ATL18 raster product which holds canopy cover data. A study by Neuenschwander et al. 2022 proposed a theory for estimating canopy gap fraction from ATL08 data, but did not test it. The proposed method uses radiometric profiles to correct for the vegetation and ground reflectivity. With my thesis I test two methods for computing canopy gap fraction from ATL08. First I simply use the ratio of canopy to total photons. Then I use the radiometric profile to try to correct for the reflectivity.

My main research question is: To what extent can canopy gap fraction be estimated from ICESat-2 ATL08 product?

## Methods
To answer this question I downloaded openly available airborne lidar point clouds as a reference data as well as ICESat-2 ATL08 data of the entire mainland of Estonia. I filtered the data to only keep the segments with intact forest. I then clipped the airborne point clouds according to the 12 x 100 m segments of the ATL08 and computed canopy gap fraction from the airborne lidar data. Lastly, I computed canopy gap fraction for each segment from the ATL08 data using the two methods and compared the results with ALS data.

## Results
The results I received were not as accurate as I had hoped. Comparing the canopy gap fraction computed from the ALS data with the results from ATL08 data showed a lot of noise and with the timeframe I had for this project, I was not able to improve the results. However, it was clear that ICESat-2 can capture the annual changes in canopy gap fraction as overall the winter months showed much higher canopy gap fraction than the summer months which could be explained by the absence of leaves in the winter. 

Overall I think using ICESat-2 to better understand our forest ecosystem has a lot of potential as it provides continuous data throughout the year and has global coverage. This is something that cannot be achieved by ALS as although the spatial resolution of airborne lidar is most likely higher, its temporal and spatial coverage is much lower.

## Take note
I hope the code here helps somebody - feel free to reach out if you have any questions. Keep in mind that this was a MSc project completed in 2023 with limited time available, therefore it is not a complete and perfect project. I share the code in Jupyter notebooks as it is easier to add notes and explain my thinking process.
