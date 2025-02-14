# 💾 Storage Layer  

## 1️⃣ Introduction  
The **Storage Layer** is responsible for storing processed and normalized movie ratings efficiently.  
It ensures **fast retrieval, scalability, and reliability** by using a combination of relational, NoSQL, and data lake storage solutions.  

## 2️⃣ Why is this Layer Important?  
- **Structured and unstructured data must be handled efficiently.**  
- **Fast query performance** is required for the API and web application.  
- **Historical data must be stored for analytics and machine learning models.**  

## 3️⃣ Components of Storage Layer  
| 🏗 **Component** | 🔍 **Description** |  
|----------------|------------------|  
| **Relational Database (PostgreSQL/MySQL)** | Stores structured movie metadata and normalized ratings. |  
| **NoSQL Database (MongoDB/Redis)** | Caches frequently accessed data for fast retrieval. |  
| **Data Lake (Cloud Storage, S3, BigQuery)** | Stores raw and historical data for analytics. |  

---

## 4️⃣ Relational Database (PostgreSQL/MySQL)  
A **relational database** is used to store structured movie data, such as:  
- **Movie title, genre, release year, director, etc.**  
- **Normalized ratings** after processing.  
- **User-generated metadata** (e.g., comments, custom lists).  

### **🔹 Example Table Schema**  
```sql
CREATE TABLE movies (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    genre VARCHAR(255),
    release_year INT,
    director VARCHAR(255)
);

CREATE TABLE ratings (
    id SERIAL PRIMARY KEY,
    movie_id INT REFERENCES movies(id),
    source VARCHAR(255),
    normalized_rating FLOAT
);
```

---

## 5️⃣ NoSQL Database (MongoDB/Redis)  
A **NoSQL database** is used for **caching and flexible data storage**.  
- **MongoDB** stores semi-structured movie metadata and user interactions.  
- **Redis** caches frequently accessed ratings to improve performance.  

### **🔹 Example MongoDB Document**  
```json
{
    "movie_id": "tt1375666",
    "title": "Inception",
    "normalized_rating": 85.5,
    "genres": ["Sci-Fi", "Thriller"],
    "cached_at": "2025-01-31T12:00:00Z"
}
```

---

## 6️⃣ Data Lake (Cloud Storage, S3, BigQuery)  
A **data lake** stores raw and historical data for analytics and machine learning.  
- **Cloud Storage/S3** stores raw CSV/XML files from data ingestion.  
- **BigQuery** allows complex queries and trend analysis over time.  

### **🔹 Example BigQuery Query**  
```sql
SELECT title, AVG(normalized_rating) as avg_rating 
FROM `c_movie_dataset.ratings`
GROUP BY title
ORDER BY avg_rating DESC;
```

📌 **The Storage Layer ensures efficient and scalable storage of movie ratings for fast queries and long-term analytics.** 🚀

