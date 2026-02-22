## Demographic Patterns Across Wisconsin Counties (ACS 2024 5-Year Estimates)

Author: Yuanji Zhong

### 1. Project Overview

This project analyzes and visualizes county-level demographic patterns across the state of Wisconsin using the 2024 American Community Survey (ACS) 5-Year Estimates.

Two thematic maps were developed:

- Total Population by County
- Population Density (people per km²)

The objective is to demonstrate spatial data processing, attribute joining, classification techniques, and cartographic design principles using QGIS.

------

### 2. Data Sources

- **Geographic Boundary Data:**
     U.S. Census Bureau TIGER/Line Shapefiles (2025), County-level boundaries data of all county in the United States

- **Demographic Data:**
     U.S. Census Bureau – ACS 2024 5-Year Estimates Table B01003, Total population data of all county in the United States

------

### 3. Data Processing Workflow

The following workflow was implemented in QGIS:

#### Step 1 – Data Preparation

- Imported county boundary shapefile
- Filtered dataset to include Wisconsin counties only
- Imported ACS population CSV file

#### Step 2 – Data Cleaning

- Renamed field `ACSDT5Y2024.B01003_Estimate!!Total` to `Population` and field `ACSDT5Y2024.B01003_Geography` to `CSV_GEOID`
- Verified attribute consistency of `GEOID` fields between shapefile and ACS table (CSV file)

#### Step 3 – Table Join

- Joined ACS population data to county boundaries using `GEOID` and `CSV_GEOID`
- Verified successful join via attribute table inspection

#### Step 4 – Derived Metric Creation

- Calculated land area in square kilometers (using `ALAND`)

- Created new field:

    ```sql
    Pop_Density = Population / (ALAND / 1,000,000)
    ```

- Verified units (people per km²)

------

### 4. Map 1 – Total Population

#### Classification Method

- Natural Breaks (Jenks)
- 5 classes

#### Rationale

The Jenks method was chosen to identify meaningful clusters in population distribution and minimize within-class variance.

#### Key Observations

- Milwaukee County exhibits the highest total population.
- Southeastern Wisconsin contains the largest concentration of residents.
- Northern counties are significantly less populated.
- Clear urban–rural population contrast is visible statewide.

![](.\Wisconsin Population 2024.png)

------

### 5. Map 2 – Population Density

#### Data Transformation

Due to skewness in density distribution, a logarithmic transformation (log10) was applied prior to classification.

#### Classification Method

- Log transformation
- Equal Interval
- 5 classes

#### Rationale

Population density varies dramatically across counties. Log transformation reduces skew and improves visual interpretability.

```sql
Log_Density = log10(Pop_Density)
```

#### Key Observations

- Milwaukee County has the highest population density.
- Suburban counties such as Waukesha, Racine, and Kenosha also exhibit high density.
- Northern Wisconsin counties show very low density.
- The spatial pattern highlights strong metropolitan concentration in the southeast.

![](.\Wisconsin Population Density 2024.png)

------

### 6. Cartographic Design Considerations

- Sequential color ramps were selected for clarity.
- Thousand separators were added to improve legend readability.
- Clear title hierarchy was implemented.
- Scale bar and legend positioned for balance.
- Source citation included in layout.

------

### 7. Technical Skills Demonstrated

- GIS Data Cleaning and Field Management
- Attribute Table Joins
- Spatial Classification Methods (Jenks, Log Transformation)
- Derived Metric Calculation (Population Density)
- Cartographic Layout Design
- Publication-Ready Export in PDF Format

------

### 8. Conclusion

This project demonstrates the ability to transform raw demographic and spatial data into interpretable geographic visualizations. The comparison between total population and population density reveals structural urban concentration patterns across Wisconsin and highlights the importance of appropriate classification methods in thematic mapping.