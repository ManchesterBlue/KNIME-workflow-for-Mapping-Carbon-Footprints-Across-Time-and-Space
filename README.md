# KNIME Workflow For Mapping Carbon Footprints Across Time And Space
# Abstract
As the world grapples with the unprecedented challenge of climate change, the role of carbon footprints—defined as the total amount of carbon dioxide emissions that are directly and indirectly caused by an activity or accumulated over the life stages of a product—in shaping our environmental future has never been more critical (Wiedmann & Minx, 2008). Each step we take leaves a mark on our planet, shaping the landscape of tomorrow. In this context, understanding the spatial and temporal dynamics of carbon footprints is essential for devising effective environmental policies and strategies. This study aims to harness advanced geospatial analytics to meticulously map carbon emissions over time and across diverse geographies. Utilizing the intuitive data integration capabilities of KNIME, this research endeavors to apply rigorous methods to analyze spatio-temporal carbon data. By melding detailed visualizations with sophisticated data processing, the study seeks to reveal underlying patterns in carbon footprint distribution, thereby enriching our understanding of both global and regional environmental impacts. The expected findings promise to deliver critical insights for policymakers, researchers, and environmental stakeholders, all united in their goal to mitigate the harmful effects of carbon emissions. This research will add a nuanced layer to the ongoing discourse on sustainable practices and proactive climate action.
# Workflow
## Current Version
![image](https://github.com/user-attachments/assets/28ae5c52-c545-4f1c-a9c2-19db014eda68)
## Future Version
<img width="947" alt="412468a150d3109e5e9ca15f5df721f" src="https://github.com/user-attachments/assets/e2f29a6f-266f-477e-8bbb-492bbc353fbc">

# Introduction
The data I use is currently all from this website: Our World in Data. Our World in Data is a unique web resource that presents empirical research and statistics to make international data on important issues both accessible and understandable. It aims to provide a detailed, data-driven overview of the world’s major challenges and developments across various fields such as health, food provision, the environment, poverty, violence, and education. The "CO2 emissions" section focuses on global carbon dioxide emissions, providing a comprehensive look at their sources, intensity, and impact across different regions and timescales. It includes historical data, present-day statistics, and future projections to illustrate how CO2 emissions have changed over time and what this means for climate change.
<img width="1499" alt="image" src="https://github.com/user-attachments/assets/848684a4-7d4f-4c2c-b5ee-5cbe7e20a3d2">

The data table I use now is a patchwork of various carbon emissions data available on the site. This is a very large table with all kinds of data about carbon emissions. Including but not limited to the carbon emission data caused by various fuels, carbon emission data of countries and continents, annual per capita carbon emissions, annual carbon emission increase, cumulative carbon emissions and many other variables.
<img width="1440" alt="image (1)" src="https://github.com/user-attachments/assets/a01da1db-52dd-45fc-a0fa-681559bc9c64">

This is my KNIME workflow. I present the body part, eliminating the duplicate nodes such as generating tables or images. To get different variables in this workflow, you just need to adjust them in configure.
<img width="750" alt="image (2)" src="https://github.com/user-attachments/assets/29ffa13f-6fb9-469a-996d-47a89d86d9f4">

I will briefly introduce these nodes, which is convenient for the whole workflow to have a full understanding. The first is rule-based row splitter. In my entire data table, the packets contain countries and continents, and it even includes Asia excluding China and Indi and North America excluding the United States. It is responsible for differentiating them.
<img width="101" alt="image (3)" src="https://github.com/user-attachments/assets/4f68763c-030d-45a4-8b29-7522c6fa4ba3">
<img width="398" alt="image (4)" src="https://github.com/user-attachments/assets/e8713ac5-3218-45c7-8e19-887f69deab7b">

I currently plot part of the data about continents and map part of the data about countries. Let's first start with the part about continents. It first delimit a time range using Row Filter. The upper and lower bounds here are 2020 and 1950 respectively. But the upper and lower bounds could be adjusted.


Then the Interactive Range Slider Filter will further select within the range you delimit, which can be slid to easily analyze the carbon emissions over a period of time. One might wonder if this is similar to the previous Row Filter. My answer is that the first part of the selection will lead to other branches in my further exploration. This is just for the purpose of drawing the plots, and for the sake of convenience, I will select the time area again.
<img width="93" alt="image (5)" src="https://github.com/user-attachments/assets/9492c7ec-2d3a-44da-84fb-ddcb438898f3">
<img width="484" alt="image (6)" src="https://github.com/user-attachments/assets/17bc0a5b-03b5-4b0e-be9d-b52964a9db45">


The Interactive Value Filter will select the continent from which you want to analyze your data. As shown in the figure, the default continent is Europe.

Finally, we can plot the data for the continent we want to analyze. I have chosen the growth percentage in carbon dioxide. As we can see, there are a lot of options for analysis. We will look at the details of the plot later in the section that presents the results.
