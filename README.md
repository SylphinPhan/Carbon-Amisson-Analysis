# Carbon-Amisson---Analysis
![image](https://github.com/SylphinPhan/Carbon-Amisson---Analysis/blob/main/cover.jpg)

![image](https://github.com/SylphinPhan/Carbon-Amisson---Analysis/blob/main/Database%20diagram.png)


1. Introduction**
---What is the project about?

![image](https://github.com/SylphinPhan/Carbon-Amisson---Analysis/blob/main/cover.jpg)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.

Data Source: Where Our Data Comes From
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).

Data Structure
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.

![image](https://github.com/SylphinPhan/Carbon-Amisson---Analysis/blob/main/Database%20diagram.png)

Tables' columns description
Table 'product_emissions'
id: Identifier for each product emission record.
company_id: Identifier for the company associated with the product.
country_id: Identifier for the country where the product is being produced.
industry_group_id: Identifier for the industry group to which the product belongs.
year: The year in which the emissions data was recorded.
product_name: The name of the product associated with the emissions data.
weight_kg: The weight of the product in kilograms.
carbon_footprint_pcf: The carbon footprint of the product, measured in CO2 equivalent.
upstream_percent_total_pcf: The percentage of the total carbon footprint attributed to upstream activities.
operations_percent_total_pcf: The percentage of the total carbon footprint attributed to operations.
downstream_percent_total_pcf: The percentage of the total carbon footprint attributed to downstream activities.
 

Table 'industry_groups'
id: Unique identifier for each industry group.
industry_group: The name of the industry group, categorizing businesses within similar sectors based on their products or services offered.
 

Table 'companies'
id: Unique identifier for each company.
company_name: The name of the company, identifying the specific organization within the dataset.
 

Table 'countries'
id: Unique identifier for each country.
country_name: The name of the country.
2. Project brief
Q1
```
SELECT product_name, AVG(carbon_footprint_pcf) AS total_emissions
FROM product_emissions
GROUP BY product_name
ORDER BY total_emissions DESC
LIMIT 5;
```

| product_name |avg_emissions  |
| --- | --- |
|Wind Turbine G128 5 Megawats  |3718044 |
|Wind Turbine G132 5 Megawats |3276187 |
|Wind Turbine G114 2 Megawats  |1532608  |
|Wind Turbine G90 2 Megawats  |1251625  |
|Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.  |191687  |

Q2
```
SELECT p.product_name, i.industry_group, AVG(p.carbon_footprint_pcf) AS avg_emissions
FROM product_emissions p
JOIN industry_groups i ON p.industry_group_id = i.id
GROUP BY p.product_name, i.industry_group
ORDER BY avg_emissions DESC
LIMIT 5;

```

| product_name                                                       | industry_group                     | avg_emissions | 
| -----------------------------------------------------------------: | ---------------------------------: | ------------: | 
| Wind Turbine G128 5 Megawats                                       | Electrical Equipment and Machinery | 3718044  | 
| Wind Turbine G132 5 Megawats                                       | Electrical Equipment and Machinery | 3276187 | 
| Wind Turbine G114 2 Megawats                                       | Electrical Equipment and Machinery | 1532608| 
| Wind Turbine G90 2 Megawats                                        | Electrical Equipment and Machinery | 1251625 | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit. | Automobiles & Components           | 191687 | 

Q3
```
SELECT i.industry_group, AVG(p.carbon_footprint_pcf) AS total_emissions
FROM product_emissions p
JOIN industry_groups i ON p.industry_group_id = i.id
GROUP BY i.industry_group
ORDER BY AVG_emissions DESC
LIMIT 10;
```
| industry_group                                   | total_emissions | 
| -----------------------------------------------: | --------------: | 
| Electrical Equipment and Machinery               | 891050.7273     | 
| Automobiles & Components                         | 35373.4795      | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 24162.0000      | 
| Capital Goods                                    | 7391.7714       | 
| Materials                                        | 3208.8611       | 
| "Mining - Iron, Aluminum, Other Metals"          | 2727.0000       | 
| Energy                                           | 2154.8000       | 
| Chemicals                                        | 1949.0313       | 
| Media                                            | 1534.4667       | 
| Software & Services                              | 1368.9412       | 

Q4
```
SELECT c.company_name, avg(p.carbon_footprint_pcf) AS total_emissions
FROM product_emissions p
JOIN companies c ON p.company_id = c.id
GROUP BY c.company_name
ORDER BY total_emissions DESC
LIMIT 10;
```
| company_name                           | total_emissions | 
| -------------------------------------: | --------------: | 
| "Gamesa Corporación Tecnológica, S.A." | 2444616.0000    | 
| "Hino Motors, Ltd."                    | 191687.0000     | 
| Arcelor Mittal                         | 83503.5000      | 
| Weg S/A                                | 53551.6667      | 
| Daimler AG                             | 43089.1892      | 
| General Motors Company                 | 34251.7500      | 
| Volkswagen AG                          | 26238.4000      | 
| Waters Corporation                     | 24162.0000      | 
| "Daikin Industries, Ltd."              | 17600.0000      | 
| CJ Cheiljedang                         | 15802.8333      | 

Q5
```
SELECT co.country_name, SUM(p.carbon_footprint_pcf) AS total_emissions
FROM product_emissions p
JOIN countries co ON p.country_id = co.id
GROUP BY co.country_name
ORDER BY total_emissions DESC
LIMIT 10;
```

| country_name | total_emissions | 
| -----------: | --------------: | 
| Spain        | 9786130         | 
| Germany      | 2251225         | 
| Japan        | 653237          | 
| USA          | 518381          | 
| South Korea  | 186965          | 
| Brazil       | 169337          | 
| Luxembourg   | 167007          | 
| Netherlands  | 70417           | 
| Taiwan       | 62875           | 
| India        | 24574           | 

Q6
```
SELECT year, SUM(carbon_footprint_pcf) AS total_emissions
FROM product_emissions
GROUP BY year
ORDER BY year;
```

| year | total_emissions | 
| ---: | --------------: | 
| 2013 | 503857          | 
| 2014 | 624226          | 
| 2015 | 10840415        | 
| 2016 | 1640182         | 
| 2017 | 340271          | 

Q7

```
SELECT p.year,
i.industry_group,
ROUND(AVG(carbon_footprint_pcf),2) AS pcf
FROM product_emissions p
JOIN industry_groups i
ON i.id = p.industry_group_id
GROUP BY 1,2
ORDER BY industry_group,year,pcf DESC
```



```
