# nehadipali-Unstructured-Data-Analysis-Project---GameStop-Meme-Stock
The project analyzes the trends before, during and after GameStop became a meme stock. We also try to see if sentiment analysis helps realize short term gains in the stock market

Based on poor company fundamentals, hedge funds and other large investors were convinced that GameStop’s share price would decline. They bet against GameStop with large short positions. At the same time, thousands of small individual investors saw the opportunity to turn a profit by working against the investment establishment. Based on an idea discussed in WallStreetBets, a community on Reddit, thousands of individual investors made small investments in GameStop, knowing that eventually the short sellers would need to buy back the shares of GameStop – effectively creating a “short-squeeze.”

![image](https://user-images.githubusercontent.com/61624917/159141277-1fe16c7b-d4a0-4a26-bdb0-434756b1386b.png)

Driven by the demand from the individual investors as well as the fact that the Wall Street firms needed to cover their short sales, GameStop stock increased nearly 1500% at one point. GameStop’s case shows how powerful social media can be. When Robinhood, subject to additional capital requirements, had to temporarily block its customers from trading GameStop on their platform, the price of the stock dropped considerably. As soon as Robinhood re-enabled trading for GameStop, the stock changed course and its share price once again took off in a meteoric rise. Some of the upward pressure in price was driven by retail investors who were not part of the “short-squeeze,” but saw the escalating stock price and had a fear of missing out on its appreciation. 

It is important to note that none of the recent volatility in GameStop stock is based on any material changes to the underlying fundamentals of the company. 

The project included the following phases - 
- Data Extraction by Scraping Twitter using SNScrape: Please refer '01 - Twitter Data Scraping using SNScrape.ipynb'
- Data Cleaning: Please refer '02 - Data Cleaning.ipynb'
- Pre-Post Analysis of GameStop becoming a Meme Stock using Word Cloud, Sentiment Analysis, Topic Modeling and Cosine Similarity: Please refer '03 - Cosine Similarity.ipynb' and '04 - Word Cloud, Topic Modeling, Sentiment Analysis.ipynb'
- Stock Price Movement Direction Prediction using Sentiment Analysis Model

![image](https://user-images.githubusercontent.com/61624917/159141289-1e445b0f-c69f-4ea0-9e3b-686732de0aec.png)

For gathering the data, we scraped 40,000 tweets containing “#GME” or “#GameStop” using SNScraper. This user-generated content had been created between Oct'20 and Oct'21. Oct'20 to Dec'20 was considered as the pre-meme-stock period, while Jan'21 to Mar'21 was considered as the meme-stock-period. Apr'21 to Jun'21 was considered as the post-meme-stock period. We used stemming, lemmatization, word cloud and topic modeling to identify the dominant themes in the tweets during these periods.

![image](https://user-images.githubusercontent.com/61624917/159141298-a22e4c04-3320-4f46-b107-1760010ad709.png)

Our objective was to determine if social media sentiment could be used to realize short term gains in the stock market. For this, 10000 tweets were scraped between Jul'21 and Sep'21. This time period was selected for two reasons - 
- Recency – The recent events are more relatable.
- Volatility – Between Feb’21 and Mar’21, GameStop stock price had been highly volatile. The movement after June has been relatively smoother

![image](https://user-images.githubusercontent.com/61624917/159141324-ae1b2a0d-26f1-4d89-be8e-91b867588a15.png)

![image](https://user-images.githubusercontent.com/61624917/159141328-ce2b636b-5c79-44fa-a6ee-31ef3ec17aa1.png)

![image](https://user-images.githubusercontent.com/61624917/159141334-90e334ee-54b9-472e-b520-4d11fd63ae04.png)


For the stock price movement direction prediction, the following steps were used for model creation using VADER - 
- Sentiment analysis was done for each tweet for each day of the training period. We are more interested in the general sentiment of the tweets and not the strength of sentiment of individual tweets. Hence the direction of the compound sentiment for each tweet was considered. +1 indicated a positive sentiment, while -1 indicated a negative sentiment. For each day the score obtained in the previous step was averaged. 
- For example, if there are 100 tweets on a Tuesday, with 60 of them having positive compound score and 40 of them having negative compound score, then we have the day sentiment as {60*1 + 40*(-1)} = +20 -> As day sentiment > 0, we say direction of day sentiment = 1 (else, it would have been -1)
- For the stock prices, we consider the difference in the closing prices. In this case, we look for the impact on Tuesday’s tweets on the direction of movement on Wednesday. If price(Wednesday) > price(Tuesday) then direction of stock = 1 (in the converse case it would have been -1)
- For accuracy, we consider the number of times the direction of day sentiment was equal to the direction of the stock movement in the 92-day period.

![image](https://user-images.githubusercontent.com/61624917/159141343-79acaad0-0cb0-435a-97a8-b1de00ea61e6.png)

Our insights are as follows -
- Trending Topic Effect – people using "#GME" even though their post is unrelated to GME. This proved to be a challenge for us. We needed to exclude tweets that didn't really correspond to GME.
- Accuracy of the model improved from 43% to 57% after removing unrelated tweets. This indicates that there is scope for more data cleaning!
- We realize that unstructured data analysis can be used to gain advantage in a very short term horizon (<1 week). It is unsuitable as an investment strategy for a longer horizon as it cannot be a substitute for fundamental analysis 
While scraping the tweets consumed about 10% of the total time allocated, majority of the time was invested in cleaning the data and improving the data quality. There were multiple iterations to it – the biggest challenge included exclusion of the tweets concerned with inventory of the stores and had little to do with the stock price. 
