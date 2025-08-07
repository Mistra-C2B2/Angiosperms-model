# 🌿 Introduction 

## What are we building?


In this Jupyter notebook, we will explore an example methodology to model *the probability of presence of the Zosteraceae species* in the Living Lab West of Sweden, which encompasses the Kattegat and Skagerrak regions. The goal is to predict the suitability of these areas for Zosteraceae, providing insights into their distribution and helping inform marine spatial planning decisions. 

Zosteraceae, commonly referred to as Zoster or seagrasses, is a family of flowering plants that grow in marine environments. These plants are unique because they are the only group of flowering plants adapted to live fully submerged in saltwater. They are found in shallow coastal areas around the world, typically in estuaries, mangrove swamps, and seagrass meadows.

Zosteraceae species, such as Zostera marina (eelgrass), play an important role in coastal ecosystems. These seagrasses are crucial for biodiversity, carbon sequestration, and maintaining ecosystem services in marine environments.

## Why are we building it?

This Jupyter notebook is designed to support the first **C2B2-Mistra Hackaton** in **October 2025**. This hackathon focus on improving the [Symphony Tool](https://www.havochvatten.se/en/eu-and-international/marine-spatial-planning/swedish-marine-spatial-planning/the-marine-spatial-planning-process/development-of-plan-proposals/symphony---a-tool-for-ecosystem-based-marine-spatial-planning.html) developed by the Swedish Marine and Water Authority (SMWA). The **Symphony Tool** is instrumental in assessing human pressures on marine ecosystems, guiding data-driven marine spatial planning.

For further details, refer to the official project repository:

👉 [Symphony GitHub Repository](https://github.com/Mistra-C2B2/MSP-Symphony)

In the hackathon participants participants will work on improving the **Symphony Layers**. To assist them in identifying areas for data improvement, I have developed the [Symphony Layers Interactive Explorer](https://mistra-c2b2-symphony-layers-interactive-explorer-interface.streamlit.app/). This **Web Application for Data Visualisation** provides a transparent and interactive overview of the data layers used within the Symphony Tool.

The web application provides:
- 📑 A **summary** of each layer. 
- 🛠️ A section with **recommendations for data improvement**, designed to guide participants in modeling the raster data and suggest useful starting points for their work.

This notebook aims to improve the *Angiosperms* raster.
_____


# 🛠️ Methodology / Theory

## Environmental parameters of the model

Based on the **summary** and the **recommendation for data improvement** of the *Angiosperms* layer and additional studies of angiosperms, I have dressed a list of the relevant parameters. The [Symphony Metadata Report (March 2019)](https://github.com/Mistra-C2B2/Symphony-Layers-Interactive-Explorer/blob/main/Symphony%20Metadata%20March%202019.pdf) recommends using additional environmental criteria such as *water depth*, *substrate salinity*, and *exposure* to model the Angiosperms probability of presence.  In addition, a study of the [distribution and co-occurrence patterns of charophytes and angiosperms in the northern Baltic Sea](https://www.nature.com/articles/s41598-023-47176-8) lists relevant parameters to create a model for Angiosperms plants. 

Here is the list of environmental variables I need for my model:
- Water depth
- Slope of seabed
- Salinity 
- Wave exposure
- Current velocity
- Water temperature
- Concentration of nitrates
- Concentration of phosphates
- Chlorophyll a content of sea surface
- Proportion of ice cover
- Proportion of soft sediment

Most of all I need observations data of Zosteraceae species. The Zosteraceae point dataset I used is coming from a very big database of observations. However this means I don't have absence points. That's why the MaxEnt Model, a presence only model.

## MaxEnt model

Maxent is a species distribution modeling (SDM) system that uses **species observations** and **environmental data** to predict where a species might be found under past, present or future environmental conditions.

It's a presence/background model. Maxent uses data on where a species is present and, instead of data on where it is absent, it uses a random sample of the landscape where you might expect to find that species. This is convenient because it reduces data collection requirements, but it also introduces some unique challenges for fitting and interpreting models.

background samples (a sample of environments in the landscape) 

For further information sea the documentation of the library I used :
👉 [`elapid` documentation](https://earth-chris.github.io/elapid/sdm/maxent/)

## Available datasets

Helping me with the [Symphony Layers Interactive Explorer](https://mistra-c2b2-symphony-layers-interactive-explorer-interface.streamlit.app/), I easely found relevant datasets to complete my needs.

### Observations

I have downloaded the dataset of *Zosteraceae* obstervations on [GBIF](https://www.gbif.org).

*Source* : 🌱 [Artportalen](https://www.gbif.org/dataset/38b4c89f-584c-41bb-bd8f-cd1def33e92f)

### Environmental variables

I have downloaded datasets of the environmental variables on [Copernicus Marine Data Store](https://data.marine.copernicus.eu/products).

*Source* : 

- 🌐 [Baltic Sea Physics Reanalysis](https://data.marine.copernicus.eu/product/BALTICSEA_MULTIYEAR_PHY_003_011/description)
- 🧪 [Baltic Sea Biogeochemistry Reanalysis](https://data.marine.copernicus.eu/product/BALTICSEA_MULTIYEAR_BGC_003_012/description)
- 🌊 [Baltic Sea Wave Hindcast](https://data.marine.copernicus.eu/product/BALTICSEA_MULTIYEAR_WAV_003_015/description)
- 🗺️ [EMODnet Bathymetry](https://emodnet.ec.europa.eu/en/bathymetry)





_____

# 🚀 Let's start:

### **Step 0** : Setup (Python environment and requirements) 📚


### **Step 1** : Dowloading the data 📥


### **Step 2** : Preprocesssing 🛠️

This step is the most important one because it prepares and formats the data for the model. Any mistake can influance your result and it is very difficult to found the mistake analyzing the final result. I have applyed 2 diffrent transformations to my datasets :
#### A. 🗺️ Creating a spatial mask and spatially filter the inputs

I was thinking that I had to filter the raster I dowloaded before resampling it but it was unecessary. 

#### B. 📅 Calculating the annual mean - Temporal Resampling

#### C. 🌐 Creating and Apply a 250x250m grid - Saptial Resampling



### **Step 3** : Filter and format the inputs ➡️

#### A. 🔢 Correlation Matrix

#### B. 📄 Format of the inputs

### **Step 4** : Applying the MaxEnt Model 🚀
