---
layout: post
title: Metis final project - Fishing for Retweets
published: True
---

I presented my final project at Metis last thursday.  I talked about using ML to increase the chance that a famous newscaster would retweet me.  This post is a work in progress.

Here are my [slides](/assets/fishing_retweets/twitter_metis_ajs.pdf).


## Motivation

I set out to build a model that would tell me what tweets were likely to get retweeted by specific people.  I did not think there would be enough data about most individual users (except maybe Marc Andriessen) to train a model, so I would need to train a model to target a group of users that are presumed to have similar behavior.  I targeted political journalists because they're the gorup I'm most interested in interacting with on twitter.  My twitter feed consists of politics and hockey, and hockey players are not very interesting people [in conversation](https://www.youtube.com/watch?v=07r8UfdCphA).

I focused on Don Lemon in particular because I like the guy, and because his twitter profile describes him as a "Twitter King". I have been monitoring the twitter traffic of a lot of people for a few weeks, and I beg to differ.  Donald John Trump is the king of Twitter, all others are pretenders.

## Data

I collected the twitter activity around 108 political reporters and journalists.  I got most of the names from the list [here](http://www.politico.com/blogs/media/2015/04/twitters-most-influential-political-journalists-205510), which included 105 names categorized as "Left", "Center", or "Right", and added a few names of my own (Harry Enten, Mike Pesca, Julia Ioffe, and Wikileaks).  Andrea Tantaros is on the list, but I had to leave her out because her account is private.

I collected each users' tweets (including quotes, replies, and retweets), and tweets that mentioned them.  The users' quotes, replies, and retweets were the tweets I was most interested in, because these represent interactions with other users.  The tweets mentioning them were my control group, because they were cases where someone started an interaction that was not (usually) reciprocated.  Many of the users I tracked got so many mentions that I was not able to collect all of them.  Instead, I collected 100 tweets every hour.  I was able to estimate the overall rate by seeing how long it took to get 100 tweets.  This method gave me hourly and overall estimates of the rates, and I used these estimates to determine the overall probability that each user reacts to a tweet at them.  You can see an example of this analysis [here](https://github.com/alanjschoen/kojak/blob/master/Time%20Histogram.ipynb).

{% include image_topcaption_tall.html url="/assets/kojak/lemon_time_ratio.png" description="The best times of day to tweet at @donlemon" %}





