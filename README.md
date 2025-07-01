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
| year | industry_group                                                         | pcf       | 
| ---: | ---------------------------------------------------------------------: | --------: | 
| 2015 | "Consumer Durables, Household and Personal Products"                   | 116.38    | 
| 2013 | "Food, Beverage & Tobacco"                                             | 94.25     | 
| 2014 | "Food, Beverage & Tobacco"                                             | 99.44     | 
| 2015 | "Food, Beverage & Tobacco"                                             | 0.00      | 
| 2016 | "Food, Beverage & Tobacco"                                             | 4011.56   | 
| 2017 | "Food, Beverage & Tobacco"                                             | 143.73    | 
| 2015 | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 685.31    | 
| 2015 | "Mining - Iron, Aluminum, Other Metals"                                | 2727.00   | 
| 2013 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 16135.50  | 
| 2014 | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 40215.00  | 
| 2015 | "Textiles, Apparel, Footwear and Luxury Goods"                         | 14.33     | 
| 2013 | Automobiles & Components                                               | 26037.80  | 
| 2014 | Automobiles & Components                                               | 20910.45  | 
| 2015 | Automobiles & Components                                               | 37146.68  | 
| 2016 | Automobiles & Components                                               | 40138.09  | 
| 2013 | Capital Goods                                                          | 5015.83   | 
| 2014 | Capital Goods                                                          | 10411.00  | 
| 2015 | Capital Goods                                                          | 3505.00   | 
| 2016 | Capital Goods                                                          | 796.13    | 
| 2017 | Capital Goods                                                          | 18989.80  | 
| 2015 | Chemicals                                                              | 1949.03   | 
| 2013 | Commercial & Professional Services                                     | 144.63    | 
| 2014 | Commercial & Professional Services                                     | 119.25    | 
| 2016 | Commercial & Professional Services                                     | 96.33     | 
| 2017 | Commercial & Professional Services                                     | 370.50    | 
| 2013 | Consumer Durables & Apparel                                            | 286.70    | 
| 2014 | Consumer Durables & Apparel                                            | 113.10    | 
| 2016 | Consumer Durables & Apparel                                            | 40.07     | 
| 2015 | Containers & Packaging                                                 | 373.50    | 
| 2015 | Electrical Equipment and Machinery                                     | 891050.73 | 
| 2013 | Energy                                                                 | 750.00    | 
| 2016 | Energy                                                                 | 2506.00   | 
| 2015 | Food & Beverage Processing                                             | 7.05      | 
| 2014 | Food & Staples Retailing                                               | 77.30     | 
| 2015 | Food & Staples Retailing                                               | 70.60     | 
| 2016 | Food & Staples Retailing                                               | 0.50      | 
| 2015 | Gas Utilities                                                          | 61.00     | 
| 2013 | Household & Personal Products                                          | 0.00      | 
| 2013 | Materials                                                              | 4177.35   | 
| 2014 | Materials                                                              | 1513.56   | 
| 2016 | Materials                                                              | 1401.06   | 
| 2017 | Materials                                                              | 11217.74  | 
| 2013 | Media                                                                  | 2411.25   | 
| 2014 | Media                                                                  | 2411.25   | 
| 2015 | Media                                                                  | 479.75    | 
| 2016 | Media                                                                  | 602.67    | 
| 2014 | Retailing                                                              | 6.33      | 
| 2015 | Retailing                                                              | 5.50      | 
| 2014 | Semiconductors & Semiconductor Equipment                               | 16.67     | 
| 2016 | Semiconductors & Semiconductor Equipment                               | 2.00      | 
| 2015 | Semiconductors & Semiconductors Equipment                              | 1.00      | 
| 2013 | Software & Services                                                    | 1.50      | 
| 2014 | Software & Services                                                    | 29.20     | 
| 2015 | Software & Services                                                    | 1523.73   | 
| 2016 | Software & Services                                                    | 2538.44   | 
| 2017 | Software & Services                                                    | 690.00    | 
| 2013 | Technology Hardware & Equipment                                        | 1053.45   | 
| 2014 | Technology Hardware & Equipment                                        | 1780.44   | 
| 2015 | Technology Hardware & Equipment                                        | 1895.66   | 
| 2016 | Technology Hardware & Equipment                                        | 65.25     | 
| 2017 | Technology Hardware & Equipment                                        | 788.34    | 
| 2013 | Telecommunication Services                                             | 52.00     | 
| 2014 | Telecommunication Services                                             | 45.75     | 
| 2015 | Telecommunication Services                                             | 45.75     | 
| 2015 | Tires                                                                  | 1011.00   | 
| 2015 | Tobacco                                                                | 1.00      | 
| 2015 | Trading Companies & Distributors and Commercial Services & Supplies    | 39.83     | 
| 2013 | Utilities                                                              | 61.00     | 
| 2016 | Utilities                                                              | 61.00     | 


```
