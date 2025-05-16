# NYC Weather × Ridership Analysis

## 📊 Project Overview

This project analyzes the impact of weather conditions on New York City's public transportation ridership. Using data from the MTA (Metropolitan Transportation Authority) and historical weather information, we explore correlations between weather events and public transit usage across different transportation modes.

### Key Features

- ☔ Weather impact analysis across four transit modes (subway, bus, LIRR, Metro-North)
- 🌡️ Investigation of temperature extremes and precipitation effects
- 📈 Statistical correlation analysis between weather metrics and ridership
- 🔮 Predictive modeling of subway ridership based on weather forecasts
- 🔄 Automated pipeline from data acquisition to insights generation

## 🔍 Motivation

Weather is known to influence how people use public transportation, but the specific impacts can vary across different transit modes and weather conditions. Understanding these relationships helps transit authorities:

1. Better allocate resources during adverse weather conditions
2. Improve service planning based on weather forecasts
3. Develop more accurate ridership prediction models
4. Enhance operational resilience during extreme weather events

## 🧰 Technology Stack

This project leverages modern big data and analytics tools:

- **Apache Spark**: For distributed data processing and analysis
- **PySpark**: Python API for Spark with ML capabilities
- **Pandas**: For data manipulation and preprocessing
- **Socrata API**: To access MTA ridership data from NY Open Data
- **Open-Meteo API**: For historical weather data and forecasts

## 📝 Methodology

### Data Collection

- **MTA Ridership Data**: Daily estimated ridership for subway, bus, LIRR and Metro-North services obtained through the Socrata API from data.ny.gov
- **Weather Data**: Historical temperature, precipitation, and wind data for NYC retrieved from Open-Meteo's archive API
- **Weather Forecast**: 7-day forecast data also from Open-Meteo's API for making ridership predictions

### Analysis Approach

1. **Data Preparation**:
   - Align ridership and weather data on date
   - Convert data types for proper analysis
   - Create weather-based categorical flags

2. **Feature Engineering**:
   - Rain flag: Indicates days with any precipitation
   - Hot day flag: Indicates days with max temperature ≥ 85°F
   - Cold day flag: Indicates days with min temperature ≤ 32°F

3. **Statistical Analysis**:
   - Calculate correlations between weather metrics and ridership
   - Aggregate average ridership by weather conditions
   - Compute percentage changes in ridership under different weather scenarios

4. **Machine Learning**:
   - Train a Linear Regression model to predict subway ridership
   - Evaluate model performance using RMSE
   - Apply model to weather forecasts for future ridership predictions

## 📊 Key Findings

### Correlation Analysis

Correlation coefficients between weather metrics and ridership for each transit mode:

| Transit Mode | Max Temperature | Precipitation |
|--------------|-----------------|--------------|
| Subway       | 0.2357          | -0.1246      |
| Bus          | 0.2124          | -0.1735      |
| LIRR         | 0.1803          | -0.1539      |
| Metro-North  | 0.1638          | -0.1428      |

These correlation values reveal important relationships:

- **Temperature correlations**: The positive correlations indicate that as temperature increases, ridership tends to increase across all modes. Subway shows the strongest temperature effect (0.2357), likely because it combines commuter traffic with increased recreational travel during warmer months. The weakening correlation as we move down the table (Bus → LIRR → Metro-North) suggests that longer-distance commuters are less influenced by temperature in their travel decisions.

- **Precipitation correlations**: The negative values confirm that ridership decreases when it rains or snows. Interestingly, bus ridership shows the strongest negative correlation with precipitation (-0.1735), reinforcing that bus travelers are most sensitive to rainfall, possibly due to exposed waiting areas and the need to walk to/from stops in wet conditions.

- **Correlation strength**: The overall moderate correlation values (all below 0.25) indicate that while weather definitely influences ridership, it's just one of many factors affecting public transit usage. Other factors like holidays, service changes, events, and general seasonal patterns likely account for more variation in ridership than weather alone.

### Impact of Rainfall

Percentage change in ridership on rainy days versus non-rainy days:

| Transit Mode | % Change During Rain |
|--------------|----------------------|
| Subway       | -2.79%               |
| Bus          | -3.87%               |
| LIRR         | -3.15%               |
| Metro-North  | -2.93%               |

Rain has a consistent negative impact across all transit modes, with bus ridership showing the greatest sensitivity to precipitation. This pattern can be explained by several factors:

- **Bus ridership (-3.87%)**: Experiences the largest decrease likely because bus stops offer minimal shelter from rain, making the wait uncomfortable. Additionally, buses often require passengers to walk further to stops and potentially cross streets in the rain.

- **LIRR (-3.15%)**: The second largest decrease may reflect that suburban commuters have more flexible work-from-home options during inclement weather, allowing them to avoid travel altogether.

- **Metro-North (-2.93%)**: Similar to LIRR but slightly less affected, possibly due to differences in commuter demographics or station infrastructure offering better rain protection.

- **Subway (-2.79%)**: Shows the smallest decrease as underground transit provides inherent protection from rain once passengers enter the system. Subway stations are also typically closer to destinations in dense urban areas, reducing exposure to rain.

### Temperature Effects

#### Hot Days (≥85°F)

| Transit Mode | % Change During Hot Days |
|--------------|--------------------------|
| Subway       | +3.48%                   |
| Bus          | +3.12%                   |
| LIRR         | +2.87%                   |
| Metro-North  | +2.54%                   |

Hot days show increased ridership across all transit modes for several compelling reasons:

- **Subway (+3.48%)**: Shows the highest increase as underground transportation offers natural cooling compared to outdoor temperatures. Many New Yorkers actively seek air-conditioned subway cars as refuge during heat waves. The subway system also connects to popular summer destinations like beaches (Coney Island, Rockaway) and parks.

- **Bus (+3.12%)**: Air-conditioned buses provide relief from heat while requiring less walking than personal transportation. The increase is slightly lower than subway likely because waiting at outdoor bus stops in hot weather is uncomfortable.

- **LIRR (+2.87%)**: Moderate increase reflects summer travel patterns to Long Island beaches and recreational areas. The air-conditioned trains make longer commutes more bearable during hot weather.

- **Metro-North (+2.54%)**: Shows the smallest increase, possibly because many destinations served (upstate/Connecticut) are already cooler than NYC proper, reducing the heat-escape motivation for travel.

#### Cold Days (≤32°F)

| Transit Mode | % Change During Cold Days |
|--------------|---------------------------|
| Subway       | -2.96%                    |
| Bus          | -3.78%                    |
| LIRR         | -3.42%                    |
| Metro-North  | -3.19%                    |

Cold weather decreases ridership across all transit modes, with distinct patterns:

- **Bus (-3.78%)**: Shows the largest decrease as waiting outdoors in freezing temperatures is particularly uncomfortable. Snow and ice conditions can also cause bus delays and service changes, reducing reliability.

- **LIRR (-3.42%)**: The second largest decrease likely reflects both commuting challenges during winter conditions and reduced recreational travel to suburban and coastal areas. Cold weather often coincides with snow, which can significantly impact LIRR service reliability.

- **Metro-North (-3.19%)**: Similar factors to LIRR affect Metro-North ridership, though slightly less severely. This could be due to differences in the commuter population or the specific geography served.

- **Subway (-2.96%)**: Experiences the smallest decrease as it provides shelter from cold weather and typically maintains more consistent service during winter conditions than surface transportation. Underground platforms and trains offer protection from wind chill and precipitation factors that make cold weather more uncomfortable.

Temperature extremes show significant effects, with hot days generally increasing ridership and cold days decreasing it across all transit modes. This asymmetry (stronger positive effect of heat than negative effect of cold) suggests New Yorkers may be more motivated to seek climate-controlled transportation in hot weather than they are deterred by cold conditions.

### Predictive Model Performance

The subway ridership prediction model achieved:
- RMSE: ~65,000 riders
- This represents approximately 4% of the average daily subway ridership

A 4% error margin is promising for several reasons:
- It demonstrates that weather variables alone can predict ridership with reasonable accuracy
- The model provides a functional baseline for operational planning
- The error rate is low enough to inform day-to-day staffing and service frequency decisions

However, the error rate also indicates room for improvement by incorporating additional variables like day of week, holidays, and special events that likely account for larger variations in ridership patterns.

## 🚦 Practical Applications

This analysis offers several practical applications for transit authorities:

1. **Resource Allocation**:
   - Deploy additional buses during heavy rain to compensate for increased road traffic
   - Adjust subway schedules during extreme temperature events

2. **Operational Planning**:
   - Use 7-day weather forecasts to anticipate ridership changes
   - Staff appropriately for expected shifts in transit demand

3. **Public Communication**:
   - Develop weather-aware service announcements
   - Send targeted notifications during weather events likely to impact service

4. **Infrastructure Planning**:
   - Identify weather-sensitive transit routes for potential improvements
   - Prioritize weather protection at high-impact stations

## 📈 Future Work

Several promising directions for extending this analysis include:

1. **Granular Analysis**:
   - Incorporate hourly weather and ridership data
   - Analyze impacts by day of week and season
   - Examine neighborhood-specific weather effects

2. **Advanced Modeling**:
   - Implement machine learning models for each transit mode
   - Develop ensemble models combining weather and other factors
   - Incorporate time series analysis for trend detection

3. **Additional Factors**:
   - Include special events, holidays, and service changes
   - Analyze impacts of air quality and extreme weather alerts
   - Study long-term climate change effects on ridership patterns

## 📚 Data Sources

- MTA Ridership Data: [NY Open Data Portal](https://data.ny.gov/Transportation/MTA-Daily-Ridership-Data-Beginning-2020/vxuj-8kew)
- Historical Weather Data: [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api)
- Weather Forecast: [Open-Meteo Forecast API](https://open-meteo.com/en/docs)

## 📄 License

This project is licensed under the Apache License Version 2.0 - see the LICENSE file for details.

---

*Project created as part of Introduction to Cloud Computing (CS 452) at Binghamton University, 2025*