# 🌿 Introduction

## What Are We Building?

In this Jupyter notebook, we will walk through a methodology to model the *probability of presence of Zosteraceae species* in the **Living Lab West** of Sweden, which includes the **Kattegat** and **Skagerrak** regions. Our primary objective is to predict the **suitability of these areas** for Zosteraceae and provide insights into their distribution, thereby aiding **marine spatial planning** decisions.

Zosteraceae, commonly known as **seagrasses**, are a family of **flowering plants** that thrive in **marine environments**. These plants are unique in that they are the only group of **flowering plants** fully adapted to live submerged in **saltwater**. Zosteraceae species, such as **Zostera marina** (eelgrass), are commonly found in **shallow coastal areas** across the globe, particularly in **estuaries**, **mangrove swamps**, and **seagrass meadows**.

These plants play a pivotal role in **coastal ecosystems**. They are essential for:
- **Biodiversity**: Providing habitat and food for various marine species.
- **Carbon sequestration**: Acting as a carbon sink to help mitigate climate change.
- **Ecosystem services**: Contributing to water filtration, sediment stabilization, and erosion control.

In this notebook, we aim to model and predict the **probability of Zosteraceae presence**, which can help with **marine conservation efforts** and **ecosystem management** in these regions.

## Why Are We Building It?

This notebook is created to support the **C2B2-Mistra Hackathon**, which will take place in **October 2025**. The focus of the hackathon is to improve the [**Symphony Tool**](https://www.havochvatten.se/en/eu-and-international/marine-spatial-planning/swedish-marine-spatial-planning/the-marine-spatial-planning-process/development-of-plan-proposals/symphony---a-tool-for-ecosystem-based-marine-spatial-planning.html), developed by the **Swedish Marine and Water Authority (SMWA)**. The **Symphony Tool** is instrumental in assessing **human pressures** on marine ecosystems and supporting **data-driven marine spatial planning**.

For more information, check out the official project repository:

👉 [Symphony GitHub Repository](https://github.com/Mistra-C2B2/MSP-Symphony)

During the hackathon, participants will work on enhancing the **Symphony Layers**, which represent key environmental data used in the tool. To assist them in identifying areas for improvement, I developed the [**Symphony Layers Interactive Explorer**](https://mistra-c2b2-symphony-layers-interactive-explorer-interface.streamlit.app/). This **Web Application for Data Visualization** provides an interactive and transparent overview of the data layers in the Symphony Tool.

The web application offers:
- 📑 A **summary** of each layer, outlining its purpose and attributes.
- 🛠️ A section with **recommendations for data improvement**, providing guidance on modeling and suggesting potential starting points for participants’ work.

The ultimate aim of this notebook is to contribute to improving the **Angiosperms raster** by modeling the **presence probability of Zosteraceae** in this context, which can help inform future **marine spatial planning** and **conservation efforts**.

_____


# 🛠️ Methodology

## Environmental Parameters for the Model

To build an effective model for the **probability of presence** of *Zosteraceae* in the **Living Lab West of Sweden**, I first identified the key environmental parameters that influence the distribution of these plants. This process was guided by both the **Symphony Metadata Report (March 2019)** and relevant scientific studies on angiosperms, particularly seagrasses like **Zostera marina**.

**Key Sources**:
1. The **[Symphony Metadata Report (March 2019)](https://github.com/Mistra-C2B2/Symphony-Layers-Interactive-Explorer/blob/main/Symphony%20Metadata%20March%202019.pdf)** suggests additional environmental parameters such as **water depth**, **substrate salinity**, and **exposure**.
2. A recent study on the **[distribution and co-occurrence patterns of charophytes and angiosperms in the northern Baltic Sea](https://www.nature.com/articles/s41598-023-47176-8)** lists several important environmental variables to model the distribution of **Angiosperms**, including **Zosteraceae**.

Based on these recommendations and the available environmental data, I compiled the following list of parameters essential for the model:

- **Water depth**
- **Slope of seabed**
- **Salinity**
- **Wave exposure**
- **Current velocity**
- **Water temperature**
- **Concentration of nitrates**
- **Concentration of phosphates**
- **Chlorophyll a content of the sea surface**
- **Proportion of ice cover**
- **Proportion of soft sediment**

While the environmental parameters provide a good foundation, the most crucial input for this model is the **presence data of Zosteraceae species**. The **Zosteraceae observation dataset** I used comes from a large repository of plant observations. However, as it contains only **presence data** and not **absence points**, the **MaxEnt model** (a **presence-only model**) is the ideal choice for this analysis.


## MaxEnt Model

**MaxEnt** (Maximum Entropy) is a widely-used **species distribution modeling (SDM)** system that predicts the **probability of species occurrence** based on **presence data** and **environmental variables**. 

The **MaxEnt model** operates as a **presence-background model**:
- **Presence data**: It uses observed occurrences of the species.
- **Background data**: Instead of using absence data (where the species is not found), MaxEnt uses a random sample of points (the **background samples**) from the landscape where the species could potentially be found. 

The absence data is **not required**, which is why **MaxEnt** is particularly useful when working with **presence-only data** like the one we have for **Zosteraceae**.

For further details on how the MaxEnt model works and how it's implemented in Python, refer to the documentation of the library I used:  
👉 [**elapid documentation**](https://earth-chris.github.io/elapid/sdm/maxent/)


## Available Datasets

Using the **Symphony Layers Interactive Explorer**, I easily identified the necessary datasets to complete the model. These datasets include both **Zosteraceae presence data** and **environmental variables**.

1. **Zosteraceae Observations**

   I obtained the **Zosteraceae observation data** from the **Global Biodiversity Information Facility (GBIF)**, which provides a comprehensive dataset of species occurrences.

   **Source**: 🌱 [Artportalen via GBIF](https://www.gbif.org/dataset/38b4c89f-584c-41bb-bd8f-cd1def33e92f)

2. **Environmental Variables**

   The environmental datasets were obtained from the **Copernicus Marine Data Store** and **EMODnet**. These datasets provide detailed environmental conditions such as temperature, salinity, exposure, and bathymetry, which are essential for modeling the habitat suitability of Zosteraceae.

   **Source**:  
   - 🌐 [Baltic Sea Physics Reanalysis](https://data.marine.copernicus.eu/product/BALTICSEA_MULTIYEAR_PHY_003_011/description)  
   - 🧪 [Baltic Sea Biogeochemistry Reanalysis](https://data.marine.copernicus.eu/product/BALTICSEA_MULTIYEAR_BGC_003_012/description)  
   - 🌊 [Baltic Sea Wave Hindcast](https://data.marine.copernicus.eu/product/BALTICSEA_MULTIYEAR_WAV_003_015/description)  
   - 🗺️ [EMODnet Bathymetry](https://emodnet.ec.europa.eu/en/bathymetry)

   
_____

# 🚀 Let's start:

Each step of the precess is explain in a specific Notebook. Just follow the steps.

### **Step 0** : Setup (Python environment and requirements) 📚

Install the dependencies using:

`pip install -r requirements.txt`


### **Step 1** : Dowloading the data 📥


### **Step 2** : Preprocesssing 🛠️

#### A. 📅 Calculating the annual mean - Temporal Resampling

#### B. 🗺️ Creating a spatial mask

#### C. 🌐 Creating and Apply a 250x250m grid - Saptial Resampling

### **Step 3** : Filter and format the inputs ➡️

#### A. 🔢 Correlation Matrix

#### B. 📄 Format of the inputs

### **Step 4** : Applying the MaxEnt Model 🚀
