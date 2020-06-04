---
title: Movie Night
summary: A group recommender engine for your movie night! After each user answers a few movie questions, the system will find movies that best appeal to the whole group.
authors: [Yuan Meng]
tags: []
categories: []
date: "2020-05-31"
slides:
  theme: night				
  highlight_style: dracula

---

## 🎬 Movie Night 🍿
#### A Group Movie Recommender System

Yuan Meng

[GitHub](https://github.com/Yuan-Meng/movie-night) | [Website](https://www.yuan-meng.com/project/movie_night/)

{{< speaker_note >}}
- Hi my name is Yuan, a PhD student in CogSci at UC Berkeley. 
- Today I'll be presenting my final capstone, Movie Night, which is a group movie recommender system that I built.
{{< /speaker_note >}}

---

#### A Zoom movie night

<figure>
  <img src="/img/movie_night.jpeg" align=top width="480" />
</figure>

<ul>
  {{% fragment %}}<li>One hour choosing, two hours watching...</li>{{% /fragment %}}
  {{% fragment %}}<li>How can we painlessly pick a movie that makes everyone happy? 🤔</li>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- Today, recommender systems are everywhere. In a world overloaded with options, they help us choose what movies to watch, products to buy, restaurants to eat, and many more.
- If personal decisions are already hard enough, then making decisions for a group only gets much trickier. For example, I had a Zoom movie night with two friends a while ago. Although we were very happy with our choice, it took us almost an hour to decide.
- I thought there must be a movie recommender for a group like us but after some Googling, I found many theorectial papers on this topic but not a commercial application that I can readily use. So I decided to prototype such a group movie recommender system in this project. And I think during this pandemic, group recommender systems will come really handy as families more decisions together and need to accommodate each other more so than ever.
{{< /speaker_note >}}

---

# Part I
## Build A Movie Recommender

{{< speaker_note >}}
- The first step is to build a regular recommender system for single users.
{{< /speaker_note >}}

---

### Data: <a href="https://grouplens.org/datasets/movielens/latest/">MovieLens</a> 

- 100,836 ratings of 9,742 movies by 610 users from 1996 to 2018 (updated in 2018)

<figure><img src="/img/movielens_viz.jpeg" align=top width="700" hspace="-10" /></figure>

{{< speaker_note >}}
- Two datasets are most popular for building movie recommender systems: MovieLens and the Netflix Prize Data. Both use an explict rating system on a scale from 1 to 5 stars. The Netflix data was last updated in 2005 so MovieLens is much more suitable for making timely recommendations.
- The version I'm using was updated in 2018 and has about 100,000 ratings of 9,742 movies by 610 users. The average rating is 3.5 stars so the users were pretty generous. Each movie received a median of 8 ratings and each user gave out a median of 77 ratings. A few movies are particularly popular and some users are especially prolific. 
{{< /speaker_note >}}

---

### Algorithms

To make recommendations is to predict ratings:
<figure>
  <img src="/img/sparse_matrix.png" align=top width="400" hspace="-10" />
</figure>

<ul>
{{% fragment %}}<li><b>Content filtering:</b> User and/or item features</li>{{% /fragment %}}
{{% fragment %}}<li><b>Collaborative filtering:</b> User-item interactions</li>{{% /fragment %}}
{{% fragment %}}<li><b>Hybrid filtering:</b> Combining both of the above</li>{{% /fragment %}}
</ul>

{{< speaker_note >}}
- Each user only rated a small proportion of all the movies in the system. To make recommendations is to predict how each user would rate each movie and recommend top N movies to them.
- So how do we do that? One common approach is content filtering based on the idea that similar movies receive and similar users give similar ratings. For instance, considering that LOTR has such high ratings, you may predict that other fantasy movies with epic battle sequences and ancient mythologies will also be rated highly. Another approach is collaborative filtering, which predicts ratings based on user-item interactions. The idea is that users who gave similar ratings to some movies will give similar ratings to other movies; the same can be said about similar movies receiving similar ratings from similar users.
- Of course, we can combine both, which is called the hybrid approach. I'll use collaborative filtering in this project because 1) it doesn't require a lot of information about movies or users but 2) it usually makes high-quality predictions.
{{< /speaker_note >}}

---

### Matrix Factorization

- SVD: $R = M\Sigma U^{T}$ ($R$: user-item matrix; $U$: user-feature matrix; $U^{T}$: item-feature matrix transposed; $\Sigma$: diagonal matrix for scaling)

<img src="/img/mf.png" align=top width="350" hspace="-10" />

- [SVD++](https://www.quora.com/Whats-the-difference-between-SVD-and-SVD++) also exploits implicit ratings: Users prefer rated items to random unrated ones

{{< speaker_note >}}
- More specifically, I'll use matrix factorization to implement collaborative filtering. It's an algorithm inspired by singular value decomposition (or "SVD"), which factorizes the user-item matrix into 3 smaller matrices: A user-feature matrix, a transposed item-feature matrix, and a diagonal matrix for scaling. We can use stochastic gradient descent to find factorization that minimizes predictor errors on ratings that we already know. 
- SVD++ enhances SVD by exploiting implicit ratings, that is, whether a user rated a movie or not. The idea is that users prefer rated items than random unrated items. SVD++ is the algorithm that won the famous Netflix competition. 
{{< /speaker_note >}}

---

## Data Splits
#### 20% validation 
#### 60% training
#### 20% test

Built with the [`Surprise`](http://surpriselib.com/) library 

{{< speaker_note >}}
- I implemented SVD++ using the Python library "Surprise", which is super popular for building recommender system.
- I split the whole dataset into 3 parts and used 20% of the data for hyperparameter tuning, 60% for training, and 20% for testing the trained model.
{{< /speaker_note >}}

---

### Tuning

- Find the optimnal learning rate $\gamma$ (`lr_all`) and regularization term $\lambda$ (`lr_reg`) for SVD++

```
# Define the hyperparameter space
param_grid = {"lr_all": [0.005, 0.01], "reg_all": [0.02, 0.1]}
# Find an SVD++ estimator that minimizes RMSE
gs = GridSearchCV(SVDpp, param_grid, 
                  measures=["rmse"], n_jobs=-1, 
                  cv=3)
gs.fit(validation)
# This is the best SVD++ estimator
algo = gs.best_estimator["rmse"]
```

{{< speaker_note >}}
- First of all, SVD++ has several hyperparameters, including the learning rate $\gamma$ for gradient descent and a regularization term $\lambda$.
- I used grid search to find which hyperparameter combination results in the smallest root-mean-square error (or "RMSE") when predicting ratings in the held-out data during 3-fold cross-validation.
{{< /speaker_note >}}

---

### Training

- Use the best SVD++ estimator we just found to fit the training data

```
algo.fit(train)
```

- Predict user ratings in the test data with the trained algorithm 

```
predictions = aglo.test(test)
```

{{< speaker_note >}}
- Then I used the tuned SVD++ to fit the training data and predicted user ratings in the test data using the trained model.  
{{< /speaker_note >}}

---

## Evalution
### Is the recommender any good?

{{< speaker_note >}}
- How can we know if the recommender system we just built is any good? Unlike your typical regression or classification problems, the answer is not that straightforward.
- Ideally, we can ask users if they like our recommendations or not. However, before deloying the recommender system, we won't have such data. However, there are several ways to evaluate a recommender system without user feedback.
{{< /speaker_note >}}

---

## Accruacy

- Overall accuracy: **RMSE**
- Accuracy for "relevant" items (e.g., rated 3.5 stars or above)
  - Mean Average Precision@K (**MAP@K**): On average, out of items recommended to each user, how many are relevant
  - Mean Average Recall@K (**MAR@K**): On avergae, out of items relevant to each user, how many get recommended
  

{{< speaker_note >}}
- For instance, we can look at whether the recommender predicts user ratings **accurately** by comparing actual ratings with predicted ratings. Accuracy can be measured by root-mean-square error (RMSE).
- For recommender systems, however, the overall accuracy doesn't matter as much as accuracy for top-rated items. After all, mediocre items may never get recommended. We can set a threshold such as 3.5 stars and consider items with ratings lower than this irrelevant. For each user, we can compute out of items recommended to them, how many are relevant. This is "Precision @K". We can also compute out of relevant items, how many get recommended, which is "Recall @K".
- By averaging these metrics acorss all users, we get "Mean Average Precision@K" and "Mean Average Recall@K".
{{< /speaker_note >}}

---

## Diversity

- Intra-list similarity (**ILS**): consine similarity of movies recommended to the same user, averaged across all pairs of items

$$\mathrm{ILS_{user}} = \frac{1}{2}\sum_{i_j\in L}\sum_{i_k \in L}\mathrm{sim}(i_j, i_k)$$

- We can average ILS across all users to measure the diversity of the entire system

{{< speaker_note >}}
- However, it takes more than accuracy to make good recommendations. For instance, if a user likes the first TLOR movie, it's safe to say that they like the rest but recommending 3 TLOR movies is pretty boring.
- Another question we can ask about a recommender system is if it makes diverse recommendations. To quantify diversity, we can compute the average cosine similarity among movies recommended the same user. The higher the intra-list similarity, the lower the diversity.
{{< /speaker_note >}}

---

## Personalization

- **Personalization**: dissimilarity (1 - cosine similarity) between different recommendation lists, averaged across all pairs of lists

$$\mathrm{Personalization} = 1 - \sum_{u_i\in U}\sum_{u_j\in U} \mathrm{sim}(L_{u_i}, L_{u_j})$$

{{< speaker_note >}}
- A "lazy" recommender may just recommend the same set of highly rated movies to everyone. We can ask if a recommender system makes personalized recommendations **personalized** for different users. 
- "Personalization" is quantified by the dissimilarity between lists of movies recommended to different users.
{{< /speaker_note >}}

---

### Evaluation

- Baseline model (`NormalPredictor`): Predicts a random rating based on the distribution (assumed to be normal) of the training set

{{% fragment %}}
  <figure>
    <img src="/img/eval.png" align=bottom width="800" />
  </figure> 
{{% fragment %}}
SVD++ outperforms the baseline in all but Personalization (extremely high for both)
{{% fragment %}}

{{< speaker_note >}}
- None of these metrics by themselves tells us whether a recommender system is good or bad. To know that, we can compare our sophisticated SVD++ to a baseline algorithm that generates random predictions based on the rating distribution in the training data.
- As we can see, SVD++ outperforms the baseline in almost everyway except Personalization, which is high for both models.  
{{< /speaker_note >}}

---

# Part II
## Extend to Groups

{{< speaker_note >}}
- The next step is to extend the regular recommender system to groups. 
{{< /speaker_note >}}

---

### Merging profiles 
- Merge all users' profiles into a single one: e.g., Alice {TLOR: 5, The Matrix: 3}, Bob {TLOR: 4, Midsommar: 5} → merged {TLOR: 4.5, The Matrix: 3, Midsommar: 5}
- Add the new pseudo profile to the original data and retrain SVD++ on the combined data
- Recommend top N movies to this pseudo user

{{< speaker_note >}}
- As you can imagine, there are two ways to do this. 
- First, we can merge the profile of each user in the group into a single one. For instance, the merged profile of Alice and Bob will include all the movies they each rated. If one movie was rated by more than one user, then we take the average.
- Since this new pseudo user is not in the system, we need to add it to the original user-item matrix. After that, we retrain SVD++ on the combined data, find new predictions for the pseudo user, and recommend top N movies to them.
{{< /speaker_note >}}

---

### Example

- Recommend movies for a group of 3 (UID = 217, 13, 7) by merging users' profiles 

```
# Enter ID of each user in the group
group = form_group()
# Create a pseudo user by merging profiles
average_user = average_profile(data_df, group)
# Predict the new pseudo user's rating
new_user_rating = new_rating(data_df, average_user, [999])
# Recommend movies based on predicted ratings
generate_rec(new_user_rating, "predicted_rating")
```

<img src="/img/profile_merging.png" align=bottom width="500" />

{{< speaker_note >}}
- Here's an example using this approach. First, each user enters their ID, which is used to retrieve their profile. 
- The group can specify how many recommendations they want (e.g., 5) and the recommender system will print out 5 recommendations for this group.
{{< /speaker_note >}}


---

### Merging recommendations

Make predictions for each user in the group:

<img src="/img/group_rating.png" align=bottom width="600" />

- **Average:** group rating = average rating 
- **Least misery:** group rating = minimun rating 
- **Average-without-misery**: filter out movies outside of each user's top 1% predicted ratings  → group rating = average rating across users

{{< speaker_note >}}
- Alternatively, we can merge users' predicted ratings and make recommendations based on group ratings. 
- Group ratings can just be average ratings across users. However, if one user gave a low rating to the chosen movie with a high average rating, they may have to suffer through the movie night. To avoid "misery", we can assign minumun ratings to be group ratings. However, this doesn't take account of other users' happiness.
- To take advantage of both methods, we can use "average-without-misery" to aggregate ratings: First, we can select only movies that are in each user's top 1% predicted ratings to avoid "misery"; then, we can use average ratings as group ratings. 
{{< /speaker_note >}}

---

### Example

- Recommend movies for a group of 3 (UID = 217, 13, 7) by merging each user's predicted ratings using "average-without-misery" 

```
# Score = group rating × how many times a movie is in top 1%
mwm_rating = mean_without_misery(individual_ratings)
# Make recommendations based on scores
generate_rec(mwm_rating, "score")
```

<img src="/img/rec_merging.png" align=bottom width="800" />

{{< speaker_note >}}
- Here's an example using average-without-misery to recommend for the same group. 
{{< /speaker_note >}}

---

## What about new users?

{{< speaker_note >}}
- As is often the case, not everyone in the group is an existing user in the system. How do we recommend for a group consisted of new users?
- Apparently, it's hard to make recommendations for new users because we know nothing about their preferences. This is known as the "cold-start problem".
{{< /speaker_note >}}

---

### Overcome the "cold-start"

- Ask each new user to rate 20 movies (narrowed down by genre, e.g., "Horror")
  - Popularity: great for connecting users
  - Entropy: informative for learning tastes
<img src="/img/HELP.png" align=bottom width="550" />
  - Questions are chosen from 100 movies with highest "HELP" (harmonic mean of entropy and $\log$ frequency)

{{< speaker_note >}}
- To overcome this problem, we need to learn each new user's preference by asking them to rate, for instance, 20 movies. 
- It's crucial how we choose these movies. We want them to be somewhat popular so we can connect new users to existing users. However, super popular movies tend to be universally acclaimed and therefore tell us nothing about a user's unique taste. To mend for that, we can ask new users about controversial movies with high entropies in terms of their ratings. However, controversial movies tend to be obscure.
- As a compromise, we can ask about movies with the highest harmonic mean of entropy and $\log$ frequency.
{{< /speaker_note >}}

---

### Example
- Each group member rates the same 20 movies

```
# Randomly select 20 questions from the pool to ask
question_list = random.sample(question_pool, 20)
# Get each user's ratings on these movies
group_ratings = new_group(question_list)
```

<img src="/img/new_user.png" align=bottom width="600" />

{{< speaker_note >}}
- Here's an example of making recommendations for a group of new users.
- First, each group member will rate the same set of 20 movies. Then we can either merge profiles or recommendations.
{{< /speaker_note >}}

---

### Example
- Then we average their profiles, retrain SVD++, and recommend for the new pseudo user

<img src="/img/new_profile.png" align=bottom width="800" />

{{< speaker_note >}}
- Here's are the recommendations based on profile merging.
{{< /speaker_note >}}


---

### Example
- Or we predict each user's ratings, merge predicted ratings ("average-without-misery"), and recommend movies with top group ratings

<img src="/img/new_recs.png" align=bottom width="800" />

{{< speaker_note >}}
- Here's are the recommendations based on recommendation merging using average-without-misery.
{{< /speaker_note >}}

---

### Summary 
- **Product**: A prototype group movie recommender system that can learn preferences of new users and recommend movies of certain genre for them as a group
- **End users**: Stand-alone application or part of a streaming service (e.g., Netflix, Hulu, Amazon Prime Video, etc.) for a group of users who want to watch a movie together

{{< speaker_note >}}
- To sum up this project, I built a movie recommender system for an arbitrary group of users. Each group member can be an existing user or a new user. Further, they can choose to receive movie recommendations of any genre or a specific one. 
- This is only a prototype. In the future, a group movie recommender like this can either be a stand-alone app or an integrated part of a streaming service (e.g., Netflix, Hulu, Amazon Prime Video, etc.).
{{< /speaker_note >}}

---

## Extending this work

- Enrich the recommender by adding user/movie features and using hybird filtering
- Train on the larger version of MovieLens with 25 million ratings (using Spark)
- Deploy the group recommender as a web app (e.g., using Flask + Heroku)

{{< speaker_note >}}
I plan to extend this work in several ways:
- As mentioned before, we can combine user-item interactions with user/item features to enrich the recommender system. 
- Due to running time concerns, I trained SVD++ on the smallest version of the MovieLens data. In the future, I can use Spark to scale up the system so we can train the algorithm on larger rating data, like the version with 25 million ratings. 
- Last but not least, to make the app accessible to users, I plan to deploy it as a web app, potentially using Flask and Heroku.
{{< /speaker_note >}}

---

# Questions?

[Email](yuan_meng@berkeley.edu)

[LinkedIn](https://github.com/Yuan-Meng/COVID-19)

{{< speaker_note >}}
- Thanks for listening! I'm happy to answer some questions!
{{< /speaker_note >}}
