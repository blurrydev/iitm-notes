# Data Core Concepts

### Part 1
- **Data:** Units of information.
- **Data Documents:** Types of abstract groupings of data.
- **Data Sets:** Unstructured logical grouping of data
- **Data Structures:** 
	- **Unstructured:** A bunch of loose data that has no organization or possible relations. E.g.: Flat files.
	- **Semi structured data:** Data that can be browsed or searched with limitations.
		- XML: A markup language that looks like HTML
		- JSON: A text file that is composed of dictionaries and arrays.
		- RCFiles: A storage format designed for MapReduce framework
		- ORC: A columnar data structure, 75% more efficient than RCFiles.
		- AVRO: A row-wise data structure for Hadoop systems
		- Parquet: A columnar data structure that has more support for Hadoop system than ORC.
	- **Structured:** A data that can be easily browsed and searched.
- **Data Types:** How single units of data is intended to be used.
- **Database Administrator:** *Configures and maintains database*
- **Data Engineer:** *Design and implement data tasks* related to transfer and storage of big data.
- **Data Analyst:** *Analyzes business data* to reveal important insights.
- **Software as a Service (SaaS):** *For Consumers* A product that is run and managed by the service provider.
- **Platform as a Service (PaaS):** *For Developers* Focus on deployment and management of your apps.
- **Infrastructure as a Service (IaaS):** *For Admins* Basic building blocks for cloud IT. Provides access to networking, computers and data storage space.

### Part 2
- **Datastores:** Unstructured or semi-structured data for housing data. This can encompass anything that stores data.
- **Databases:** Structured data that can be quickly accessed and searched (*row based, tabular data for OLTP*.
- **Data warehouses:** Structured or semi-structured data for creating reports and analytics (*Column based*).
- **Data marts:** A subset of data warehouse for specific business data task.
- **Data lakes:** Stores unstructured or semi-structured data.
- **Notebooks:** Data arranged in pages. Customized for easy consumption.
- **Batching:** When you send batches of data to be processed. *Not real-time*
- **Streaming:** When data is processed as soon as it arrives. *Real time*
- **Relational data:** Data that uses structured tabular data and has relationships between tables.
	- **One-to-one:** One person has one passport.
	- **One-to-Many:** One teacher teaches many student.
	- **Many-to-Many:** A user can belong to multiple community and a community can have multiple users.
- **Row-store:** Data organized into rows, optimized for OLTP.
- **Column-store:** Data organized into columns, optimized for OLAP.
- **Indexes:** Data structures that improves read time of database.
- **Pivot Table:** It is a table of statistics that summarizes the data of a more extensible table from a database or spreadsheet or BI tool.
- **Non-relational data:** Data that is semi structured, associated with schemeless and NoSQL databases.
	- **Key value:** Each value has a key, designed to scale, only simple lookups.
	- **Document:** Primary entity is a XML or JSON like data structure called document.
	- **Graph:** Data is represented with nodes and structures. Where relationships matter.

### Part 3
- **Data Modeling:** An abstract model that organizes elements of data and standardizes how they relate to one another and to real-world entities.
- **Schema:** A formal language that describes the structure of data used by the database and data stores during data modeling phase.
- **Schemaless:** Generally used when upfront data modelling can forgo because the schema is flexible. Normally used in NoSQL databases.
- **Data Integrity:** The maintenance and assurance of data accuracy and consistency over it's entire life cycle.
- **Data Corruption:** The act or state of data not being in the intended state and will result in data loss and misinformation.
- **Normalized:** A schema design to store non redundant and consistent data.
- **Denormalized:** A schema design that combines such that accessing data is fast.
- **Extract, Transform and Load (ETL):** Transform data from one data store to another. Loads data in an intermediate stage. *Does not work with data lake.* 
- **Extract Load and Transform (ELT):** Transformations done at the target data store, works with data lakes, more common in cloud services.
- **Query:** When user request data from data store using query language to return data result.
- **Data Source:** A data source is where data originates from. Analytics and data warehouses tools maybe connected to various data sources.
- **Data Consistency:** When data being kept at two different places and whether data matches exactly.
	- **Strongly Consistent:** Every time you request data, you can expect consistent data to be returned within the time.
	- **Eventually Consistent:** When you request data you may get back inconsistent data. (*Stale data*).
- **Synchronization:** Continuous stream of data that is synchronized by a timer or clock *(guarantee of time)*.
- **Asynchronization:** Continuous stream of data separated start and stop bits (*no guarantee of time*).
- **Data Mining:** The extraction of pattern and knowledge from large amounts of data. *But not extraction of data itself*.
- **Data Wrangling:** The process of transforming and mapping data from  *raw* format into another format.

- **Data Analysis:** Data analysis is *examining, transforming and arranging data* so that you can extract and study useful information.
- **Key Performance Indicators:** Type of performance measurement that a company or organization use to determine the performance over time.

##### Important
- **Descriptive Analytics:** *(What happened?)* - Describe what happened using accurate, comprehensive, live-data and effective visualization to find out what happened in the data.
- **Diagnostic Analytics:** *(Why it happened)* - Drill down to investigate the root cause, focused on the subset of descriptive analytics dataset. Isolates the anomalies into it's own dataset and applies statistical techniques.
- **Predictive Analytics:** *(What will happen)* - Use historical data with statistics and ML to predict future trends and predictions.
- **Prescriptive Analytics:** *(How can we make it happen)* - Goes one step beyond *Predictive analytics* and uses ML to ingest hybrid data to predict future scenarios that are exploitable.
- **Cognitive Analysis:** *(What if this happens)* - Using analytics to draw pattern and create *what if* scenarios and *what actions can be taken* if those scenarios become reality.

- **One Drive:** Storage and storage synchronization service for single user.
- **SharePoint:** Storage and storage synchronization service for an organization.

# Azure Synapse & Data lake Cheatsheet

- **Data Lake:** A data lake is a *centralized data repository for unstructured and semi structured data.*
	- It is intended to store vast amount of data.
	- Data Lakes generally use *blobs* or *files* as it's storage medium.
- **Azure Data Lake store (gen 2):** It is Azure blob storage which has been extended to support big data analytics workloads.

	> In order to efficiently access data, Data lake store adds a *hierarchical namespace* to Azure Blob storage.

	- **Hierarchical Namespace gives access to:**
		- Access Control List
		- Throttling and timeout management
		- Performance Optimizations

	- Data lake can be accessed via:
		- Blob endpoint for Blobs: Object Store Driver
		- DFS endpoint for Files: File System Driver

- **Azure Synapse Analytics:** It is a *Data warehouse* and *Unified analytics platform*.
	- It has *two* underlying transformation engines:
		1. SQL Pool
		2. Spark Pool
	- Synapse SQL is a T-SQL but designed to be distributed.
		- SQL dedicated pools: Reserves compute for processing
		- Serverless Endpoints: On demand, no guarantee of performance.
	- *Data is stored* on Azure Data Lake Store (Gen 2)
	- *Operations are performed* within Azure Synapse Studio
	- **Polybase:** Enables your SQL server instance to query data with T-SQL from many relational data sources.

# Account Storage Cheatsheet

- **Azure Storage accounts:** An umbrella service for various forms  of managed storage.
	- Azure Tables
	- Azure Blob storage
	- Azure Files
- **Azure Blob Storage:** Object storage that is distributed across many machines.
	- Supports 3 types:
		1. **Blob blobs:** Store text and binary data. Can be managed individually. Up-to 4.7 TB.
		2. **Append blobs:** Optimized for append operations. Useful or logging.
		3. **Page blobs:** Store random access files up-to 8 TB in size.
- **Azure Files:** Fully managed shared files in the cloud.
	- To connect to the file share a network protocol is used:
		1. **SMB:** Server Message block
		2. **NFS:** Network File System
- **Azure Storage Explorer:** A standalone cross-platform app to access various storage formats within Azure Storage accounts.

# Power BI Cheatsheet

- **Business Intelligence:** Helps an organization take informed business decision using data analytics and technology.
- **Power BI desktop:** Used to create interactive reports which can be published to Power BI Service.
- **Power BI Service:** Used to view report, create interactive dashboard.
- **Power BI Mobile:** View Power BI reports and dashboards. 
- **Power BI Report Builder:** Windows application to build pixel perfect printable reports.
- **Power BI Embedded:** Embed power visualizations into web app.
- **Interactive Reports:** Reports in Power BI, drag visualization, loads data from various sources (both desktop and services).
- **Paginated Reports:** Pixel perfect printable report file format, Tabular data laid out in page format.

# Relational Databases Cheatsheet

- **SQL:** Designed to access and maintain databases for RDBMS.
- **OLTP:** Frequent and short queries for transactional information.
- **OLAP:** Complex queries for large databases to create reports and analytics.
- **Read replicas:** A duplicate of your database kept in sync with the main database to reduce read operations on the main database..
- **Azure SQL:** An umbrella service for different offerings of MS SQL databases hosting services.
	- **SQL VM:** For lift and shift when you need OS level access control. 
	- **Managed SQL:** For lift and shift when you want the broadest amount of compatibility with SQL versions. Can be used with Azure Arc to run on premise. Gives you many of the benefits of the fully managed databases.
	- **SQL Database:** Fully managed SQL database.
		- Runs a single server.
		- Runs as a database (collection of servers)
		- runs in Elastic pool (Database of different sizes residing on one server to save costs.) 
- **Connection Policy:** There are three modes
	1. Default: Choose Proxy or Redirect initially depending on if the server is within the Azure network or outside the Azure network.
	2. Proxy: *Outside the Azure network* proxied through a gateway.
	> Listen on port 1443

	3. Redirect; redirect to Azure network.

# T-SQL Cheatsheet

- **DDL:** Used to define a language schema.
	- CREATE
	- RENAME
	- ALTER
	- DROP
	- TRUNCATE
	- COMMENT

- **DML:** Used to manipulate data in the database.
	- INSERT
	- UPDATE
	- DELETE
	- MERGE - UPSERT
	- CALL
	- LOCK TABLE

# Database Security Cheatsheet

- **MS SQL Database Authentication:** There are two ways.
	1. *Windows Authentication Mode:* Enables windows authentication and disables SQL server authentication.
	2. *Mixed Mode:* Enables both windows authentication and SQL server authentication.
- **Network Connectivity:** 
	- **Public Endpoint:** Reachable outside Azure network over the internet. Uses firewall for protection, all connections are rejected by default.
	- **Private Endpoint:** Only reachable within the Azure network. Uses Azure private links to keep traffic within Azure Network.
- **Azure Defender SQL:** A unified package for advanced SQL security capabilities for vulnerability assessment and advanced threat protection.
- **Always Encrypted:** A feature that encrypts column in an Azure SQL database or SQL server.
##### Role based access control (RBAC) for databases:
- **SQL Database Contributor:** Can manage SQL databases. Can't access them, can't manage their security related policies or their parent SQL server.
- **SQL Managed Instance Contributor:** Can manage SQL managed instances and it's required network configuration. Can't give access to others.
- **SQL Security Manager:** Can manage security related policies of SQL servers and databases. Can't access the SQL server.
- **SQL Server Contributor:** Can manage SQL server and databases. Can't access the SQL server.
- **Transparent Data Encryption:** Encrypts data-at-rest for Microsoft Databases.
- **Dynamic Data Masking:** You can choose a database column that will be masked for specific users.

# Azure Tables and CosmosDB Cheatsheet

- **Azure Tables:** A key value store.
	- Can be hosted on a single storage which is designed for a single region and single table.
	- Can be hosted on CosmosDB which is designed to scale across multiple regions.
- **CosmosDB:** A fully managed NoSQL service that supports multiple NoSQL engines called APIs.
	- **Core SQL API** *(default)* - A document database which can be used to query documents.
	- **Graph API** - A graph database, uses gremlin to traverse edges and nodes.
	- **MongoDB API** - MongoDB database, document database.
	- **Tables API** - Azure tables key/value

# Hadoop Cheatsheet

- **Apache Hadoop:** Open-Source framework for *distributed processing of large datasets*.
	- **Hadoop Distributed File System (HDFS):** A resilient and redundant file storage distributed on clusters of common hardware.
	- **Hadoop mapReduce:** Writes apps that can process multi-terabyte data in parallel on large clusters of common hardware.
	- **Hbase:** A distributed, scalable, big data store.
	- **YARN:** Manages resources, nodes, containers and performs scheduling.
	- **HIVE:** Used for generating reports using SQL language.
	- **PIG:** A high level scripting language used for complex data transformation.
- **Apache Spark:** Can perform 100x faster in memory and 10x faster in disk than Hadoop. Supports ELT, streaming and ML work flows.
- **Apache Kafka:** Steaming pipeline and analytical service.
- **HDInsight:** It is a fully managed Hadoop system.

# Apache Spark & Databricks Cheatsheet

- **Apache Spark:** An open-source *unified analytical engine* for big data and ML.
	- 100x faster in memory than Hadoop
	- 10x faster in disk than Hadoop
	- perform ELT (batch), streaming and ML workloads.
	- The Apache Spark ecosystem is composed of;
		- **Spark Core:** The underlying engine and API.
		- **Spark SQL:** Use SQL and also new data structure called Dataframe to work with data.
		- **Spark Streaming:** Ingest data from many streaming services.
		- **GraphX:** Distributed graph processing framework.
		- **Machine Learning Library (MLib):** A distributed machine learning framework.
	- **Resilient Distributed Dataset (RDD):** A domain specific language used to execute parallel operations on an Apache Spark Cluster.
- **Databricks:** A software company which provides fully managed Apache Spark Clusters.
- **Azure Databricks offers two environments:**
	1. **Azure Databricks Workspace:** Used for building data pipelines from Azure data related services.
	2. **Azure Databricks SQL Analytics:** Run query on data lake.

# ELT and SQL Tools Cheatsheet

- **Azure Data Factory:** Fully managed service for ELT, ETL and data integration.
	- Create data driven workflows by *orchestrating* data movement and *transforming data* at a scale.
	- Build ELT pipeline visually without writing any code via web interface.
- **SQL Server Integration Services (SSIS):** A platform for building enterprise level data integration and data transformation solutions.
	- A low code tool for building ELT pipelines, similar to Azure Data Factory but existed 15 years prior.
	- Integrates with Azure Data Factory.
- **Azure Data Studio:** An IDE similar to VS Code that is cross platform and woks with SQL and non relational data. Has many extensions.
- **SQL Server Management Studio (SSMS):** An IDE for managing any SQL infrastructure that only work with windows. More Mature than data studio.
- **SQL Server Data Tools (SSDT):** Visual Studio extension to work and design SQL databases visually.