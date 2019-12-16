# Board-Game-Rec-Sysem
Recommends board games based on user scores

## Import Packages
Imported surprise to build the recommender and scikit-learn to obtain metrics for the recommender.

## Preparing Data
I obtained a kaggle dataset with over 13 million unique boardgame reviews, with each row containing a user, a game, and a user score for the game (1-10). To make the data more computationally feasible I randomly sampled 0.3% of the data and ended up with 7112 unique games and 29588 unique users.

## Building the Model
I used singular value decomposition (SVD) to predict user scores. After splitting my data into a train and test set, I fit the model using the train set and was able to obtain a root mean squared error 1.48 when predicting the scores of the test set.

I built a function which takes in a user name and predicts a user score for all the games that that user has not played and returns a top 5 list of games where the predicted score is the highest. I also wanted to be able to account for new users who haven't rated any of the games yet, so I built another function that takes in a new user name, a data set, and the number of games he wishes to score. The function randomly selects a game and allows the user to either skip or rate the game. After the specified number of games has been rated the function outputs a list the selected games along wih their inputed ratings so that they can easily be added to the model so that my first function can return recommendations for the new user.

In order to improve the performance of my model and recommendations, I cut out all users who rated less than 5 to make the data less sparse. I also performed a gridsearch to pinpoint the optimal parameters I should be using for my SVD model. After making these changes my RMSE was slightly reduced to 1.47.

Lastly I created and item based recommendation system using K nearest neighbors. This model was able to ahcieve an RMSE of 1.58 when predicting the user scores of the test set. More importantly, this model is able to return recommendations based on a game, instead of a user. I created a function that takes in a game and the number of desired recommendations. The function uses the K nearest neighbors algorithm to return the specified number of games that are most similar to the inputed game. 
