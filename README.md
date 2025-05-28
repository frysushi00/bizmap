# 📌 **BIZMAP: Intelijen Pemetaan Usaha Berbasis Machine Learning di Pekanbaru** 📌
Internship project for MBKM at Badan Pusat Statistik Provinsi Riau. This repo contains the applications of Machine Learning and Data Analysis for business mapping in Pekanbaru. This includes data analytics and ML development for classification, clustering, and NLP (Semantic search). BIZMAP is designed to transform raw business data into intelligent and accessible geospatial insights, supporting trend analysis, identification of growth patterns, and exploration of factors influencing business development.

## 🛠 TOOLS
* **Machine learning :** TensorFlow, Keras, Transformer (IndoBERT Base P1), Scikit-learn, Hugging Face Transformers (IndoBERT-Base-p1), PyTorch
* **Scraping :** Overpass Turbo, Octoparse
* **Visualization :** Matlotlib, Seaborn, GeoPandas, Contextily
* **Development Environment :** VSCode, Google Colab, Kaggle (GPU T4, and CPU)


## 📁  COMPREHENSIVE DATA SOURCING & PREPROCESSING
The dataset was collected using scraping method from Google Maps and OpenStreetMap.
Main Datasets consist of 39k business datas (after cleaning and preprocessing).
The training data for KBLI classification with CNN consist of more than 1500 business landmark across Pekanbaru, Riau.
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

To ensure data quality and address bias, a meticulous data preprocessing pipeline was implemented:
* **Main Data Cleaning:** Unicode character normalization, removal of irrelevant special symbols, space standardization, and elimination of duplicate data (businesses with name similarity of at least 70% and located within a 2 km radius). Irrelevant data such as places of worship, cemeteries, and general fields were also removed.
* **Model-Specific Training Datasets:**
  * **KBLI Classification:** To mitigate class imbalance and enrich context, additional data (over 1600 rows) from various regions outside Pekanbaru (via Octoparse) were collected. This data focused on underrepresented KBLI categories to enable the model to learn more effectively.
  * **Semantic Search:** The dataset was manually compiled with pairs of user queries (query column) and relevant place type/KBLI labels (label column). This dataset was specifically augmented with diverse examples (paraphrasing and additional varied queries) for classes that showed low performance (e.g., food, cafe, agriculture, bank, rental, school, store, supermarket, florist, health, meal_takeaway, primary_school, shopping_mall, convenience_store, digital_and_information, establishment r, architecture_firm) to improve accuracy and semantic understanding.

## 🧠 MACHINE LEARNING AND MODELS
The core focus of the project is the development and application of machine learning models for in-depth geospatial analysis and text understanding:

### 📊 KBLI CLASSIFICATION MODEL BASED ON CNN (CONV1D)
This model utilizes a **Convolutional Neural Network** (CNN with Conv1D) architecture trained to automatically classify business establishments based on their textual descriptions (placeName and placeTypes) into 21 KBLI (Klasifikasi Baku Lapangan Usaha Indonesia) categories. The process involved TF-IDF feature engineering and handling of class imbalance using class_weight. This model demonstrates promising accuracy in identifying business types in Pekanbaru. There's still bias in the model. But overall the accuracy reach 8

### 📍 DISTRICT-BASED GEOSPATIAL CLUSTERING
To analyze spatial patterns and group business locations based on geographical proximity, clustering methods were implemented. This approach uses **K-Means** to identify 15 clusters resembling the sub-district divisions in Pekanbaru and assigned kelurahan (villages/urban communities) to the nearest kecamatan (sub-districts). The clustering results enable visualization and analysis of business distribution at the administrative regional level, confirming the consistency of the formed clusters with Pekanbaru's map.

### 🔎 GEOSPATIAL-BASED SEMANTIC SEARCH ENGINE WITH TRANSFORMER INDOBERT-BASE-P1
This is the core innovation of the project, integrating natural language intelligence with geospatial mapping. The model was developed through the fine-tuning of the **IndoBERT Base P1** Transformer model.

* **Semantic Query Understanding:** This model is specifically trained to comprehend the semantic intent of user queries in Indonesian, classifying extracted entities into relevant place type labels. Strategies such as gradual unfreezing of transformer layers and class weights in the loss function were applied to improve accuracy, although overfitting remains an area for further improvement.
* **Advanced Search Logic:** The search function integrates semantic place type prediction with keyword matching and geographical distance calculation using the Haversine formula. Search results are prioritized not merely by name matching, but also by semantic relevance and proximity to the user's location, resulting in a smarter and more contextual search experience. Analysis indicates that this approach significantly enhances result relevance compared to searches without the model, especially for ambiguous queries, despite an ongoing tendency towards pure lexical matching that is currently being addressed.

## **RESULTS :**
| **COMPONENTS**                          | **FUNCTIONS**                                                            | **RESULT**                                                                  |
|----------------------------------------|--------------------------------------------------------------------------|------------------------------------------------------------------------------|
| KBLI Classification Model with CNN     | Automatically predict the KBLI category of a business place             | F1 Score:   0.877                                |
| Semantic Search Engine with IndoBERT   | Retrieve the most relevant business based on user queries and location  | Accuracy: > 86%             |
| Geospatial Clustering & Visualization  | Visualize clustered Datas for analysis       | 15 clusters matching Pekanbaru’s regions, clearly visualized on the map     |


The BIZMAP project exemplifies how machine learning can be a powerful tool for geospatial analysis and understanding unstructured data, providing valuable insights for urban planning and business development in Pekanbaru.
