# GlobalSuicideRates
Understanding mental health and global suicide rates
 

## Table of Contents
1.[Introduction](#introduction)

2.[Getting Started](#getting-started)

3.[Features](#features)

4.[Data](#data)

5.[Analysis](#analysis)

6.[Results](#results) 

7.[Recommendations](#recommendations)

##  Introduction
Welcome to the Crude Suicide Rates Project, the cleaning,sorting and analysis were performed on SQL and visualization done on Tableau

## Getting Started 
As a healthcare data analyst, the suicide rates for different countries were retrived from the World Health Organization website with the sole aim of comparing the different rates in various countries and according to age groups and visualizing for proper information.

## Features
Some key features include:

--**Average Crude Suicide Rate by country**

--**Top 10 countries with the Highest Average Crude Suicide rates**

--**Total number of countries in the dataset**

--**Comparison of the Crude Suicide Rates of various countries according to age group**.

--**Percentage Distribution of Suicides by Sex within Each Age Group**

## Data
Data was downloaded from the World Health Organization website as a csv file containing 549 rows and 4 columns containing the Countries,Sex,Age groups(15-29) and (30-49).



**Data Analysis**

use whoproject;

-- Average Crude Suicide Rates(CSR) for each Country

```select Countries,
AVG(`CSR(2019)15-29`) AS AVG_CSR_15_29,
AVG(`CSR(2019) 30-49`) AS AVG_CSR_30_49
FROM sdgsuicide
GROUP BY
Countries;
```

-- Top 5 Countries with the Highest Average CSR(15-29)

```select 
	Countries,
    AVG(`csr(2019)15-29`) as avg_csr_15_29
from
	sdgsuicide
group by 
	Countries
order by
	avg_csr_15_29 desc
LIMIT 10
```

-- Comparison of CSR between Age groups for a Specific Country

```SELECT 
	Countries,
    `csr(2019)15-29` as csr_15_29,
    `csr(2019) 30-49` as csr_30_49
FROM 
	sdgsuicide
WHERE
	Countries = 'Guyana'
```

-- Percentage Distribution of Suicides by Sex within Each Age Group

```SELECT
    Countries,
    sex,
    (SUM(`csr(2019)15-29`) / (SUM(`csr(2019)15-29`) + SUM(`csr(2019) 30-49`))) * 100 AS percentage_15_29,
    (SUM(`csr(2019) 30-49`) / (SUM(`csr(2019)15-29`) + SUM(`csr(2019) 30-49`))) * 100 AS percentage_30_49
FROM
    sdgsuicide
GROUP BY
    Countries, sex;
```

## Results

After analysis,it was discovered that the Top 5 countries with the highest suicide rates in the age group(15-29) were Guyana, Kiribati, Micronesia (Federated States of), Lesotho, Vanuatu while the Top 5 countries with the highest suicide rates in the age group (30-49) were Lesotho, Eswatini, Guyana, South Africa, Kiribati.

Guyana and Lesotho appeared in both age groups

Comparing the CSR rate by age groups for specific countries were also carried out, the result shown here will be specifically for Guyana,there's a very slight difference in the rates for the different age groups: 58.2,	55.2 for 15-29years and 30-49years age groups respectively.

The percentage distributiion of suicides by sex within each age group was calculated.


## Recommendations

The mental health status of the top countries with the highest suicide rates needs to be researched on and compared to the situation with the countries with the lowest to observe changes and how to decrease the suicide rates. Lesotho and Guyana need more attention as all age groups seem to be committing suicide at almost an equal rate.



