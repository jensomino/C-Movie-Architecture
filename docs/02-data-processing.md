# 📂 Data Processing & Normalization Layer  

## 1️⃣ Introduction  
The **Data Processing & Normalization Layer** is responsible for **cleaning, standardizing, and processing** movie ratings from multiple sources.  

## 2️⃣ Why is this Layer Important?  
- Different sources use **different scales** (e.g., IMDb: 0-10, Rotten Tomatoes: 0-100%).  
- Movie genres **are not standardized** across platforms.  
- Some sources provide **incomplete or incorrect data**, which must be cleaned.  

## 3️⃣ Components of Data Processing Layer  
| 🏗 **Component** | 🔍 **Description** |  
|----------------|------------------|  
| **Data Cleaning & Standardization** | Removes duplicate, missing, or inconsistent data |  
| **Rating Normalizer** | Converts all ratings to a **0-100 scale** |  
| **C-Rating Aggregator** | Computes the final **C-Rating™** |  

🔹 **For more details about the final rating calculation, refer to:**  
📌 **[C-Rating Aggregator](#-c-rating-aggregator)**  

## 4️⃣ **Rating Normalization**  
Different sources use different rating scales, so we **normalize them** to a **0-100 scale**.  

### **🔹 Normalization Formula**  
| Source | Original Scale | Normalization Formula |  
|--------|--------------|----------------------|  
| **IMDb** | 0-10 | `rating * 10` |  
| **Rotten Tomatoes** | 0-100% | `rating (unchanged)` |  
| **Metacritic** | 0-100 | `rating * 0.85` |  

### **🔹 Python Example**  
```python
def normalize_rating(source, rating):
    if source == "IMDb":
        return rating * 10  # Convert 0-10 to 0-100
    elif source == "Rotten Tomatoes":
        return rating  # Already in 0-100 scale
    elif source == "Metacritic":
        return rating * 0.85  # Adjusting Metacritic scale
    return None
```

