# KNIME Workflow For Mapping Carbon Footprints Across Time And Space
# Abstract
As the world grapples with the unprecedented challenge of climate change, the role of carbon footprints—defined as the total amount of carbon dioxide emissions that are directly and indirectly caused by an activity or accumulated over the life stages of a product—in shaping our environmental future has never been more critical (Wiedmann & Minx, 2008). Each step we take leaves a mark on our planet, shaping the landscape of tomorrow. In this context, understanding the spatial and temporal dynamics of carbon footprints is essential for devising effective environmental policies and strategies. This study aims to harness advanced geospatial analytics to meticulously map carbon emissions over time and across diverse geographies. Utilizing the intuitive data integration capabilities of KNIME, this research endeavors to apply rigorous methods to analyze spatio-temporal carbon data. By melding detailed visualizations with sophisticated data processing, the study seeks to reveal underlying patterns in carbon footprint distribution, thereby enriching our understanding of both global and regional environmental impacts. The expected findings promise to deliver critical insights for policymakers, researchers, and environmental stakeholders, all united in their goal to mitigate the harmful effects of carbon emissions. This research will add a nuanced layer to the ongoing discourse on sustainable practices and proactive climate action.
# Workflow
The current workflow is mainly composed of the following parts: First, the Access the Data part. **CSV Reader** is responsible for reading CSV Data. Here I use the Data provided by _Our World in Data_, which includes various indicators of carbon emissions. I concatenate the data into CSV Reader. Then there's the Data Range Selection part. Since the data table contains data of both continents and countries, I first used a **Rule-based Row Splitter** to split the data into continents and countries. Here, I use two different perspectives to observe carbon emission data of continents and carbon emission data of countries. In the former, I take a period of time as the standard to explore the carbon emission situation of a single continent during such years, expressed in the form of plot. In the latter, I take a certain year as the standard to explore the carbon emission situation of all countries and regions in the world in this year, expressed in the form of choroplethic map. If we were looking at carbon emissions across continents, **Interactive Range Slider Filter Widget** can go a step further to provide an interactive interface that allows end-users to dynamically select a time range on the frontend. **Interactive Value Filter Widget** can select a specific one from each continent. After determining the time range and specific continents studied, we can use **Line Plot** to plot the change plot of carbon emissions. If we are looking at the carbon emissions of each country in the world, we can draw a global carbon emission table based on a certain carbon emission index. The details will be demonstrated in the following Introduction section.
A screenshot of the workflow is shown below.

![image](https://github.com/user-attachments/assets/28ae5c52-c545-4f1c-a9c2-19db014eda68)

# Introduction
The data I use is currently all from this website: **_Our World in Data_**. Our World in Data is a unique web resource that presents empirical research and statistics to make international data on important issues both accessible and understandable. It aims to provide a detailed, data-driven overview of the world’s major challenges and developments across various fields such as health, food provision, the environment, poverty, violence, and education. The "CO<sub>2</sub> emissions" section focuses on global carbon dioxide emissions, providing a comprehensive look at their sources, intensity, and impact across different regions and timescales. It includes historical data, present-day statistics, and future projections to illustrate how CO<sub>2</sub> emissions have changed over time and what this means for climate change.
Official website: [https://ourworldindata.org/co2-emissions](CO<sub>2</sub> emissions)
The main interface of the offcial website is shown below.

<img width="1499" alt="image" src="https://github.com/user-attachments/assets/848684a4-7d4f-4c2c-b5ee-5cbe7e20a3d2">

The data table I use now is a patchwork of various carbon emissions data available on the site. This is a very large table with all kinds of data about carbon emissions. Including but not limited to the carbon emission data caused by various fuels, carbon emission data of countries and continents, annual per capita carbon emissions, annual carbon emission increase, cumulative carbon emissions and many other variables.

<img width="1440" alt="image (1)" src="https://github.com/user-attachments/assets/a01da1db-52dd-45fc-a0fa-681559bc9c64">

I will briefly introduce these nodes, which is convenient for the whole workflow to have a full understanding. The first is rule-based row splitter. In my entire data table, the packets contain countries and continents, and it even includes Asia excluding China and Indi and North America excluding the United States. It is responsible for differentiating them.

<img width="101" alt="image (3)" src="https://github.com/user-attachments/assets/4f68763c-030d-45a4-8b29-7522c6fa4ba3">

<img width="398" alt="image (4)" src="https://github.com/user-attachments/assets/e8713ac5-3218-45c7-8e19-887f69deab7b">

I currently plot part of the data about continents and map part of the data about countries. Let's first start with the part about continents. It first delimit a time range using Row Filter. The upper and lower bounds here are 2020 and 1950 respectively. But the upper and lower bounds could be adjusted.

<img width="93" alt="image (5)" src="https://github.com/user-attachments/assets/9492c7ec-2d3a-44da-84fb-ddcb438898f3">

<img width="484" alt="image (6)" src="https://github.com/user-attachments/assets/17bc0a5b-03b5-4b0e-be9d-b52964a9db45">

Then the Interactive Range Slider Filter will further select within the range you delimit, which can be slid to easily analyze the carbon emissions over a period of time. One might wonder if this is similar to the previous Row Filter. My answer is that the first part of the selection will lead to other branches in my further exploration. This is just for the purpose of drawing the plots, and for the sake of convenience, I will select the time area again.

<img width="100" alt="image (7)" src="https://github.com/user-attachments/assets/8428985a-b51d-4b2d-aa56-606831557f82">

<img width="756" alt="image (8)" src="https://github.com/user-attachments/assets/2ad3c38c-f7a0-436a-a3ad-1b924238cdd3">

The Interactive Value Filter will select the continent from which you want to analyze your data. As shown in the figure, the default continent is Europe.

<img width="326" alt="image (9)" src="https://github.com/user-attachments/assets/3f393a49-15b4-4053-bb18-1fb74deb40d8">

<img width="569" alt="image (10)" src="https://github.com/user-attachments/assets/13443480-7a84-432e-a7e8-069079c987c1">

Finally, we can plot the data for the continent we want to analyze. I have chosen the growth percentage in carbon dioxide. As we can see, there are a lot of options for analysis. We will look at the details of the plot later in the section that presents the results.

<img width="254" alt="image (11)" src="https://github.com/user-attachments/assets/1870c64d-b037-4e3c-8ca2-42bec3bd11a0">

<img width="545" alt="image (12)" src="https://github.com/user-attachments/assets/d05938f0-6539-47d4-9eab-910a1008a01d">

Instead of looking at continental changes in carbon emissions, the alternative is to look at global emissions in a particular year. When I first tried to use the geospatial extensions, I either could not generate images or the images I generated were unsatisfactory. Eventually I found that the Choropleth Map Node seemed to fit the bill. Here we first use Row Fliter to select a particular year. Take 2019 here, the eve of covid-19.

<img width="209" alt="image (13)" src="https://github.com/user-attachments/assets/f98e527f-0a08-4230-8c8a-9e9b9269cd42">

<img width="484" alt="image (14)" src="https://github.com/user-attachments/assets/c021e453-206a-4448-b3b4-620f5c927802">

This is the Choropleth Map Node that finally draws the map. It can draw a map through a column that we select. Such a map is more clear and intuitive, which can facilitate us to directly judge the overall trend and make a clear comparison.

<img width="243" alt="image (15)" src="https://github.com/user-attachments/assets/f5861e2f-3ec5-42b9-933a-e7ccf00f7c21">

<img width="377" alt="image (16)" src="https://github.com/user-attachments/assets/65da02e7-fb34-4942-9e39-d44aeed435eb">

# Examples
Now I'm going to show you a little bit of that. Since there are many tables and maps that can be drawn as a whole, I will only select a few pictures to ment`ion a little. The first is this plot. we analyze the growth in percentage of carbon emissions in Europe as a whole. This chart vividly illustrates the fluctuations in annual growth rates of carbon emissions across Europe from 1950 to the present. As we observe, there was a significant peak in 1950, suggesting a high point in carbon emissions growth. Following this, the trend generally appears to decline, though the decrease is not markedly steep. It seems that a pivotal event or series of events in the 1950s might have catalyzed a sharp drop in emissions growth, after which the levels largely stabilized, like industrial restructuring, energy efficiency and techn
ological innovations, introduction of nuclear power, and economic shifts especially the Marshall Plan beginning in 1948. The vertical lines and points on the graph represent the variability in annual rates, indicating that despite the long-term trend of decline, there were substantial fluctuations year over year. This could be attributed to varying factors such as shifts in environmental policies, economic activities, or energy consumption patterns. Remarkably, in recent years, the growth rates have even dipped into the negative, signifying that the annual carbon emissions are decreasing compared to previous years. This graph not only showcases the historical changes but also underscores the ongoing efforts and their impact on reducing carbon footprints in Europe.

<img width="756" alt="image (18)" src="https://github.com/user-attachments/assets/ef227f17-3cb5-497d-9622-2d99fff17b38">

This graph reflects the results of global per capita carbon emissions in 2019. As you can see, the per capita carbon emissions of the most populous countries, China and India, are not very high. The United States, Saudi Arabia, and Australia are the largest carbon emitters per capita. Despite their smaller populations, these countries have significantly higher emissions due to factors such as higher energy consumption per capita and greater reliance on fossil fuels. This stark contrast underscores the differences in energy use and emissions management strategies across nations. The data highlight the need for tailored policies that reflect the unique economic, industrial, and environmental contexts of each country to effectively address global carbon challenges.

<img width="756" alt="image (17)" src="https://github.com/user-attachments/assets/527961ad-2656-41a9-bbf8-b88436055d44">

This map illustrates the variation in cumulative carbon emissions per capita across the globe, as of 2019. The intensity of the colors represents the range from the lowest to the highest emissions, highlighting the stark disparities between different regions. Nations like Canada, the United States, and Australia show significantly higher cumulative emissions per capita, as depicted in darker hues, reflecting their historical industrial activities and higher levels of energy consumption from fossil fuels. In contrast, countries in Africa and parts of Asia, marked in lighter colors, exhibit much lower cumulative emissions. This discrepancy underscores not only the varied stages of industrial development but also the differences in energy sources and consumption patterns across countries. Such a visual representation helps identify both the leading contributors to global carbon emissions and those nations that, while rapidly developing, still maintain lower emission levels, offering insights into the global effort to manage and reduce carbon footprints effectively.

<img width="756" alt="image (19)" src="https://github.com/user-attachments/assets/976de4b9-636d-4b06-b83e-aff5201ad2bf">

This map displays the concentration of computing power across different countries as measured by data centers and computing resources available as of 2019. The scale of the map, ranging from 0 to over 14,684 units, shows a pronounced concentration in China, highlighted in deep purple, indicating a significant dominance in computing infrastructure. This is contrasted starkly by the lighter hues observed in regions like North America, Europe, and parts of Asia, which, although substantial in their computing capacities, do not match the scale found in China. The palest colors across Africa and parts of South America reflect minimal computing resources, underscoring global disparities in technological infrastructure. This geographical distribution is pivotal for understanding the global landscape of technology and innovation, where computing power is a crucial asset for economic development, digital innovation, and competitive advantage in the global market.

<img width="756" alt="image (20)" src="https://github.com/user-attachments/assets/b2196eb9-cfa9-4e40-994c-08a69212b820">
