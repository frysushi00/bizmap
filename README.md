# bizmap
Internship project in collaboration with Badan Pusat Statistic Prov. Riau. This repo contains my part (ML) only, that includes data analytics and ML development for classification, clustering, and NLP

## TOOLS
* **Machine learning :** TensorFlow, Keras, Transformer, Scikit-learn
* **Scraping :** Overpass Turbo, Octoparse
* **Visualization :** Matlotlib
* **IDE :** VSCode, Google Colab, Kaggle (GPU T4, and CPU)


## DATASETS
The dataset was collected using scraping method from Google Maps and OpenStreetMap.
The training data consist of more than 1500 business landmark across Pekanbaru, Riau.
The tools used for scraping are OctoParse and Overpass Turbo.
The dataset contains:
* placeId : IDs of places (Unique)
* placeName : Building / landmark names
* placeAddress : Adresses of the Buildings
* placeBusinessStatus : OPERATIONAL or CLOSED_TEMPORARY
* placeTypes : General types of the buildings, ex: park, florist, mining, etc.
* placeLatitude
* placeLongitude
* kbli : KBLI (Klasifikasi Baku Lapangan Usaha Indonesia)'s category. This was classified using the KBLI Classification model. There are 21 classes A-U. You can see the details here : [KBLI 2020](https://oss.go.id/informasi/kbli-berbasis-risiko)


## MACHINE LEARNING AND MODELS
My part of internship was to make models and apply machine learning and doing some data analysis. Mostly my machine learning works here involved geospatial data.

### KBLI CLASSIFICATION MODEL
The .ipynb of this model can be downloaded from this repository. I basically use simple Neural Network and also tried Convolutional Neural Network also. Both models workes nicely for classifying the KBLI category from Pekanbaru's business places.

### DISTRICT BASED GEOSPATIAL CLUSTERING
The .ipynb can also be downloaded. This clustering means to make clusters based on the latitude and longitude of the buildings and latitude and longitude from Pekanbaru's region (15 region). I use KNN and K-Means both result on the same clusters. You can overlay the clustering results with Pekanbaru's map and it looks quite similar.

### GEOSPATIAL BASED SEARCH ENGINE WITH AUTOFILL
Contains two models, one for generic semantic search engine (semanic similarity model) and one is for the autofill fitur. Both models then roceeds onto the SE functions to create the search engine that counts the semantic similarity and also the distance of the places from user's location and return the most similar and the closest place.
