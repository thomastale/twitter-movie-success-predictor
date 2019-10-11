# Twitter-Movie-Success-Predictor

## movie data scraper
Used BeautifulSoup4 to parse online movie database for movies from 2015-2018. <br>
Chose most recent years to try to offset any inflation in tweets from growth in number of Twitter users.
Got movie title, opening weekend revenue, theaters (released in), and date released.

## twitter data scraper

### tweets, likes, retweets
Used a library called GetOldTweets3 to scrape twitter for tweets, likes and retweets containing the movie title 
between a certain range of dates.
Free Twitter API and tweepy only allow for scraping from all of twitter to 7 days prior.
(Allows for unlimited scraping from one user's timeline though).

### average tweet sentiment
Parsed the actual content of the tweets from all the tweets containing the movie title. 
Split all the words up, removed all stopwords (and, or, if, but, etc) and the movie title itself.
From all the tweets' parsed words, found the top 10 most occuring words.
Of these top 10 words, performed a sentiment analysis on each 
to get a polarity value (-1 being negative and +1 being positive) and then averaged them all together
to get a final sentiment value for that movie.

### loop
Looped through the box office csv I scraped earlier, scraping through the 
tweets, likes, retweets, and average tweet sentiment for each movie. For movies with one word titles, the title includes both itself and it's hashtagged version in the search.<br>
Example: Deadpool and #Deadpool<br>
The name deadpool is within the #deadpool the tweets with #deadpool and not deadpool are included. <br><br>
For movies with multiple words in the title, the scraper had to be run twice. The first scrape includes the 
movie title as it is, wheras the second scrape queries tweets with the movie title converted to a hashtagged form.<br>
Example: Finding Dory for 1st Scraper, and #findingdory for 2nd Scraper 

### side note on hashtags vs regular form of movie title
Ran a short script with 4 different movies and all were found to have 80% of total tweets regarding the movie to not use a hashtag
just the regular form. However, the remaining 20% that used hashtags were found to have a higher total percentage of
likes and retweets 30%+. <br>
Hypothesis as to why is that influencers, celebrities, and official accounts are more likely to use hashtags
as a form of promotion rather than average twitter users informing their social circles about their lives.

### limitations
Due to a limit in processing power of my personal computer, the tweet analytics only reflect one day's worth of data
for each movie. (the day one month before release of each respective movie was what I chose in this particular instance)
With only one day's worth of data, fluctuations due to Social Media Manager's release schedule, day of the week, viral videos,
and another number of variables could skew the twitter data significantly.
<br><br>
Ideally 30-180 days worth of tweets about the movie (prior to release date) would gather enough data to better 
make predictions.

## movie success predictor
### initial conclusions
Cleaned up data and combined dataframes for the box office data and the scraped twitter data.
Ran high level metrics and scatter plots to see if any individual tweet analytic had a major effect on revenue.
Conclusions: it didn't (refer to limitations section above).

### linear regression and ML models
Set up the target value as Opening Weekend Revenue and features as tweets, likes, retweets, and average sentiment.
Ran the data through 5 different machine learning models. Results were very poor, with the best MAE around $21 million, with
mean movie opening weekend revenue was $30 million (refer to limitations above).
