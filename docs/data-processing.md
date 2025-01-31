# Data Processing & Normalization Layer

## 1️⃣ Introduction
The **Data Processing & Normalization Layer** is responsible for **cleaning, standardizing, and processing** movie ratings from multiple sources (IMDb, Rotten Tomatoes, Metacritic, etc.).  
It ensures that all ratings are transformed into a **consistent format** and computes the **final C-Rating™**.

## 2️⃣ Why is this Layer Important?
- Different sources use **different scales** (e.g., IMDb: 0-10, Rotten Tomatoes: 0-100%).
- Movie genres **are not standardized** across platforms.
- Some sources provide **incomplete or incorrect data**, which must be cleaned.

---

## 3️⃣ Components of Data Processing Layer
This layer consists of the following components:

| Component | Description |
|-----------|------------|
| **Data Cleaning & Standardization** | Removes duplicate, missing, or inconsistent data |
| **Rating Normalizer** | Converts all ratings to a **0-100 scale** |
| **C-Rating Aggregator** | Computes the final **C-Rating™** |

🔹 **For more details about the final rating calculation, refer to:**  
📌 **[C-Rating Aggregator Documentation](docs/c-rating.md)**

---

## 4️⃣ **Data Cleaning & Standardization**
### **🔹 Tasks Performed**
✅ **Duplicate Removal:** If the same movie appears multiple times, only the most reliable data is kept.  
✅ **Missing Value Handling:** If data is missing, it is either ignored or estimated based on available sources.  
✅ **Genre Standardization:** Different platforms categorize genres differently, so they are unified.

### **🔹 Example - Standardizing Genres**
| IMDb | Rotten Tomatoes | Metacritic | **Standardized Genre** |
|------|---------------|-----------|------------------|
| Sci-Fi | Science Fiction | SciFi | **Science Fiction** |
| Drama, Mystery | Drama | Drama/Thriller | **Drama** |

### **🔹 Python Example**
```python
def standardize_genre(genres):
    mapping = {
        "Sci-Fi": "Science Fiction",
        "SciFi": "Science Fiction",
        "Science Fiction": "Science Fiction",
        "Drama/Thriller": "Drama",
        "Mystery": "Drama"
    }
    return [mapping.get(genre, genre) for genre in genres]

genres = ["Sci-Fi", "Drama/Thriller"]
print(standardize_genre(genres))  # Output: ['Science Fiction', 'Drama']
