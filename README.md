# BCN Tourist Pressure Analyzer

**In short: a hybrid big data and microservices architecture for urban economic impact analysis.**

## Overview

*Understanding how short-term rentals reshape the economic landscape of modern cities is one of the biggest urban challenges today*
*This project aims to bring data-driven clarity to this issue by focusing on Barcelona's real estate and tourism dynamics*

This project implements a polyglot data pipeline designed to monitor and analyze tourist pressure in Barcelona (Spain). It correlates real-time simulated streams of Airbnb activity with official socio-economic datasets from the Barcelona Open Data portal.

By intersecting tourism volume with local household income, the goal is to understand the relationship between short-term rentals and neighborhood wealth, helping to identify areas at risk of gentrification, price inflation, and economic displacement of residents.

## Features

*This architecture is built to handle both high-throughput streams and complex batch transformations, bridging the gap between raw data and actionable intelligence*

* **Real-time Ingestion:** a producer that simulates high-throughput event streams into Redpanda
* **Stream Processing:** real-time windowed aggregations of tourism activity metrics across different neighborhoods
* **Batch Layer:** data enrichment using official household income datasets to categorize neighborhoods by economic capacity and gentrification risk
* **Serving Layer:** a RESTful API built with **<TBD>** to expose processed insights, making them available for dashboard consumption **<TBD>**
* **Advanced Analytics:** use of Random Forest for price prediction based on property features and neighborhood income, alongside K-Means for spatial clustering

## Stack

*To ensure scalability, performance, and maintainability, this project leverages a modern, cloud-ready tech stack*

* **Languages:** Java 25 and Python 3.11+
* **Backend Framework:** Spring Boot 3.x (with Spring for Apache Kafka)
* **Big Data Engine:** Apache Spark
* **Message Broker:** Redpanda
* **Database:** PostgreSQL and MongoDB
* **Environment:** Docker
* **Reporting:** Data Studio or Tableau (to be decided)

## Architecture

*The system follows a hybrid streaming/batch architecture*
*It separates the ingestion of slow-moving contextual data from the high-speed processing of transactional events*

1.  **Static Layer:** loads `listings.csv` and `socioeconomic_data.csv` into a relational database to build the contextual dimensions
2.  **Streaming Layer:** reads historical `reviews.csv` and `calendar.csv` data, streaming them as simulated real-time events to Redpanda topics with controlled throughput
3.  **Processing Layer:** consumes messages from Redpanda, joins the live stream with the static wealth data in memory, and performs stateful windowed aggregations
4.  **API Layer:** serves the processed results via REST endpoints, allowing frontend applications or BI tools to query the final metrics seamlessly

## Data Sources

*Transparency and open data are at the core of this analysis. All datasets used to feed this pipeline are publicly available, properly licensed, and meticulously cited.*

The datasets used in this project are publicly available and are used under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

* **Inside Airbnb:** Listing, calendar, and review datasets were sourced from [Inside Airbnb](http://insideairbnb.com/get-the-data/).
* **Open Data Barcelona:** Socio-economic datasets ("Renta disponible de los hogares per cápita") were sourced from the [Open Data Portal of the Ajuntament de Barcelona](https://opendata-ajuntament.barcelona.cat/).

*You can read the full text of the license here: [CC BY 4.0 License](https://creativecommons.org/licenses/by/4.0/)*

## License

*Open source is about sharing knowledge and empowering developers. This repository is provided under a permissive license to encourage learning, adaptation, and collaboration.*

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.
