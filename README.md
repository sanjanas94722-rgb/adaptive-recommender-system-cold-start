# An Adaptive Hybrid Recommender System for the Item Cold-Start Problem

**Author:** Sanjana (ID 240335366)
**Supervisor:** Prof. Nicola Perra
*A dissertation project for the degree of Master of Science in Data Analytics at Queen Mary University of London.*

---

## 1. Abstract

[cite_start]Recommender systems are crucial to modern digital platforms, but their efficacy is often undermined by the item cold-start problem—the failure to provide relevant suggestions for new items lacking user interaction data[cite: 19]. [cite_start]This dissertation addresses this gap by developing and testing an adaptive hybrid recommender system that combines content-based and collaborative filtering methods[cite: 21].

[cite_start]Using the MovieLens dataset[cite: 23], this study implements and evaluates three models:
1.  [cite_start]**Content-Based Model:** Uses Term Frequency-Inverse Document Frequency (TF-IDF) on movie genres[cite: 24].
2.  [cite_start]**Collaborative Filtering Model:** Uses Singular Value Decomposition (SVD)[cite: 25].
3.  [cite_start]**Adaptive Hybrid Model:** A novel system that combines predictions from the first two models using a linear ramp-up weighting function, which dynamically adjusts its logic based on an item's popularity[cite: 26].

---

## 2. Dataset

[cite_start]This project uses the **MovieLens (ml-latest-small)** dataset from GroupLens. It contains 100,836 ratings on 9,742 movies by 610 users.

* The data is included in the `/data/` folder.
* The raw files are `ratings.csv`, `movies.csv`, and `tags.csv`.

---

## 3. Methodology

The full analysis is contained in the `notebooks/dissertation_code.ipynb` file. The process follows these phases:

1.  **Data Cleaning & Preprocessing:** Loaded 100,000+ ratings. Cleaned and standardized movie titles, extracted release years, and converted timestamps (cells 127-129).
2.  **Exploratory Data Analysis (EDA):** Visualized the distribution of ratings, genre frequency, and the long-tail distribution of ratings per movie, which confirms the item cold-start problem (cells 134-137).
3.  **Model Implementation:**
    * **Content-Based:** Built using TF-IDF on movie genres and Cosine Similarity to find item-item likeness (cell 140).
    * **Collaborative Filtering:** Built using the `surprise` library and the SVD algorithm (cell 143).
    * **Adaptive Hybrid:** Implemented a blending logic with an adaptive weighting function `w(n) = min(n/k, 1.0)` that transitions from content-based predictions for new items (low `n`) to collaborative predictions for established items (high `n`) (cells 149, 152).
4.  **Evaluation:**
    * Analyzed the standalone SVD model, confirming it has a high error (RMSE) for cold-start items (cell 153).
    * Performed a final comparative analysis of all three models for both accuracy (RMSE) and speed (cell 156).

---

## 4. Key Results

The final analysis (cell 156) provides a clear trade-off between accuracy and speed:

| Model | Accuracy (RMSE) | Speed (Time per Rec) |
| :--- | :--- | :--- |
| **Collaborative (SVD)** | **0.8809** | 0.0623s |
| **Adaptive Hybrid** | 0.9380 | 0.0127s |
| **Content-Based** | 1.0446 | **0.0045s** |

[cite_start]**Conclusion:** The standalone Collaborative Filtering (SVD) model achieved the best overall accuracy[cite: 618]. However, the Adaptive Hybrid model serves as an excellent compromise, providing a significant speed increase over pure SVD while being far more accurate than the pure Content-Based model. It effectively solves the cold-start problem by relying on content features when no ratings exist and gracefully transitioning to the more accurate SVD predictions as the item gains popularity.

The full dissertation document is available in `report/dissertation_report.pdf`.

---

## 5. How to Run This Project

1.  Clone this repository:
    ```bash
    git clone [https://github.com/](https://github.com/)[your-username]/adaptive-recommender-system-cold-start.git
    cd adaptive-recommender-system-cold-start
    ```

2.  (Optional but recommended) Create a virtual environment:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  Install the required libraries:
    ```bash
    pip install -r requirements.txt
    ```

4.  The raw data is already included in the `/data/` folder.

5.  Open the Jupyter Notebook to see the full analysis:
    ```bash
    jupyter notebook notebooks/dissertation_code.ipynb
    ```
