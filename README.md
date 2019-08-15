# music_recommend

1. Collobrative filtering

Note: (1) In the cost function, there is no X0 = 1. (2) Random initilization is important to break the symmetricity of the matrix. (3) Mean normalization is used to help the optimization process.

2. Content-based collobrative filtering

By adding new vector making the user space to a higher dimension space, we can add information, such as time and location into the user profile for collobrative filtering. 

Resource:

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
