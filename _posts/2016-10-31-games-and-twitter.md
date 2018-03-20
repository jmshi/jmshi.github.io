---
id: 270
title: games and twitter
date: 2016-10-31T01:05:01+00:00
author: jiming5_wp
layout: post
permalink: /games-and-twitter/
image: /wp-content/uploads/2016/10/bird_nest.png
categories: Data Science
---

# 1. Introduction
### Motivation:
<img class="size-medium wp-image-273 alignright" src="/assets/bird_nest-300x300.png" alt="bird_nest" width="400" height="400" srcset="/assets/bird_nest-300x300.png 300w, /assets/bird_nest-150x150.png 150w, /assets/bird_nest.png 420w" sizes="(max-width: 400px) 100vw, 400px" />Along with the explosion of popularity of mobile devices, mobile games also become more and more popular nowadays. From retro games such as Plants vs. Zombies and Flappy Bird to more recent multiplayer games such as Clash of Clans and Pokemon Go, there are a variety of them which all made big success but with very different strategies.Investigating how popular they are and what make them popular or not would bring instructional information which is invaluable to determine a better short/long term plan of their product and service. 
   
Text mining via social media such as Twitter comes in handy in this kind of task. As Twitter data constitutes a rich source of information about any topic imaginable, they can be used to find trends related to a specific keyword, measuring brand sentiment, and gathering feedback about new products and services.

In this proposal, I will demonstrate the possibility to use Twitter to (1) make very efficient and productive survey in the mobile game business, and (2) perform detailed analysis on given product (here use Pokemon Go as an example) to find out important information such as hot terms/topic, product usage patterns, and the customer sentiment of the product.
         
### Methods/Tools:
I use <a href="https://dev.twitter.com/streaming/overview">Twitter Streaming API</a> together with Python libraries such as <a href="http://www.tweepy.org/">$\texttt{Tweepy}$</a> and <a href="https://pypi.python.org/pypi/twitterscraper">$\texttt{twitterscraper}$</a> to collect user information and relevant tweets (in the past 1-2 weeks) about certain set of popular mobile games. Use Natural Language Processing libraries such as $\texttt{NLTK}$ to find keywords which characterize the game, and use $\texttt{matplotlib}$ and $\texttt{Vincent}$ to render plots.
 
    

# 2. Data collection
For the popularity survey, I first use Twitter Streaming API together with Python libraries to extract user information, such as number of followers, created time, and number of likes, from the official twitter account of a list of 14 most popular mobile games, based on internet reviews in 2015 and 2016.

I then collect all tweets that are related to each game in the past week (Oct-23 to Oct-29, 2016) using web scraping library twitterscraper. This results in about 120K tweets in total.
 
In order to perform more detailed study of a given mobile game, I pick the most popular game Pokemon Go as an example, and expand the data set to include all tweets within the past two weeks. That gives a total tweets count about 120K for Pokemon Go alone.
         
# 3. Popularity Survey
## 3-1. user information from official account
One way we can get an easy measurement of if a game is popular or not is to pull out some information associated with its official twitter account, such as the number of followers and number of likes. Normally, a more popular game would be garnished with more followers and more likes. However, cautions are needed as not every twitter user who plays a particular game would follow its official account on twitter.

The following plot shows total number of followers to-date of a list of 14 popular mobile games (list based on internet reviews in 2015 and 2016):
There are two winners: *Clash of Clans* and *Pokemon Go*, both have followers more than 2 millions, which clearly shows both are or were very popular games (follower number only goes up with time, so there is a bias toward games with longer time spans.)

<img class="size-medium wp-image-273 aligncenter" src="/assets/followers.png" alt="followers" width="400" height="300" />
           
        
In order to show the bias, or extract a unbiased analysis, we here plot number of followers (left) and number of days of the game&#8217;s lifetime (right) together. Note Pokemon Go only released this June, but the official account was registered in 2014 which is when that game is conceived.
Both <strong>Clash of Clans and Pokemon Go</strong> have a lifetime close or below the average ages of the list of games we considered. However their follower counts are exceptional, clearly indicate their popularity in recent years. Especially for Pokemon Go, it shows a strong momentum to keep its popularity.
          
<img class="size-medium wp-image-273 aligncenter" src="/assets/followers_days.png" alt="followers" width="400" height="300" />
           
On the other hand, number of likes might not be a good indicator of a game&#8217;s recent popularity. Some games gained more likes due to their longevity, such as angry birds and Plants vs Zombies. Some popular games such as Pokemon Go gains less likes partly because of its very young age. One exception is Ingress, a location based, multiplayer online game, a relative of Pokemon Go. It attracts the third highest number of likes within a time span less than the averaged lifetime of the games in the list.
<img class="size-medium wp-image-273 alignright" src="/assets/likes_days.png" alt="followers" width="400" height="400" />


## 2.2 tweets count

Another way to measure the popularity of a game is by counting how many times twitter users mentioned the game. I therefore scrapped the tweets on the web within the past week for the following six games: Candy Crush, Clash of Clans, Flappy Bird, Plants vs Zombies, Subway Surfers, Pokemon Go. 
    
    
The following plot shows the number of tweets that mentioned individual game in the past week.
* It is not surprising to see Pokemon Go alone hits 70K tweets,while the rest of five combined only gives 10K.

It indicates that,        
* 1) overall Pokemon Go is the most dominant mobile game based on social media , or
* 2) Pokemon Go players tweet much more often (almost 100 times) than other game players do
        
although the second might not be so likely. Further study with data over longer time span, and/or get user information might be very useful to tell. <strong>In any rate, Pokemon Go does a great job to get its players excited indicated by the huge amount of tweets over a relatively short period of time.

<img class="size-medium wp-image-286 aligncenter" src="/assets/barchart-248x300.png" alt="barchart" width="248" height="300" srcset="/assets/barchart-248x300.png 248w, /assets/barchart.png 309w" sizes="(max-width: 248px) 100vw, 248px" />
      
# 3. Pattern of usage
## 3-1. weekly pattern
Before we move on to the text content, lets do a histogram of total count grouped by days of week. For this and following study, I have doubled the data size which now spans over the past two weeks (120k tweets in total). Based on the following plot,
* there is a clear uprising trend from Monday to Thursday, and a sudden drop on Friday and then gradually climb up back during the weekend.
Whether it is an indicator of people spend more time on Pokemon Go from Monday to Thursday, or people tend to tweet more during Mon to Thursday is unclear at this moment.
<img class="size-medium wp-image-273 aligncenter" src="/assets/days_of_week.png" alt="followers" width="400" height="300" />        
    
  

## 3-2. daily pattern<a class="anchor-link" href="#3-2.-daily-pattern">¶</a>

* Most of the tweets occur between the day time from 6am to 4pm which is reasonable
* It peaks at the noon time, which is perhaps because people have more free time during lunch
<img class="size-medium wp-image-273 aligncenter" src="/assets/daily_pattern.png" alt="followers" width="400" height="300" />                   


# 4. Text analysis
## 4-1. terms occurrence

By searching and sorting all meaningful single words in the text of tweets within the last two weeks, here are the first 10 most frequent words:<br /> *(&#8216;twitter&#8217;, 38406), (&#8216;pic&#8217;, 23536), (&#8216;halloween&#8217;, 10795), (&#8216;video&#8217;, 9545), (&#8216;new&#8217;, 8537), (&#8216;update&#8217;, 7604), (&#8216;liked&#8217;, 7068), (&#8216;event&#8217;, 6850), (&#8216;play&#8217;, 5300), (&#8216;get&#8217;, 4227)
* The words &#8216;pic&#8217; and &#8216;video&#8217; clearly show the popular media content of the tweets;
* &#8216;halloween&#8217;, &#8216;new&#8217;, and &#8216;update&#8217; are related to recent update of the App;
* &#8216;halloween&#8217; and &#8216;event&#8217; refer to the newly announced halloween event which aims to stimulate the players to play even in this cool weather.

<img class="size-full wp-image-292 aligncenter" src="/assets/word_count-1.png" alt="word_count" width="1023" height="552" srcset="/assets/word_count-1.png 1023w, /assets/word_count-1-300x162.png 300w, /assets/word_count-1-768x414.png 768w" sizes="(max-width: 1023px) 100vw, 1023px" />


Other rankings as follows:

the first 20 most frequent hashtag

*  (&#8216;#pokemongo&#8217;, 45988), (&#8216;#pokemon&#8217;, 6280), (&#8216;#funny&#8217;, 3757), (&#8216;#minecraft&#8217;, 3723), (&#8216;#agario&#8217;, 3703), (&#8216;#amazing&#8217;, 3695), (&#8216;#game&#8217;, 3501), (&#8216;#new&#8217;, 3342), (&#8216;#europe&#8217;, 3319), (&#8216;#turkey&#8217;, 3319), (&#8216;#trolling&#8217;, 3318), (&#8216;#love&#8217;, 2584), (&#8216;#pok&#8217;, 2055), (&#8216;#gaming&#8217;, 1163), (&#8216;#pokeballs&#8217;, 1053), (&#8216;#pokemongocoinspic&#8217;, 1015), (&#8216;#teamvalor&#8217;, 779), (&#8216;#pokecoins&#8217;, 605), (&#8216;#tech&#8217;, 601), (&#8216;#halloween&#8217;, 555)

 the first 10 most frequent mention
*  (&#8216;@youtube&#8217;, 9318), (&#8216;@leafyishere&#8217;, 1304), (&#8216;@omgitsalia&#8217;, 1239), (&#8216;@pokemongoapp&#8217;, 1210), (&#8216;@trnrtips&#8217;, 1029), (&#8216;@nianticlabs&#8217;, 907), (&#8216;@fsu_atl&#8217;, 522), (&#8216;@lachlanyt&#8217;, 301), (&#8216;@suknives&#8217;, 286), (&#8216;@witelightinghwd&#8217;, 222)
 
 A search based on bi-gram gives the first 20 most frequent two adjacent words:
*  (&#8216;pic twitter&#8217;, 23446), (&#8216;@youtube video&#8217;, 7179), (&#8216;#pokemongo pic&#8217;, 4509), (&#8216;halloween event&#8217;, 3673), (&#8216;#game #trolling&#8217;, 3318), (&#8216;play pokemon&#8217;, 2750), (&#8216;go update&#8217;, 2228), (&#8216;#love #amazing&#8217;, 2199), (&#8216;new pokemon&#8217;, 1497), (&#8216;halloween update&#8217;, 1182), (&#8216;celebrates halloween&#8217;, 968), (&#8216;need pokecoins&#8217;, 911), (&#8216;rare pokemon&#8217;, 814), (&#8216;apple pen&#8217;, 768), (&#8216;pine apple&#8217;, 764), (&#8216;ppap pine&#8217;, 764), (&#8216;still play&#8217;, 747), (&#8216;still playing&#8217;, 744), (&#8216;candy count&#8217;, 695), (&#8216;go cheats&#8217;, 685)

which indicates that
* Pokemon Go players and sellers use twitter and youtube frequently;
* recent update and event also show up timely in tweets;
* tweets show great need of pokecoins, candy and rare species etc. which might poses difficulties for current and potential users;
* Pokemon Go game is very addictive as people like to use phrases such as &#8216;still play/playing&#8217;.
* Pokemon Go&#8217;s influence even reaches popular songs (e.g., Pen Pineapple Apple Pen).

To sum up the finding, Pokemon Go clearly has very good and successful marketing strategies to stimulate their players such as holding events, and sharing pic/movies with/among the users. It is also integrated in the pop culture very well in which the game can benefit from. Certain needs such as pokecoins and rare species might pose difficulties for current and potential players, and the effects of that should be further investigated.
        
  
## 4-2. sentiment analysis

We can try to measure the sentiment scores of the tweets about Pokemon Go, which provides a way to tell game players&#8217; opinion about the game. We use the same data sample as above, but only use the most recent 4000 tweets as a test and run those tweets through a <a href="http://pythonhosted.org/sentiment_classifier/">sentiment classifier</a> built base on Word Sense Disambiguation using wordnet and word occurance statistics from nltk.
* Based on the 4000 tweets, we find a much greater positive score (85.6) than the total negative score (33.9), indicates Pokemon Go is overall receiving a very positive feedback.
       
Similar analysis can be applied to other games too, and a comparison among a pool of mobile games would also show how much people like the games.
        
   
# 5. Summary
In this proposal, I have demonstrated that we could make use of the data from Twitter to gain insight in the mobile game industry.
* We can perform very efficient and productive survey, which benifits both the game development and marketing
* We can also perform detailed analysis on given product (here use Pokemon Go as an example) to find out important information such as hot terms/topic, product usage patterns, and the customer&#8217;s opinion of the product.

Further improvement:
* bigger data set and larger sample of mobile games
* distinguish tweets from different categories, such as original post or retweet, ads or sale, etc.
* quantitative measure of the relationship between the twitter users and the real game players

