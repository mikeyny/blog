---
layout: post
section-type: post
comments: true
title:  "How to start a movement using a twitter bot"
category: tech
tags: [ 'python','programming','bots','social media' ]
---
## BOTS ,BOTS ,BOTS

![image](http://static.wixstatic.com/media/433ed0_bdd1602c3e487168aab17ff4493a20e4.jpg/v1/fill/w_442,h_180,al_c,q_80,usm_0.66_1.00_0.01/433ed0_bdd1602c3e487168aab17ff4493a20e4.jpg)

So lets face bots are taking over, they are on all major social media sites Facebook, Telegram, Slack and Twitter. Even Whatsapp which is against having bots on its platform is filled with bots with a vast number of services ranging from giving sports updates to conversational A.I bots to web-browsing.

To all those a bit lost here, a bot is just software developed to automate tasks you would normally do on your own like checking game scores, making dinner reservations ,fetching or displaying information.Bots have been around for a long time(about 50 years now) but they have only become famous now due to advancements in A.I, a rise in RESTful APIs and their integration onto the social media platform.

### MY TWITTER BOT

![twitter bot image](http://justsimplyoutsourcingworldwide.com/wp-content/uploads/2013/08/robot-icon-twitter-featured.jpg)

In this tutorial I will show you how to make a simple twitter bot using python that re-tweets everything on a certain topic on #hashtag.

Hmmmm ,but whats the point of a it mindlessly retweeting posts ?

Glad you asked ,It can be used to promote certain events or news across a wider audience. People can use this to receive updates on a particular topic, instead of the original poster on Twitter as they are only interested in specific Tweets and not everything that user has to say. People can use the hashtag ReTweet bots to follow the hashtag within their stream, so they don’t have to search for it.You can use this bot to promote your business or support a movement or an organisation using a particular hashtag. A live implementation can be found here [A Bot has no name](https://twitter.com/thisflag_zw) , the bot Re-tweets everything with the hashtag #ThisFlag ,a movement against corruption in Zimbabwe.

### NOW TO THE FUN STUFF !!!

First thing is first , head to twitter and create a new app, details on how to do that can be found here [Create a twitter app](http://iag.me/socialmedia/how-to-create-a-twitter-app-in-8-easy-steps/) .Make sure the application has both read and write access in step 8.

You'll need to generate and copy your:

* OAUTH_TOKEN
* OAUTH_SECRET
* CONSUMER_KEY
* CONSUMER_SECRET

we will need them later

Although the are many twitter libraries for python, in this tutorial we will be using [Tweepy](http://www.tweepy.org/) an easy-to-use Python library for accessing the Twitter API.

First head over to your console and install tweepy using

```
pip install tweepy
```

Next lets import it

```python
# import the necessary libraries
import tweepy

```
Now we will define all necessary variables for the script

```python
# define the necessary variables

# The hashtag or search term to retweet
hashtag = ""

#tweet language ,you can leave it blank for all languages
tweetLanguage = ""

# Number of tweets to retweet at a time (Twitter has a limit of 180 requests per every 15 mins)
num = 

#Your twitter app consumer key
consumer_key=""

#Your twitter app consumer secret
consumer_secret=""

#Your twitter app access_token
access_token=""

#Your twitter app access_token_secret
access_token_secret=""

```
Setting up tweepy is very is simple ,all we have to do is specify our keys

```python
# Setting up tweepy
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth)

```

Now its time to make our code actually do something useful ,the following snippet queries twitter using our hashtag

```python
# search query
timelineIterator = tweepy.Cursor(api.search, q=hashtag, lang=tweetLanguage).items(num)

# put everything into a list to be able to sort/filter
timeline = []
for status in timelineIterator:
    timeline.append(status)
```
Finally we loop through our search results and retweet them one by one.

```python
tweet_counter = 0
error_counter = 0

# iterate the timeline and retweet
for status in timeline:
    try:
        print("(%(date)s) %(name)s: %(message)s\n" % \
              {"date": status.created_at,
               "name": status.author.screen_name.encode('utf-8'),
               "message": status.text.encode('utf-8')})

        api.retweet(status.id)
        tweet_counter += 1
    except tweepy.error.TweepError as e:
        # just in case tweet got deleted in the meantime or already re-tweeted
        error_counter += 1
        # print e
        continue

print("Finished. %d Tweets re tweeted, %d errors occurred." % (tweet_counter, error_counter))
```
And thats it save, your code and run it ,and watch the magic.


For a further advanced and more re-usable version of this code, checkout my repository [here](https://github.com/mikeyny/retweet-bot)


#### **DISCLAIMER**

The above code is my python3.5 implementation of github user basti2342 's [retweet-bot](https://github.com/basti2342/retweet-bot)




