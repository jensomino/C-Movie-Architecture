# C-Movie Architecture Diagram

## Overview
This is the system architecture for the C-Movie rating aggregation platform. The diagram below represents the various layers and components involved in the system.

```mermaid
flowchart TB
    %% Layers
    subgraph L1 [Data Ingestion Layer]
        APICon[API Connectors - IMDb, Rotten Tomatoes, etc.] --> MsgQueue["Message Queue (Kafka/RabbitMQ)"]
        FileProcessor[File Processor - CSV Handling] --> MsgQueue
    end
    
    subgraph L2 [Data Processing Layer]
        MsgQueue --> CleanStandardize[Data Cleaning & Standardization]
        CleanStandardize --> RatingNormalizer[Rating Normalizer]
        RatingNormalizer --> CRatingAggregator["C-Rating Aggregator"]
        
        %% Batch vs Streaming Processing
        subgraph ProcessingMethods ["Batch vs Streaming Processing"]
            BatchProcessing["Batch Processing\n(Cloud Scheduler, Airflow)"] --> RatingNormalizer
            StreamingProcessing["Streaming Processing\n(Kafka, Apache Flink)"] --> RatingNormalizer
        end
    end
    
    subgraph L3 [Storage Layer]
        CRatingAggregator --> RelationalDB["Relational Database PostgreSQL/MySQL"]
        CRatingAggregator --> NoSQLDB["NoSQL Database MongoDB/Redis"]
        CRatingAggregator --> DataLake["Data Lake (Cloud Storage, S3, BigQuery)"]
    end
    
    subgraph L4 [API & Web Application Layer]
        RelationalDB & NoSQLDB & DataLake --> RESTAPI["REST API with OAuth & Rate Limiting"]
        RESTAPI <--> WebApp["Web Application (React/Vue.js)"]
        RESTAPI --> CRatingAggregator
    end
    
    subgraph FutureEnhancements ["Future Enhancements"]
        UserReviews["User Reviews & Feedback System"] --> WebApp
        RecommendationEngine["AI-based Recommendation Engine"] --> WebApp
    end
