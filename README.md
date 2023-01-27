# COVID-19 Project Showcase

## Summary: 
### This COVID-19 project demonstrates my data analytical skills by utilizing SQL and Tableau. I used SQL to clean and query the data to create 4 tables, and then visualized the results on a Tableau dashboard. The key findings from the dashboard as of January 2023, show that around 1% of the world's population who have been infected with COVID-19 have died. Additionally, Europe has the highest infection death count and infection rate in the world. The project highlights my ability to effectively use SQL and Tableau to analyze and present data, as well as my ability to extract valuable insights from the data. 


## Author
- [IbrahimsDataVault](https://github.com/IbrahimsDataVault)

## Table of Contents
- [Problem](#Problem)
- [Data Source](#Data-Source)
- [Methods](#Methods)
  - [Data Cleaning](#Data-Cleaning)
  - [Data Analysis](#Data-Analysis)
- [Solutions](#Solutions)
- [Conclusion](#Conclusion) 
- [Next Steps](#Next-Steps) 

## Problem
In this case study, I analyzed data on COVID-19 infection rates and death counts. The goal of this analysis is to understand the spread of the virus and identify any patterns or trends that can help inform policy decisions. The data will be cleaned and organized in SQL, and then visualized using Tableau to gain insights.

## Data Source 
https://ourworldindata.org/covid-deaths
## 
## Methods

### Data Cleaning
```sql
--1. compare the overall deaths to cases ratio for the entire world
SELECT 
  SUM(new_cases) as total_cases,
  SUM(new_deaths) as total_deaths,
  (SUM(new_deaths)/SUM(new_cases))*100 AS death_percentage
FROM
  `sql-portfolio-project-375703.Portfolio_Project.Covid Deaths `
WHERE 
  continent IS NOT NULL
ORDER BY
  1,2
  ```
  <img width="440" alt="image" src="https://user-images.githubusercontent.com/123592482/215175883-5b0dafea-c691-4bb2-a4a9-3c111306ec8c.png">

 ```sql
 --2. Pull the 'total_death_count' for each continent in the location column while filtering out the income (upper, middle, lower class), World, European Union, and International rows that's displayed in the location column
SELECT 
  location,
  SUM(new_deaths) AS total_death_count
FROM 
  `sql-portfolio-project-375703.Portfolio_Project.Covid Deaths `
WHERE
  continent IS NULL AND 
  location NOT LIKE '%income%' AND 
  location NOT LIKE '%World%' AND
  location NOT LIKE '%European Union%' AND
  location NOT LIKE '%International%' 
GROUP BY
  location
ORDER BY 
  total_death_count DESC
  ```
 <img width="392" alt="image" src="https://user-images.githubusercontent.com/123592482/215176243-816edfcc-ea15-4618-a70c-10c0e62e9ab3.png">

 ```sql 
 --3. Countries with highest infection rate per population
SELECT
  location,
  population,
  MAX(total_cases) AS highest_infection_count,
  MAX((total_cases/population)) * 100 AS infection_percent_per_population
FROM
  `sql-portfolio-project-375703.Portfolio_Project.Covid Deaths `
WHERE
  location NOT LIKE '%income%'
GROUP BY
  location,
  population
ORDER BY
  infection_percent_per_population DESC
 ```
 <img width="966" alt="image" src="https://user-images.githubusercontent.com/123592482/215180014-8f896c9e-4fca-422b-bee4-74b546f04b86.png">

 ```sql
 --4. Countries with highest infection rate per population grouped by date 
SELECT
  location,
  population,
  date,
  MAX(total_cases) AS highest_infection_count,
  MAX((total_cases/population)) * 100 AS infection_percent_per_population
FROM
  `sql-portfolio-project-375703.Portfolio_Project.Covid Deaths `
WHERE
  location NOT LIKE '%income%'
GROUP BY
  location,
  population,
  date
ORDER BY
  infection_percent_per_population DESC
 ```
 <img width="962" alt="image" src="https://user-images.githubusercontent.com/123592482/215180802-b08918ea-6131-4fa0-b4d2-3e5701a48061.png">
 
### Data Analysis 
1. 
<img width="587" alt="image" src="https://user-images.githubusercontent.com/123592482/215181074-97858872-e6a1-4004-b226-37380a4d6f1e.png">

2. 
<img width="890" alt="image" src="https://user-images.githubusercontent.com/123592482/215181305-d95887f1-c75f-44b0-aa99-ad10a8a75c9d.png">

3. 
<img width="865" alt="image" src="https://user-images.githubusercontent.com/123592482/215181878-d978f91d-ac59-4bc3-9b3e-7932a9b491bc.png">

4. 
<img width="995" alt="image" src="https://user-images.githubusercontent.com/123592482/215182431-08da3d59-5c8d-4aa3-b686-54720e72c263.png">

## Solutions

## Conclusion
Key findings from the dashboard until the date of knowledge cutoff (2022) show that about 1 percent of the world's population who have been infected with COVID-19 have died, and Europe leads the world with the highest infection death count and infection rate in the world. This information can be used by policymakers and healthcare professionals to make informed decisions about how to respond to the pandemic. We will continue to update the dashboard and case study to reflect the most current data and insights. The goal of this analysis is to help stakeholders understand the spread of the virus and take action to slow its spread and save lives.

## Next Steps 
Based on the data findings vizualized by the Tableau Dashboard, here are 5 solutions that can be proposed to address the COVID-19 pandemic: 
1. Increased Vaccination Efforts in Europe: Europe has the highest death count among the continents, and many countries in Europe have high infection rates. By increasing vaccination efforts in Europe, we can protect the population and potentially reduce the death count.
2. Targeted Testing and Contact Tracing in High-Risk Countries: Cyprus and South Korea have some of the highest infection rates in the world. By targeting testing and contact tracing efforts in these countries, we can identify and isolate infected individuals more effectively, slowing the spread of the virus.
3. Hospital preparedness: Since Europe has high death rate, it's important to ensure that hospitals and health care systems in Europe are prepared to handle the influx of patients. This includes having enough beds, oxygen, and other resources to provide adequate care for those who are critically ill.
4. Public awareness campaigns : Public awareness campaigns can be targeted in Europe, Cyprus and South Korea to educate people about the importance of vaccination, testing, and contact tracing. This can help increase compliance with public health guidelines and slow the spread of the virus.
5. Remote work: Encourage remote work in Europe, Cyprus and South Korea, to reduce the spread of the virus.
