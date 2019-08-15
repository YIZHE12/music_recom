# music_recommend
## Type of recommendation system
1. Collobrative filtering

Note: (1) In the cost function, there is no X0 = 1. (2) Random initilization is important to break the symmetricity of the matrix. (3) Mean normalization is used to help the optimization process.

2. Content-based collobrative filtering

By adding new vector making the user space to a higher dimension space, we can add information, such as time and location into the user profile for collobrative filtering. 
## Primary components of a recommender system

#### Candidate Generation
In this first stage, the system starts from a potentially huge corpus and generates a much smaller subset of candidates. For example, the candidate generator in YouTube reduces billions of videos down to hundreds or thousands. The model needs to evaluate queries quickly given the enormous size of the corpus. A given model may provide multiple candidate generators, each nominating a different subset of candidates.

Both content-based and collaborative filtering map each item and each query (or context) to an embedding vector.

A similarity measure is a function that takes a pair of embeddings and returns a scalar measuring their similarity. 

There are three main function for similarity measure: cosine, dot product and Euclidean distance.

Items that appear very frequently in the training set (for example, popular YouTube videos) tend to have embeddings with large norms. If capturing popularity information is desirable, then you should prefer dot product. However, if you're not careful, the popular items may end up dominating the recommendations. In practice, we often use a modulation to reduce the influence of the norm in the dot product: 

<img src = images/images/dot_product_eq.png height = 50>

#### Scoring
Next, another model scores and ranks the candidates in order to select the set of items (on the order of 10) to display to the user. Since this model evaluates a relatively small subset of items, the system can use a more precise model relying on additional queries.

#### Re-ranking
Finally, the system must take into account additional constraints for the final ranking. For example, the system removes items that the user explicitly disliked or boosts the score of fresher content. Re-ranking can also help ensure diversity, freshness, and fairness.
## Resource

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
