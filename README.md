# Recommender-System
Collaborative Filtering on Video Game Recommendation System

The dataset used for this case study is taken from a Kaggle page. The dataset contains many attributes, but only a few that are of interests for this recommendation system case study. I made some minor adjustments to the original dataset from Kaggle, such as deleting the columns I don't need in this case study. Here is the descriptions of the attributes after adjustments applied to the original kaggle dataset. *The modified dataset contains a list of users, the steam games they played, along with the number of hours played for that particular game.*

The attributes of the dataset are as follows :

1.	**userId** : Every user identified with a unique id (Structured)
2.	**steam_game** : Every game is identified with a unique name (Unstructured)
3.	**hours_played** : Number of Hours played for a game(Structured)

## The Approach Used (Latent factor models/Matrix Factorization)

Latent factor model is an approach that tries to explain the ratings by characterizing both items and users on, say, 20 to 100 factors inferred from the ratings patterns(Number of gaming hours for games in this case). For movies, the discovered factors might measure obvious dimensions such as comedy versus drama, amount of action, or orientation to children; less well-defined dimensions such as depth of character development or quirkiness; or completely uninterpretable dimensions. For games, the discovered factors might be the genres of the games such as adventure, MMORPG, action and strategy-based. For users, each factor measures how much the user likes games that score high on the corresponding movie factor. 

Reference : https://datajobs.com/data-science-repo/Recommender-Systems-[Netflix].pdf

### Matrix Factorization Methods
In its basic form, matrix factorization characterizes both items and users by vectors of factors inferred from item rating patterns.

High correspondence between item and user factors leads to a vector $q_{i}$ for $i^{th}$ item, and each user u is associated with a vector $p_{u}$. For a given item i, the elements of $q_{i}$ measure the extent to which the item possesses those **latent factors**. For a given user u, the elements of $p_{u}$ measure the extent of interest the user has in items that are high on the corresponding **latent factors**.

The resulting dot product, $\hat r = $$q_{i}^{T}$$p_{u}$, captures the interaction between user u and item i - the user's overall interest in the item's characteristics.

### Such a model is somewhat related to Singular Value Decomposition (SVD)
Singular value decomposition (SVD) is a well-established technique for identifying latent semantic factors in any given matrix. Any matrix A can be decomposed into U, $\Sigma$ and $V^{T}$. Applying SVD in the collaborative filtering domain requires factoring the user-item rating matrix. This often raises difficulties due to the high portion of missing values caused by sparseness in the user-item ratings matrix. Conventional SVD is undefined when knowledge about the matrix is incomplete. Moreover, carelessly addressing only the relatively few known entries is highly prone to overfitting.

Earlier systems relied on imputation to fill in missing
ratings and make the rating matrix dense$^2$.However, imputation can be very expensive as it significantly increases the amount of data. In addition, inaccurate imputation might distort the data considerably.

Hence, more recent works$^{3-6}$ suggested modeling directly the observed ratings only, while avoiding overfitting through a regularized model. To learn the factor vectors ($p_{u}$ and $q_{i}$), the system minimizes the regularized squared error on the set of known ratings:
<img src = 'pictures/objective_function.png'> 

The system learns the model by fitting the previously observed ratings. However, the goal is to generalize those previous ratings in a way that predicts future, unknown ratings. Thus, the system should avoid overfitting the observed data by regularizing the learned parameters, whose magnitudes are penalized. The constant λ controls the extent of regularization and is usually determined by cross-validation. Ruslan Salakhutdinov and Andriy Mnih’s “Probabilistic Matrix Factorization”$^{7}$ offers a probabilistic foundation for regularization. 


2. B.M. Sarwar et al., “Application of Dimensionality Reduction in Recommender System—A Case Study,” Proc. KDD
Workshop on Web Mining for e-Commerce: Challenges and
Opportunities (WebKDD), ACM Press, 2000. 
3. S. Funk, “Netflix Update: Try This at Home,” Dec. 2006;
http://sifter.org/~simon/journal/20061211.html.
4. Y. Koren, “Factorization Meets the Neighborhood: A Multifaceted Collaborative Filtering Model,” Proc. 14th ACM
SIGKDD Int’l Conf. Knowledge Discovery and Data Mining,
ACM Press, 2008, pp. 426-434.
5. A. Paterek, “Improving Regularized Singular Value Decomposition for Collaborative Filtering,” Proc. KDD Cup
and Workshop, ACM Press, 2007, pp. 39-42.
6. G. Takács et al., “Major Components of the Gravity Recommendation System,” SIGKDD Explorations, vol. 9, 2007, pp.
80-84.
7. R. Salakhutdinov and A. Mnih, “Probabilistic Matrix Factorization,” Proc. Advances in Neural Information Processing
Systems 20 (NIPS 07), ACM Press, 2008, pp. 1257-1264. 
