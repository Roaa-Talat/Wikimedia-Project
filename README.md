# 🌀 Wikimedia Traffic Analysis using Spark (MapReduce vs Loops)

This project explores Wikimedia traffic data using Apache Spark, applying two paradigms:
- **MapReduce-style transformations** (functional programming)
- **Spark with loops** (procedural logic)

We analyze page statistics, identify trends, and compare performance across approaches, focusing on efficiency and accuracy when processing large-scale data.

---

## 📚 Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Approaches](#approaches)
- [Problem Definitions](#problem-definitions)
- [Performance Comparison](#performance-comparison)
- [Conclusion](#conclusion)

---

## 📌 Project Overview

This project analyzes Wikimedia traffic logs using Apache Spark, implementing the same queries in two styles:
- **MapReduce Transformations** (using `map`, `reduceByKey`, `filter`, etc.)
- **Procedural Spark Loops** (using `for` loops and sequential DataFrame logic)

It benchmarks both paradigms across five key queries and compares performance based on task size, complexity, and Spark's behavior.

---

## 🛠 Tech Stack

- 🐍 Python
- ⚡ Apache Spark (PySpark)
- 📊 Matplotlib & Seaborn
- 📁 Jupyter Notebook

---

## ⚙️ Approaches

### ✅ MapReduce (Functional Spark)
- Utilizes `RDD.map`, `reduceByKey`, and `flatMap`.
- Designed for distributed computation.
- Ideal for large-scale datasets with heavy computation.

### 🔁 Spark Loops (Imperative)
- Uses Python `for` loops and `collect()`.
- Suitable for smaller tasks that fit in memory.
- Avoids Spark’s distributed overhead when unnecessary.

---

## 🧩 Problem Definitions

The project addresses the following five data analysis problems:

1. **Page Size Statistics**  
   Compute the minimum, maximum, and average page size across all entries.

2. **Titles Starting with "The"**  
   Count how many page titles start with “The” and how many of them are not part of the English project (`project != "en"`).

3. **Unique Terms in Titles**  
   Determine the number of unique normalized terms in page titles. Titles are split by “_”, with terms lowercased and cleaned of non-alphanumeric characters.

4. **Title Frequency Count**  
   Extract each title and count the number of times it appears in the dataset.

5. **Merge Duplicate Titles**  
   Group and combine records with identical titles from different sources and display each matched pair.

---

## ⚡ Performance Comparison

Measured execution times for each approach:

| Query                                           | MapReduce Time (sec) | Spark Loops Time (sec) | Speedup (×) |
|------------------------------------------------|-----------------------|-------------------------|-------------|
| Min, Max, and Avg Page Size                    | 15.6108               | 2.8708                  | 5.44×       |
| Titles Starting with "The" (non-English filter)| 8.4738                | 2.1718                  | 3.90×       |
| Unique Terms in Titles                         | 11.8674               | 4.5771                  | 2.59×       |
| Count Title Occurrences                        | 25.6639               | 3.3709                  | 7.61×       |
| Combine Data for Same Titles                   | 11.2713               | 9.8272                  | 1.15×       |

> ℹ️ **Spark Loops outperformed MapReduce in all five queries** for this dataset.  
> Spark Loops were significantly faster due to collecting data in memory and avoiding distributed job overhead — which is ideal for smaller-scale tasks.  
> **However, for large-scale datasets, the MapReduce paradigm is generally more efficient and scalable** because it fully leverages Spark’s distributed processing capabilities.

---

## ✅ Conclusion

This project highlights:
- A practical comparison between **MapReduce-style transformations** and **Spark procedural loops**.
- In this context, **Spark Loops executed significantly faster** because the dataset was manageable and local memory processing was more efficient.
- MapReduce remains a strong approach for distributed workloads and very large datasets.
- The choice between paradigms should consider **task size**, **execution context**, and **resource availability**.

