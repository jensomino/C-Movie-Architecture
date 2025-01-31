# Data Ingestion Layer

## 1️⃣ Introduction
The **Data Ingestion Layer** is responsible for collecting movie rating data from different sources.  
It ensures that data is fetched efficiently, regardless of its format (API, CSV files, or Web Scraping).  

## 2️⃣ Why is this Layer Important?
- **Multiple data sources** exist (APIs, CSV, Web Scraping), each with **different formats**.  
- Data must be **ingested, queued, and processed asynchronously** to ensure system efficiency.  
- **Real-time data fetching** needs to be balanced with **batch processing** for scalability.  

---

## 3️⃣ Components of Data Ingestion Layer
This layer consists of three main components:

| Component | Description |
|-----------|------------|
| **API Connectors** | Fetches data from external APIs (IMDb, Rotten Tomatoes, Metacritic) |
| **File Processor** | Handles periodic file uploads (CSV, JSON, XML) |
| **Message Queue (Kafka/RabbitMQ)** | Stores incoming data before processing |

---

## 4️⃣ **API Connectors**
This component connects to **external APIs** to fetch real-time data.

### **🔹 Supported APIs**
- **IMDb API** → Provides ratings and metadata for movies.
- **Rotten Tomatoes API** → Fetches critic and audience scores.
- **Metacritic API** → Collects aggregated critic reviews.

### **🔹 Example API Request**
```http
GET https://api.imdb.com/movies?title=Inception
Authorization: Bearer <token>
