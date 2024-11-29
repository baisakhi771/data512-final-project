# Wildfires' Impact on Tourism in California National Parks
## DATA512 - Baisakhi Sarkar, Master of Science in Data Science at University of Washington 2023-2025


**❗Important Note: The starting dataset named USGS_Wildland_Fire_Combined_Dataset.json could not be uploaded to git since it is 2.17GB and even after compresion it is 700Mb. But locally that is placed inside the Data folder and used (from local) in the Wildfire_Analysis_Data_Acquisition.ipynb using relative path. The dataset was fetched from [Combined Wildland Fire Datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). Please refer to this [google drive link](https://drive.google.com/file/d/1pC53GdgGRLODnyM4T8Hmasr59CkxENrv/view?usp=sharing) to get the dataset.**

---

## **Goal**
Summers in the western United States are increasingly characterized by severe wildfires with smoke spreading across multiple states. While various factors like climate change, forestry policies, and land management practices contribute to wildfires, their impacts are far-reaching, especially in sectors like tourism. 

California, home to numerous national parks, experiences frequent wildfires during the dry summer months, raising concerns about their effects on park visitation and the local economy. Tourism is a key economic driver for many regions in California, and disruptions caused by wildfires could have significant socio-economic consequences. This study aims to explore and quantify the relationship between wildfire smoke and tourism, focusing on visitation trends in national parks.

---

## **Research Questions**
This project investigates the following key questions:

1. How does wildfire smoke impact annual and monthly visitor counts in California's national parks?
2. Are certain parks more sensitive to smoke exposure than others based on distance and smoke intensity?
3. How do seasonal variations in visitor counts correlate with wildfire activity during the fire season?
4. Can predictive models estimate future trends in park visitation under increasing wildfire scenarios?

---

## **Study Design**
This project is divided into two parts:

### **1. Smoke Estimation and Trend Analysis (1964–2020)**
- **Wildfire Analysis**: Using historical wildfire data, smoke estimates were generated to quantify the intensity of smoke exposure in proximity to each park.
- **Visitor Data Analysis**: Historical visitor data for national parks was analyzed to identify trends, correlations with wildfire smoke, and seasonal patterns.
- **Correlation Analysis**: Relationships between smoke exposure and visitor counts were assessed for each park.

### **2. Prediction and Forecasting (2021–2050)**
- **Modeling Visitor Trends**: Time-series models were developed to predict future park visitation trends under increasing wildfire scenarios.
- **Scenario Analysis**: The study examined whether future wildfire smoke trends would lead to significant disruptions in tourism.

---

## **Data Sources**
The analysis relied on two main datasets:

1. **Wildfire Data**:
   - **Source** - **[Wildfire Data](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)**: US Geological Survey Combined Wildland Fire Datasets (1964–2020).
   - **Description**: This dataset includes detailed information about wildfires, including size, location, and year of occurrence. 
   - **Usage**: Smoke estimates are calculated based on wildfire proximity, size, and duration, offering insights into the intensity of smoke exposure for each park.

2. **Tourism Data**:
   - **Source** - **[Tourism Data](https://irma.nps.gov/Stats/Reports/Park/YOSE)**: (Please select "Recreation Visits By Month (1979 - Current Calendar Year" option from the list) National Park Service Visitor Use Statistics (10 National Parks with 650 miles of Palmdale, California are considered). This [link](https://irma.nps.gov/Stats/SSRSReports/Park%20Specific%20Reports/Recreation%20Visitors%20By%20Month%20(1979%20-%20Last%20Calendar%20Year)?Park=REDW) gives the csv report for each park visitor statistics, the park name and years needs to be selected accordingly.
   - **Description**: This dataset provides annual and monthly visitor counts for national parks in California, broken down by park and type of visit (e.g., recreational, camping).
   - **Usage**: Visitor data helps analyze the correlation between smoke exposure and tourism patterns, and supports trend analysis over time.

---

### API and Documentation
Air quality data was required to assess the performance of the smoke estimate created. This data was obtained from the [US Environmental Protection Agency (EPA) Air Quality Service (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html). The AQS API provides historical air quality data but does not support real-time monitoring. The [API documentation](https://aqs.epa.gov/aqsweb/documents/data_api.html) offers detailed descriptions of various parameters and examples of API calls.

The US EPA was established in the early 1970s, but standardized monitoring with quality assurance procedures only began in the 1980s. As a result, many counties have air quality data starting between 1983 and 1988, while some counties still lack monitoring stations.
The AQS API resolves this limitation by offering search functionalities for monitoring stations and data. Users can query the API using station IDs, county designations, or geographic bounding boxes.

Additional details about the Air Quality System can be found in the [EPA AirData FAQ](https://www.epa.gov/outdoor-air-quality-data/frequent-questions-about-airdata).

---

### Intermediate Data Files: 

During the course of this study, mainly three intermediate data files were created (two other redundant files are also generated but not used later for analysis):

1. **Past_60_years_wildfires_with_distances_from_Palmdale.csv**
- Generated from Analysis/Wildfire_Analysis_Data_Acquisition.ipynb and used in Analysis/Wildfire_Analysis_Data_Analysis_and_Prediction.ipynb
- This CSV file contains data on all wildfire instances spanning the years 1964 to 2020.

2. **Yearly_AQI_Data.csv**
- Generated from Analysis/Wildfire_Analysis_Data_Acquisition.ipynb and used in Analysis/Wildfire_Analysis_Data_Analysis_and_Prediction.ipynb
- This CSV file stores the maximum AQI values for each fire season (from May 1st to October 31st) on an annual basis for Palmdale, California.

3. **Final_Wildfire_Data_Cleaned.csv** 
- Generated from Analysis/Wildfire_Analysis_Data_Cleaning.ipynb. This is the final dataset used for analysis and predictive modelling in Analysis/Wildfire_and_Tourism_Data_Analysis_and_Prediction.ipynb and Analysis/Wildfire_Analysis_Data_Analysis_and_Prediction.ipynb
- This cleaned dataset was created by removing irrelevant columns, filtering out wildfires which are more than 650 miles away from Plamdale, California. The resulting dataset contains 45,891 rows and 9 columns.

---

## **Methodology**
1. **Data Cleaning and Preprocessing**:
   - Standardized visitor counts and calculated annual totals for each park.
   - Removed outliers and filled missing data to ensure consistency.

2. **Smoke Estimate Calculation**:
   - Proximity-based smoke exposure was calculated for each park, considering fire size and distance from the park.

3. **Time-Series Modeling**:
   - **SARIMAX Model**: Used for historical and future predictions of visitor counts and smoke trends.

4. **Correlation Analysis**:
   - Evaluated the relationships between smoke estimates and visitor counts for each park.

5. **Visualization**:
   - Created scatter plots, trend lines, and heatmaps to illustrate relationships and trends.

---

## **Results**
### **1. Key Findings**
- **Correlation Analysis**:
  - Parks closer to wildfire-prone areas exhibited higher correlations between smoke estimates and visitor declines (e.g., Santa Monica: 0.51 correlation).
  - Distant parks like Redwood showed weaker correlations with smoke exposure.
- **Time-Series Predictions**:
  - Predicted visitor counts for 2021–2050 indicated varying levels of resilience across parks, with some parks maintaining steady visitation trends despite increasing wildfire smoke.

### **2. Visualization Highlights**
- **Scatter Plots**: Showcased relationships between smoke exposure and visitor counts for each park.
- **Grid Plots**: Displayed predicted visitor counts and trends for individual parks.
- **Bar Charts**: Ranked correlations and distances from Palmdale, CA, to identify parks most vulnerable to smoke impacts.

---

### Reproducibility

To ensure the reproducibility of this project, all workflows and analyses have been meticulously documented and implemented in a well-organized directory structure. The project includes clearly labeled directories for raw data, processed data, scripts, Jupyter notebooks, and results, ensuring a logical progression from data retrieval to final outputs. All datasets used are either included in the repository (where licensing permits) or accessible via publicly available links, with detailed instructions for downloading and preprocessing provided in the documentation.  Automation scripts handle repetitive tasks like data cleaning, smoke estimation, and model training, simplifying the replication of results. Each Jupyter notebook is modular and well-commented, making the analysis pipeline transparent and easy to follow. Version control is managed through Git, ensuring that changes are traceable and reversible, with unnecessary files excluded via a .gitignore file. For further ease of reproducibility, a reproducibility guide has been included, detailing steps to get data, process data, run analyses, and regenerate visualizations. This ensures that anyone with access to the repository can replicate the findings, validate the methodologies, and extend the analysis with minimal effort.

#### **Reproducibility Guide**

1. Start by getting data from the above mentioned data sources.
2. Download the complete codebase from this git repository.
3. Start your python kernel to run jupyter notebooks.
4. Run Analysis/Wildfire_Analysis_Data_Acquisition.ipynb notebook completely for data fetching and csv conversions.
5. Run Analysis/Wildfire_Analysis_Data_Cleaning.ipynb notebook for data cleaning and it will generate the cleaned data dile in Intermediate_files folder for further usage. All data references are made using relative path so that it doesnt cause any issues later.
6. Run Analysis/Wildfire_Analysis_Data_Analysis_and_Prediction.ipynb to get smoke estimates and its predictions.
7. Run Analysis/Wildfire_and_Tourism_Data_Analysis_and_Prediction.ipynb for Smoke and Tourism correlations.
8. Check all output vizualizations generated inside notebook or from Results folder.

---

### Known Issues or Assumptions:

Both the Wildfire and AQI datasets used in this analysis were developed based on several key assumptions to ensure consistency and relevance to the study objectives. Below are the key assumptions and the rationale behind them:

**1. Fire Season Definition:**
The fire season was defined as the period from May 1st to October 31st each year. This time window reflects when most wildfires occur and when their impact on air quality is most significant.

**2. Maximum AQI as Annual Estimate:**
For each fire season, the maximum AQI value was selected to represent the AQI for that year. This assumption aligns with the focus of this study, which is to capture the most extreme pollution events likely driven by wildfire smoke.
Using the maximum AQI ensures that high-impact pollution incidents, which can have the most adverse effects on public health and air quality, are not overlooked.

**3. Missing Data Handling:**
AQI data was only available for select years, with many counties having incomplete or no monitoring data prior to the 1986. In such cases, AQI estimates are only reported when available, and missing years were not imputed to avoid introducing bias.

**4. No Exogenous Variables:**
Although factors like wind direction, humidity, and temperature influence smoke dispersion, they were not included in the model due to data unavailability for the entire study period.
These assumptions were made to maintain consistency across datasets, ensure data quality, and focus on the extreme pollution events most relevant to policymakers and public health officials.

---

## **Implications**
### **Policy Recommendations**:
- Parks with high correlations (e.g., Santa Monica) require targeted smoke mitigation strategies to minimize disruptions in tourism.
- Investments in air quality monitoring and public health measures can reduce the long-term impacts of wildfire smoke.

### **Tourism Management**:
- Seasonal trends indicate that peak summer months coincide with wildfire seasons, requiring adaptive management strategies to maintain visitation levels.
- Enhanced communication about air quality conditions could help visitors plan safer trips during fire seasons.

### **Future Research**:
- Investigate demographic and economic impacts of declining park visitation on local communities.
- Extend analysis to explore the effects of wildfires on park revenue and ecosystem health.

---

## **Conclusion**
This study underscores the importance of understanding the intersection of wildfires and tourism, especially in wildfire-prone regions like California. By analyzing historical trends and forecasting future scenarios, this project provides actionable insights for park managers, policymakers, and local communities to adapt and thrive in the face of increasing wildfire activity.

