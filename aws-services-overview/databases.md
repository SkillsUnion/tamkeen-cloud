# Databases

## Amazon Aurora

### Overview
Amazon Aurora is a MySQL and PostgreSQL-compatible relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases.

### Key Features
- Up to five times faster than standard MySQL databases and three times faster than standard PostgreSQL databases.
- Fully managed by Amazon RDS, which automates time-consuming tasks such as hardware provisioning, database setup, patching, and backups.
- Supports distributed, fault-tolerant, self-healing storage that scales up to 128TB per database instance.
- Aurora I/O-Optimized cluster configuration for improved price performance for I/O-intensive applications.

## Amazon DynamoDB

### Overview
Amazon DynamoDB is a key-value and document database that provides single-digit millisecond performance at any scale. It is a fully managed, multi-Region database with built-in security, backup and restore, and in-memory caching for internet-scale applications.

### Key Features
- Handles more than 10 trillion requests per day and supports peaks of more than 20 million requests per second.
- Ideal for mobile, web, gaming, ad tech, IoT, and other applications requiring low-latency data access.
- Fully managed with no need to provision or manage servers.

## Amazon ElastiCache

### Overview
Amazon ElastiCache is a fully managed in-memory caching service that improves the performance of web applications by retrieving data from fast, managed caches.

### Supported Engines
- **Redis**: A Redis-compatible in-memory service suitable for high-performance use cases such as web, mobile apps, gaming, and IoT.
- **Memcached**: A widely adopted memory object caching system compatible with existing Memcached environments.

### Key Features
- ElastiCache Serverless: A serverless option that simplifies cache management and scales automatically to support demanding applications.

## Amazon Keyspaces (for Apache Cassandra)

### Overview
Amazon Keyspaces is a managed Apache Cassandra–compatible database service that allows you to run Cassandra workloads on AWS without managing servers or software.

### Key Features
- Serverless with automatic scaling based on application traffic.
- Continuous data backup with point-in-time recovery.
- Secure by default with encryption.

## Amazon MemoryDB

### Overview
Amazon MemoryDB is a Redis-compatible, durable in-memory database service designed for modern applications with microservices architectures.

### Key Features
- Microsecond read and single-digit millisecond write latency.
- Durable data storage across multiple Availability Zones using a distributed transactional log.

## Amazon Neptune

### Overview
Amazon Neptune is a fast, reliable, fully-managed graph database service that supports Property Graph and RDF graph models for building applications that work with highly connected datasets.

### Key Features
- Supports graph use cases such as recommendation engines, fraud detection, knowledge graphs, and network security.
- High availability with read replicas, point-in-time recovery, and replication across Availability Zones.

## Amazon Relational Database Service (RDS)

### Overview
Amazon RDS makes it easy to set up, operate, and scale a relational database in the cloud with support for six familiar database engines, including MySQL, MariaDB, PostgreSQL, Oracle Database, Microsoft SQL Server, and Amazon RDS on AWS Outposts.

### Key Features
- Automates time-consuming administration tasks such as hardware provisioning, database setup, patching, and backups.
- Cost-efficient and resizable capacity optimized for memory, performance, or I/O.

## Amazon Quantum Ledger Database (QLDB)

### Overview
Amazon QLDB is a fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log owned by a central trusted authority.

### Key Features
- Tracks each application data change and maintains a complete, verifiable history of changes over time.
- Serverless with automatic scaling and no need to manage infrastructure.

## Amazon Timestream

### Overview
Amazon Timestream is a fully managed time series database service designed for IoT and operational applications.

### Key Features
- Purpose-built for time series data, making it more efficient at processing time-interval data than relational databases.
- Serverless with automated data management features like rollups, retention, tiering, and compression.

## Amazon DocumentDB (with MongoDB compatibility)

### Overview
Amazon DocumentDB is a fast, scalable, fully managed document database service that is designed for operating mission-critical MongoDB workloads at scale.

### Key Features
- Supports MongoDB workloads with compatibility for MongoDB drivers and tools.
- Fully managed with automated patching, backups, and scaling.

## Amazon Lightsail Managed Databases

### Overview
Amazon Lightsail offers managed databases separate from compute workloads with support for MySQL and PostgreSQL.

### Key Features
- Simple setup and management using the Lightsail console, CLI, API, or SDK.
- Fixed monthly pricing with options for standard or high availability configurations.

