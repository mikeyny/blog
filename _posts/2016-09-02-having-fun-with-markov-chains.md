---
layout: post
section-type: post
comments: true
title:  "Creating your own horse _ebooks using python and markov chains"
category: tech
tags: [ 'python','programming','bots','social media','markov chains' ]
---
## Horse _ebooks ?

![image](https://pbs.twimg.com/profile_images/1096005346/1_400x400.jpg)

So ever since my last blog post [How to start a movement with a twitterbot](https://mikeyny.github.io/tech/2016/07/30/twitter-bot.html) , I have been obsessed with bots. Over the past few weeks, I have hacked around with bots for twitter , messenger and reddit. I have seen a lot of great bots including [Smart Notes Bot](https://www.messenger.com/t/SmartNotesBot/), [Dear Assistant](https://twitter.com/DearAssistant),[Every Word](https://twitter.com/everyword),[Remind Me Bot](https://www.reddit.com/user/RemindMeBot) to name a few but when I came across [Horse _ebooks](https://twitter.com/horses_ebooks) I was a bit puzzled. The tweets composed by this bot were both wonderful and confusing ,implying a certain hidden deep meaning, not at all something you would expect from a bot.

The bot ,which has since gone offline ,had over 200 000 followers on twitter. It also became the inspiration for fan art, fan fiction, and unofficial merchandise. Among these are T-shirts and Horse_eComics, a [Tumblr blog](http://horseecomics.tumblr.com/) featuring comic strips inspired by the account.

Horse_ebooks was named one of the best Twitter feeds by UGO Networks in 2011 and Time.com in 2012.Some of its popular tweets include.

![image](https://www.dropbox.com/s/vy2dr7qxgge0dbv/horse_1.jpg?dl=1)

![image](https://www.dropbox.com/s/wilqn10as402mim/horse_2.jpg?dl=1)

![image](https://www.dropbox.com/s/rwiwy97xdkn7qw2/horse_3.jpg?dl=1)

So immediately I set out to find out how it was done. The creator of the bot had fed a large corpus of text from an ebook website into a markov chain program which would generate random sentences and post them as tweets. Sounds simple, right ? ,but what on earth is a markov chain ? 

Well according to [Wikipedia](https://en.wikipedia.org/wiki/Markov_chain) **a markov chain is a random process that undergoes transitions from one state to another on a state space. It must possess a property that is usually characterized as "memorylessness": the probability distribution of the next state depends only on the current state and not on the sequence of events that preceded it.**
Now unless you are an Applied Maths major , I'm pretty sure that sounds like gibberish. Thankfully I found this [Article](http://agiliq.com/blog/2009/06/generating-pseudo-random-text-with-markov-chains-u/) ,it explains the concept of markov chains in text generation beautifully.

If still not satisfied check out this video.

<iframe width="560" height="315" src="https://www.youtube.com/embed/56mGTszb_iM" frameborder="0" allowfullscreen></iframe>



### MY _EBOOKS TWITTER BOT

![twitter bot image](http://justsimplyoutsourcingworldwide.com/wp-content/uploads/2013/08/robot-icon-twitter-featured.jpg)

In this tutorial, I will run you through how to make your own _ebooks twitter bot in just 10 lines of code.

A live implementation can be found here [Quotes _Ebooks](https://twitter.com/quotes__ebooks) ,this bot uses a markov chain to generate quotes based on a corpus of quotes by famous individuals including Gandhi, Steve Jobs, Adolf Hitler, Bill Cosby to name a few.

### NOW TO THE FUN STUFF !!!

First thing is first of all head to twitter and create an account for your bot. Now head over to <https://apps.twitter.com/> and create a new app, details on how to do that can be found here [Create a twitter app](http://iag.me/socialmedia/how-to-create-a-twitter-app-in-8-easy-steps/) .Make sure the application has both read and write access in step 8.

You'll need to generate and copy your:

* OAUTH_TOKEN
* OAUTH_SECRET
* CONSUMER_KEY
* CONSUMER_SECRET

we will need them later

I already went and setup everything needed for this tutorial ,the files are available in [my github repo](https://github.com/mikeyny/_ebooks_bot) ,so head over and download the files or fork yourself a copy.

The repository includes 

secrets.py - add your app tokens and keys here.

Profile   - Required to upload our files to heroku. It defines which files we will be running on heroku.

Text - A folder containing many text sample text files to be used as our corpus ,for the tutorial I used jokes.txt which is extracted from **Jokes For All Occasions By EDWARD J. CLODE**
You can also use your own custom text file ,a large collection can be found at [Project Gutenberg](http://www.gutenberg.org/) 

requirements.txt - lists all external libraries used in our project.

bot.py - Our main project file which generates the random sentences using a markov chain and then tweets that to our bot account.

## Explaining our code.

First and foremost the import statements

```python
# Import all necessary libraries
import markovify ,tweepy ,io

# Import our app secrets form secrets.py
from secrets import *
```
Now we set up tweepy to communicate with our app

```python
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)

```

Now we have to read our file and build the markov-chain model and use that to generate out tweet

```python
# open our file
with io.open("Text\jokes.txt", encoding="utf-8") as f:
    text = f.read()

# Build the model.
text_model = markovify.Text(text)

# generate a random sentences of no more than 140 characters(a tweet)
message =text_model.make_short_sentence(140)

```

Finally, post our tweet to twitter

```python
#post your tweet
api.update_status(message)
```


## Running our code locally

Running the code is as simple as pie ,first head of to the command line and run

```

pip install -r requirements.txt

```

this command installs all of our scripts' dependencies.

Now to run the actual script ,just open your command line and type 
    
```
python bot.py

```

**Make sure you copied your app secrets to secrets.py .**


## Running the code on Heroku

Now unless your computer is always on and connected to the internet ,running the code locally is not practical. The best method is to upload your code to heroku and let it run periodically from the cloud. Heroku has a free and paid plan, the free plan offers dyno hours (time for running your app) ,which is perfect for our bot.

Go to [Heroku]() and create an account ,then heard over to the apps section and create a new app. Heroku provides simple instructions to upload your code to their servers ,either from github ,dropbox or locally from your computer. In this tutorial, I'll assume we are uploading the code from our computer. To do these your need [git](https://git-scm.com/downloads) and [Heroku toolbeit](https://devcenter.heroku.com/articles/heroku-command-line#download-and-install) installed.

Open up your terminal and navigate to the project directory and input the following commands

```
heroku login             # login to your heroku account via the terminal

git init                  # creates a git repository in your current working directory

heroku git:remote -a <myappname>     # links your git repo to the heroku app

git add .                 # adds all files in the folder to our git repository

git commit -am "first commit"   # commits all the files added to our git repository

git push heroku master          # pushes our code to heroku

```

Now go to the resources section of your app in the web interface and make sure the worker is turned on.

![image](https://www.dropbox.com/s/phyozz8w5k79drq/worker.jpg?dl=1)

That's it, your twitter app should now be automated, and posting hilarious, weird, amazing and puzzling tweets. If you run into any errors just run


```
heroku logs -t
```
and debug using google and stackoverflow.

To make your app tweet at certain intervals (every 15 /30 mins) go to add-ons and add a scheduler .

Here are some sample tweets from my bot [@quotes__ebooks](https://twitter.com/quotes__ebooks)

![image](https://www.dropbox.com/s/hcusznn6l8ozbdf/quotes_1.jpg?dl=1)

![image](https://www.dropbox.com/s/2s12lej1mja9vak/quotes_2.jpg?dl=1) 







