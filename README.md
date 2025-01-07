![carbon-dioxide-emissions](https://github.com/user-attachments/assets/3d00476e-40f2-4ec0-8129-4db306845ddf)

# CO2 Emission Analysis (2001-2021)

Welcome to the **CO2 Emission Analysis Project**! This repository showcases a SQL-based analysis of CO2 emissions across the world from 2001 to 2021. The project investigates global trends, identifies key contributors, and uncovers insights about CO2 emissions from various sources such as coal, oil, gas, cement, and flaring.

---

## **Table of Contents**

- [Introduction](#introduction)
- [User Story](#user-story)
- [Project Objectives](#project-objectives)
- [Schema Overview](#schema-overview)
- [Analysis Highlights](#analysis-highlights)
- [SQL Queries](#sql-queries)
- [Technologies Used](#technologies-used)
- [Future Enhancements](#future-enhancements)

---

## **Introduction**

This project provides an in-depth SQL analysis of global CO2 emissions data over two decades. The analysis identifies trends, top contributors, and growth patterns to facilitate data-driven insights into global and country-specific emissions.

---

## **User Story**

### **Background**

With increasing concerns over climate change, understanding CO2 emissions is essential for informed decision-making and sustainable development. This project aims to provide actionable insights into emission patterns and identify areas for intervention.

### **Analyst's Journey**

As a data analyst, my goal was to answer critical questions such as:
- Which countries emit the most CO2?
- What are the primary sources of CO2 emissions globally and by country?
- How has CO2 emission per capita evolved over the years?
- Which countries contribute the least to global emissions?

---

## **Project Objectives**

1. Analyze global CO2 emissions from 2001 to 2021.
2. Identify top and bottom contributors to CO2 emissions.
3. Classify countries based on CO2 emission per capita.
4. Calculate year-over-year growth and cumulative emission distribution.
5. Examine contributions by emission sources: coal, oil, gas, cement, and flaring.

---

## **Schema Overview**

The dataset contains CO2 emission metrics for various countries. Key columns include:
- **Country**: Name of the country.
- **Year**: Year of the record.
- **Total**: Total CO2 emissions (metric tonnes).
- **Coal, Oil, Gas, Cement, Flaring**: CO2 contributions by source.
- **Per_Capita**: Emissions per person.

---

## **Analysis Highlights**

### **Key Insights**

1. **Top Contributors**:
   - Countries with the highest average emissions over two decades.
   - Largest CO2 emitters per capita in 2021.

2. **Growth Trends**:
   - Yearly global CO2 emissions.
   - Year-over-year growth in emissions.

3. **Classification of Emissions**:
   - High, medium, and low per capita CO2 emitters.
   - Cumulative distribution of global emissions.

4. **Source Analysis**:
   - Contributions by coal, oil, gas, cement, and flaring globally and in specific countries.

---

## **SQL Queries**

Here are examples of SQL queries executed in this project:

1. **Top 10 Countries with Highest Average CO2 Emissions (2001-2021)**
   ```sql
   SELECT country, ROUND(AVG(total), 3) AS average_CO2_emission
   FROM co2emission
   WHERE year BETWEEN 2001 AND 2021
   GROUP BY country
   ORDER BY average_CO2_emission DESC
   LIMIT 10;
   ```

2. **Year-over-Year Growth of Global Emissions**
   ```sql
   SELECT year, 
          SUM(total) AS global_emission,
          (SUM(total) - LAG(SUM(total)) OVER (ORDER BY year)) / LAG(SUM(total)) OVER (ORDER BY year) * 100 AS yoy_growth
   FROM co2emission
   GROUP BY year
   ORDER BY year;
   ```

3. **Percentage Contribution of CO2 by Source (India, 2021)**
   ```sql
   SELECT country, total, 
          ROUND((coal / total) * 100, 3) AS coal_percentage,
          ROUND((oil / total) * 100, 3) AS oil_percentage,
          ROUND((gas / total) * 100, 3) AS gas_percentage,
          ROUND((cement / total) * 100, 3) AS cement_percentage
   FROM co2emission
   WHERE country = 'India' AND year = 2021;
   ```

---

## **Technologies Used**

- **Database**: PostgreSQL
- **Query Tool**: pgAdmin4

---

## **Future Enhancements**

1. Incorporate Python for deeper visualization and reporting using Pandas and Matplotlib.
2. Use machine learning techniques to predict future CO2 emissions.
3. Expand the dataset to include renewable energy usage.

---

Feel free to explore the queries and insights in this repository. Contributions and feedback are welcome!
