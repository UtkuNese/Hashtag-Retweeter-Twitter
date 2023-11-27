import tweepy
import time

# Twitter API keys
consumer_key = 'your_consumer_key'
consumer_secret = 'your_consumer_secret'
access_token = 'your_access_token'
access_token_secret = 'your_access_token_secret'

# Configure Tweepy API
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth)

# Hashtag to follow
target_hashtag = '#python'

def retweet_new_tweets():
    # Create a file to check the last retweet ID
    try:
        with open('last_retweet_id.txt', 'r') as file:
            last_retweet_id = int(file.read().strip())
    except FileNotFoundError:
        last_retweet_id = None

    # Fetch new tweets
    tweets = api.search(q=target_hashtag, count=10, result_type='recent', since_id=last_retweet_id)

    # Retweet new tweets
    for tweet in reversed(tweets):
        try:
            # Retweet the tweet
            api.retweet(tweet.id)
            print(f"Retweeted: {tweet.text}")
            
            # Update the last retweet ID
            last_retweet_id = tweet.id
            with open('last_retweet_id.txt', 'w') as file:
                file.write(str(last_retweet_id))
            
            # Wait for a while to reduce the risk of exceeding API limits
            time.sleep(5)

        except tweepy.TweepError as e:
            print(f"Error: {e.reason}")

if __name__ == "__main__":
    while True:
        retweet_new_tweets()
        # Periodically check by waiting for a specific duration
        time.sleep(300)  # For example, 5 minutes
