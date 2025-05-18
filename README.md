# 📌 **BIZMAP** 📌
Internship project for MBKM at Badan Pusat Statistik Provinsi Riau. This repo contains the applications of Machine Learning and Data Analysis for business mapping in Pekanbaru. This includes data analytics and ML development for classification, clustering, and NLP (Semantic search)

## 🛠 TOOLS
* **Machine learning :** TensorFlow, Keras, Transformer (IndoBERT Base P1), Scikit-learn
* **Scraping :** Overpass Turbo, Octoparse
* **Visualization :** Matlotlib
* **IDE :** VSCode, Google Colab, Kaggle (GPU T4, and CPU)


## 📁 DATASETS
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

I also made dataset specified for each models (classification and semantic search)
* For classification mode i just scrape places that the original dataset lack off, so that the model can learn better (avoiding class imbalance) - This dataset contains 1671 rows (scraped with octoparse from google maps), this is not specified just in Pekanbaru since in Pekanbaru some KBLI type business is not common
* For semantic search the dataset contains examples of user queries (column query) and the correlated labels or placeTypes (column label)

## 🧠 MACHINE LEARNING AND MODELS
My part of internship was to make models and apply machine learning and doing some data analysis. Mostly my machine learning works here involved geospatial data.

### 📊 KBLI CLASSIFICATION MODEL
The .ipynb of this model can be downloaded from this repository. I basically use simple Neural Network and Convolutional Neural Network (Conv1D). Both models workes nicely for classifying the KBLI category from Pekanbaru's business places.

### 📍 DISTRICT BASED GEOSPATIAL CLUSTERING
The .ipynb can also be downloaded. This clustering means to make clusters based on the latitude and longitude of the buildings and latitude and longitude from Pekanbaru's region (15 region). I used K-Means with K=15 (regions). You can overlay the clustering results with Pekanbaru's map and it looks quite similar.

### 🔎 GEOSPATIAL BASED SEMANTIC SEARCH ENGINE
Contains two models, one for generic semantic search engine (semantic similarity model) and one is a classifier model (classifying the entity extracted from the semantic model to a label). Both models then proceeds onto the SE functions to create the search engine that counts the semantic similarity and also the distance of the places from user's location and return the most similar and the closest place.
