# Data Fabric
*Sep, 2020*
## Data Fabric Architecture
*Defining a data fabric architecture and comparing/contrasting it related approaches*
- Traditionally, data lived in a Database Management System (DBMS) or in an unstructured format (e.g. shared-drive, other filesystems). As time passed, we now have both structured and unstructured data of various formats, located at various end-points.

- Emerging from Data Management, Big Data, and associated Analytics, Data Fabric is a single environment allowing access to the data (you need) via a common toolset/framework irrespective of data location, residency, or format, while providing means to analyze and transform data as it moves between underlying system/data-layer. For an end-user, it is a single system that unifies the accessibility of data from various services, technologies into one platform. Data Fabric Architecture uses the fundamentals of software design and architecture to achieve such an objective.

- Personally, it feels like it's a 1990s grid computing focused on distributed ETL involving a huge amount of heterogeneous data and real-time analytics.

- Alternative approaches to Data Fabric rely on various data-warehousing technologies (pre-processed data for a particular purpose, gathered and flattened for analysis/reporting while providing query languages on top of it). Another alternative is Data Lakes (all data at one place, transformed as needed, used for analytics, various reporting, machine learning, etc.)