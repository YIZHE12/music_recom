# Music recommendation system in Python

## Primary components of a recommender system

#### Candidate Generation
In this first stage, the system starts from a potentially huge corpus and generates a much smaller subset of candidates. For example, the candidate generator in YouTube reduces billions of videos down to hundreds or thousands. The model needs to evaluate queries quickly given the enormous size of the corpus. A given model may provide multiple candidate generators, each nominating a different subset of candidates.

Both content-based and collaborative filtering map each item and each query (or context) to an embedding vector.

A similarity measure is a function that takes a pair of embeddings and returns a scalar measuring their similarity. 

There are three main function for similarity measure: cosine, dot product and Euclidean distance.

Items that appear very frequently in the training set (for example, popular YouTube videos) tend to have embeddings with large norms. If capturing popularity information is desirable, then you should prefer dot product. However, if you're not careful, the popular items may end up dominating the recommendations. In practice, we often use a modulation to reduce the influence of the norm in the dot product: <img src = images/dot_product_eq.png height = 30>

#### Scoring
Next, another model scores and ranks the candidates in order to select the set of items (on the order of 10) to display to the user. Since this model evaluates a relatively small subset of items, the system can use a more precise model relying on additional queries.

#### Re-ranking
Finally, the system must take into account additional constraints for the final ranking. For example, the system removes items that the user explicitly disliked or boosts the score of fresher content. Re-ranking can also help ensure diversity, freshness, and fairness.

## Types of recommendation systems

### Content-based 

A content-based only model will recommend items based on similar items. If you like item A, and item B is most similar to item A, then it will be recommended to you.


#### Advantages

The model doesn't need any data about other users, since the recommendations are specific to this user. This makes it easier to scale to a large number of users.

The model can capture the specific interests of a user, and can recommend niche items that very few other users are interested in.

#### Disadvantages

Since the feature representation of the items are hand-engineered to some extent, this technique requires a lot of domain knowledge. Therefore, the model can only be as good as the hand-engineered features.

The model can only make recommendations based on existing interests of the user. In other words, the model has limited ability to expand on the users' existing interests.


### Collobrative filtering

Note: (1) In the cost function, there is no X0 = 1. (2) Random initilization is important to break the symmetricity of the matrix. (3) Mean normalization is used to help the optimization process.

<img src = images/MF.png height = 600>

The full matrix has O(mn) dimensions, while the U and V have (O(m+n)d). In reality, since d is much smaller than m or n, it reduces the complexity. 

The objective of the model is to minimize the loss of:

<img src = images/loss.png height = 60>

You may propose to use Singular Value Decomposition(SVD) to solve this problem. However, as our matrix A is very sparse, SVD will likely to propose an all zero solution. In reality, it is often used Weighted Matrix Factorization: A sum over observed entries and a sum over unobserved entries (treated as zeroes).

<img src = images/WFM1.png height = 100>

<img src = images/WFM2.png height = 50>

Common algorithms to minimize the objective function include:

1. Stochastic gradient descent (SGD)

2. Weighted Alternating Least Squares (WALS)

WALS converge faster and handle the unobserved entries better. SGD need to combine with negative sampling and gravity to handle unobserved data. Negative sampling only modify a small percentage of the weights, rather than all of them, for each training sample. Gravity is a global prior that pushes the prediction of any pair towards zero.

One of the main issue of collobrative filtering is cold-start problem: for item or user that it hasn't seen before.

This is often been solved by:
#### Projection in WALS

One iteration in WALS: the user embeddings are kept fixed, and the system solves for the embedding of item. The same can be done for a new user.

#### Averaging

The system can approximate its embedding by averaging the embeddings of items from the same category

### Hybrid

In this repo, I showed how to build a collobrative fitltering model for music recommendation, using regularlized Matrix Factorization. You can open the notebook in google Colab by clicking this button <img src = images/colab.png height = 25>. Note that you will open a read-only version, therefore, please save a copy on your own google drive to edit and run the code.
In the 'Make your own prediction to build a play list', make USER_RATINGS = True. Run the codes in the following sections and a link will pop up to ask you give authoration to use the google spreadsheet API. You will need to give the permission and a code will be generated. Please copy this code and paste it in the notebook section following the instruction on the notebook. After that, you can follow the instruciton of the notebook to give a score between 0-1 to music you like in the google spreadsheet. Your data will then used to create a music recommendation list.

I also built a Word2Vec model to compare similarity between song title in order to recommend songs that the recommendation system hasn't trained on. However, in reality, this should be replaced by the lyrics instead of song titles to have more relevant information.



## Resource

E-book:
http://charuaggarwal.net/Recommender-Systems.pdf

https://pdfs.semanticscholar.org/5d1d/d378962c7601526f65f69e408f8800a0d3c4.pdf

GCP TF solutions
https://cloud.google.com/solutions/machine-learning/recommendation-system-tensorflow-overview

Colab:
https://developers.google.com/machine-learning/recommendation/labs/movie-rec-programming-exercise

https://colab.research.google.com/github/google/eng-edu/blob/master/ml/recommendation-systems/recommendation-systems.ipynb?utm_source=ss-recommendation-systems&utm_campaign=colab-external&utm_medium=referral&utm_content=recommendation-systems


ProdToVec Paper:
https://arxiv.org/pdf/1607.07326.pdf

LightFM Package:
https://github.com/lyst/lightfm

Articles:
Collaborative embedding https://towardsdatascience.com/collaborative-embeddings-for-lipstick-recommendations-98eccfa816bd


Data:
http://millionsongdataset.com/
https://towardsdatascience.com/how-to-build-a-simple-song-recommender-296fcbc8c85



https://github.com/MaurizioFD/RecSys2019_DeepLearning_Evaluation
