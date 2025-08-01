# CODEALPHA_2

 Unemployment Analysis in India (COVID-19 Impact)

 Task Description

Analyze and visualize the unemployment trends across different regions of India using data from CMIE during the COVID-19 pandemic. Derive insights on patterns, regional disparities and temporal variations using Python and Plotly.

 Dataset Features

The dataset includes the following columns:

* Region: Name of the Indian state or union territory
* Date: Observation date
* Frequency: Measurement frequency (e.g., Monthly)
* Estimated Unemployment Rate (%): Percentage of unemployed individuals in the labor force
* Estimated Employed: Count of employed individuals
* Estimated Labour Participation Rate (%): Percentage of people in the labor force
* Area: Type of area (Urban or Rural)

 Steps and Procedure

 1. Data Preprocessing

* Load the CSV data
* Convert date columns to datetime format
* Rename columns for consistency
* Extract month/year for time-series analysis

 2. Exploratory Data Analysis & Visualizations

 a. Unemployment Rate Over Time by Area

```python
fig = px.line(df, x='Date', y='unemployment_rate', color='Area',
              title='Unemployment Rate Over Time by Area', markers=True,
              labels={'Date': 'Date', 'unemployment_rate': 'Unemployment Rate (%)'})
fig.show()
```

 b. Average Unemployment Rate by Region

```python
region_avg = df.groupby('Region')['unemployment_rate'].mean().sort_values()
fig = px.bar(region_avg, orientation='h',
             labels={'value': 'Average Unemployment Rate (%)', 'index': 'Region'},
             title='Average Unemployment Rate by Region')
fig.show()
```

 c. Seasonal Unemployment Trend (Monthly Average)

```python
df['Month'] = df['Date'].dt.month
monthly_avg = df.groupby('Month')['unemployment_rate'].mean().reset_index()
fig = px.line(monthly_avg, x='Month', y='unemployment_rate', markers=True,
              title='Seasonal Unemployment Trend (Monthly Average)',
              labels={'unemployment_rate': 'Avg Unemployment Rate (%)'})
fig.show()
```

 d. Sunburst Chart (Region → Area)

```python
fig = px.sunburst(df,
                  path=['Region', 'Area'],
                  values='unemployment_rate',
                  color='unemployment_rate',
                  color_continuous_scale='RdBu',
                  title='Unemployment Rate Breakdown by Region and Area')
fig.show()
```
 Interpretation

 Seasonal Trend (Monthly Average)

* April saw the highest unemployment rate (\~23.64%), indicating the peak COVID-19 impact on the labor market.
* Other months maintained unemployment around 9–10%, showing relative stability post-lockdown.

 Regional Insight

* Northern and Eastern regions showed higher average unemployment rates.
* Southern states had comparatively stable employment metrics.

Urban vs. Rural

Unemployment spiked more in urban areas, suggesting lockdowns had greater effects on cities than rural zones.

 Conclusion

This analysis reveals a strong COVID-19-induced shock to employment, especially during national lockdowns in early 2020. Regional and seasonal insights help policymakers identify where and when labor market interventions are most critical.

 Tools Used

* Python (Pandas, Plotly, Seaborn, Matplotlib)
* Jupyter/Colab for code execution and visualization

