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
# C-Rating Aggregator - Standardized Movie Rating Calculation

## 1️⃣ Introduction
C-Rating Aggregator is responsible for **calculating a standardized rating (0-100) for movies** based on multiple sources (IMDb, Rotten Tomatoes, Metacritic, etc.).  
It ensures fair comparison by **normalizing ratings and weighting them based on three key factors**.

## 2️⃣ Why do we need C-Rating?
- Movie ratings from different sources **vary in scale and format**.
- Some sources **are more reliable than others**, so we need **weighted aggregation**.
- We want a **single, comparable score** that represents a movie’s overall quality.

---

## 3️⃣ C-Rating Calculation Formula
C-Rating is calculated using a weighted formula:

\[
C\text{-}Rating = \frac{W_1 \times \text{Performance} + W_2 \times \text{Screenplay} + W_3 \times \text{Soundtrack}}{W_1 + W_2 + W_3}
\]

### **Weights Used:**
| Factor | Description | Weight |
|--------|------------|--------|
| **Performance** | Acting, cinematography, directing | `0.40` |
| **Screenplay** | Storyline, dialogues, plot structure | `0.35` |
| **Soundtrack** | Music composition, emotional impact | `0.25` |

---

## 4️⃣ Data Flow
1. **Raw ratings** from different sources are fetched.  
2. **Normalization** is applied to convert ratings to a **0-100 scale**.  
3. Ratings are categorized into **Performance, Screenplay, and Soundtrack**.  
4. **Weighted average is computed** to get the final **C-Rating™**.

---

## 5️⃣ Example Calculation
If we have the following ratings for a movie:

| Factor | Score |
|--------|------|
| Performance | `85` |
| Screenplay | `90` |
| Soundtrack | `80` |

Using our formula:

\[
C\text{-}Rating = \frac{0.4 \times 85 + 0.35 \times 90 + 0.25 \times 80}{0.4 + 0.35 + 0.25}
\]

\[
C\text{-}Rating = \frac{34 + 31.5 + 20}{1} = 85.5
\]

Thus, the **final C-Rating = `85.5`**.

---

## 6️⃣ Python Code Implementation
```python
def calculate_c_rating(performance, screenplay, soundtrack, w1=0.4, w2=0.35, w3=0.25):
    return round((w1 * performance + w2 * screenplay + w3 * soundtrack) / (w1 + w2 + w3), 2)

# Example calculation
print(calculate_c_rating(performance=85, screenplay=90, soundtrack=80))  # Output: 85.5

