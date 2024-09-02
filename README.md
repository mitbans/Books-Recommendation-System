# Book Recommendation System

## Understanding the Problem:
Given a dataset of user IDs, item IDs (books), and ratings, the goal is to predict which books a user might like based on their past preferences and the preferences of similar users.

#### **Collaborative Filtering:**
This is a popular technique for recommendation systems. It assumes that users who have similar tastes in the past will likely have similar tastes in the future.

## Data Understanding

#### **Book Genome Dataset**

- The data is derived from the [grouplens example datasets](https://grouplens.org/datasets/movielens/)
- Books Dataset URL: [Book Genome Dataset](https://grouplens.org/datasets/book-genome/)
- Raw ratings data includes information such as item id, user id and user ratings.
- Raw metadata includes information such as item id and title.

## Data Preparation

- Load the dataset
- Take a small sample of 500K records for ease of processing
- Load the dataset into sf

## Modeling
### Comparing Recommendation Algorithms: KNNBasic, SVD, NMF, SlopeOne, and CoClustering
#### **Understanding the Algorithms:**

- **KNNBasic:** A simple nearest neighbor algorithm that recommends items based on the ratings of similar users.   
- **SVD:** Singular Value Decomposition is a matrix factorization technique that decomposes the user-item rating matrix into latent factors.   
- **NMF:** Non-negative Matrix Factorization is another matrix factorization technique that decomposes the rating matrix into non-negative factors.
- **SlopeOne:** A simple algorithm that estimates the rating of an item by a user based on the average difference between ratings of that item and other items rated by the user.
- **CoClustering:** A clustering-based approach that simultaneously clusters users and items, assuming that users in the same cluster tend to prefer items in the same cluster.

**Cross-Validation:** Due to compute constraints, couldn't perform cross-validation for KNNBasic.

## Evaluation:
#### **Metrics:** 
Used metrics like root mean squared error (RMSE) and mean absolute error (MAE) to evaluate the accuracy of the recommendations.

## Conclusion

Based on the evaluation metrics (RMSE and MAE), SVD appears to be the most effective algorithm for the given book recommendation task. It consistently demonstrates lower error rates compared to the other algorithms (NMF, SlopeOne, and CoClustering).

### Key Findings:

- **SVD**: Best accuracy with the lowest RMSE (0.9778) and MAE (0.7746), and balanced fit and test times.
- **NMF**: Higher error rates (RMSE: 1.1363, MAE: 0.8926) with the longest fit times but faster test times.
- **SlopeOne**: Highest error rates (RMSE: 1.1809, MAE: 0.8936) with the shortest fit times.
- **CoClustering**: Better accuracy than NMF and SlopeOne (RMSE: 1.0662, MAE: 0.8086) but with longer fit times.
  
## Further Considerations:

- **Scalability**: Assessing how well each model scales with increasing data size. SVD and CoClustering may handle larger datasets better due to their matrix factorization approaches.
- **Computational Resources**: Considering the available computational resources. If resources are limited, SlopeOne’s low computational cost might be beneficial despite its lower accuracy.
- **Real-Time Performance**: Evaluating the test time and whether the model can meet real-time requirements if applicable. SlopeOne and CoClustering offer different trade-offs between accuracy and speed.
- **Interpretability**: Some models might provide better insights into the data. For instance, SVD and CoClustering can offer more interpretable results compared to NMF.
- **Robustness**: Examining how each model performs under various conditions or with noisy data. Consistency in error rates across folds is an indicator of robustness.
- **Future Updates**: Considering how easily each model can be updated or retrained as new data becomes available. 
- **Business Needs**: Aligning the choice of model with the specific needs and constraints of the business or application, including accuracy requirements, computational constraints, and real-time processing needs.

## Repository Structure
- <code>data/ratings_500k.csv</code>: Contains dataset used in the analysis, 500k samples derived from following two json files:
  - <code>data/metadata.json</code>: contains information on the books such as title, author, item id
  - <code>[Links to external drive: ratings.json](https://1drv.ms/u/s!An52_3Dm4mMNlimcP4o7uIkKkCFX?e=CWGgCg)</code>: contains information such as item_id, user_id and ratings
- <code>notebooks/Book-Recommendation-System.ipynb</code>: Jupyter notebook with code for data analysis.
- <code>README.md</code>: Summary of findings and link to notebook

## Notebook
The detailed analysis and code can be found in the Jupyter notebook <a href="https://github.com/mitbans/Books-Recommendation-System/blob/main/notebooks/Book-Recommendation-System.ipynb">here</a>.

---
