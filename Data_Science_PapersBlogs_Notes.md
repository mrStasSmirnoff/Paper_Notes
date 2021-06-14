## Medium:

#### Listing Embeddings in Search Ranking (AirBnb)

- Link: https://medium.com/airbnb-engineering/listing-embeddings-for-similar-listing-recommendations-and-real-time-personalization-in-search-601172f7603e
- Description: The idea is to train vector representations (Embeddings) of the available accomodations (listings) in Airbnb that will allow to measure similarities between them and eventually to present similar to the users (Similar Listings) or use as the extra features to improve Search Ranking model.
- Technologies: NN (to train with backprop embeddings)
- More:  Given this data set, the aim is to learn a 32-dimensional representation V(L_(i)) of each unique listing Li, such that similar listings lie nearby in the embedding space. The *Negative Sampling* techinique is used to train embeddings. Starting with initially random vectors and proceeds to update them via SGD by reading through search sessions in a sliding window manner. At each step the vector of the central listing is updated by pushing it closer to vectors of positive context listings: listings that were clicked by the same user before and after central listing, within a window of length m (m = 5), and pushing it away from negative context listings: randomly sampled listings (as chances are these are not related to the central listing).  Two modification were also made for this approach:
    - using *Booked Listing as Global Context*: The sessions that end with the user booking the listing are used to adapt the optimization such that at each step we predict not only the neighboring clicked listings but also the eventually booked listing as well.
    - adapting to *Congregated Search*: Users of online travel booking sites typically search only within a single market (same geolocation). As a consequence, for a given central listing, the positive context listings mostly consist of listings from the same market, while the negative context listings mostly consist of listings that are not from the same market as they are sampled randomly from the entire listing vocabulary. This imbalance leads to learning sub-optimal within-market similarities. To address this issue it is proposed to add a set of random negatives Dmn, sampled from the market of the central.
    
    For new accommodations *Cold Start Embeddings* authors find 3 geographically closest listings that do have embeddings, and are of the same listing type and price range as the new listing, and calculate their mean vector. The offline evaluation is done by taking the most recently clicked listing and the listing candidates that need to be ranked, which contain the listing that the user eventually booked. By calculating cosine similarities between embeddings of the clicked listing and the candidate listings we can rank the candidates and observe the rank position of the booked listing. For the *Search Ranking* where the aim is to show to the guest more listings that are similar to the ones we think they liked since starting the search session and fewer listings similar to the ones we think they did not like. To achieve this, for each user authors collected and maintain in real-time (using Kafka) two sets of short-term history events: **Hc** - set of listing ids that user clicked in last 2 weeks and **Hs** - set of listing ids that user skipped in last 2 weeks, where we define skipped listings as ones that were ranked high but skipped by a user in favor of a click on a lower positioned listing. These two similarity measures were next introduced as an additional signal that our Search Ranking Machine Learning model considers when ranking candidate listings.


#### Learning Market Dynamics for Optimal Pricing (AirBnb)

- Link: https://medium.com/airbnb-engineering/learning-market-dynamics-for-optimal-pricing-97cffbcc53e3
- Video: https://www.youtube.com/watch?v=HjYudaD6Feg&ab_channel=GlobalBigDataConference

- Description: The lead time for a booking refers to the time between the date of booking and the trip check-in date. The corresponding distribution of bookings over lead time is the booking lead time distribution. Learning the booking lead time distribution helps power our pricing system. Airbnb launched Smart Pricing to help hosts set optimal prices and maximize earnings. These tools take into account factors like demand, supply and individual listing properties in order to make price suggestions for all check-in dates on the calendar. By learning the arrival process for every check-in date and location, Smart Pricing accounts for this “early demand” and generates a pricing policy that allows hosts to optimally update their prices as we approach check-in. The goal is to learn and estimate "f" (the density of the distribution above), for each listing "i", check-in date "j", and every lead day "t" heading into check-in.




#### How does Spotify know you so well?

- Link: https://medium.com/s/story/spotifys-discover-weekly-how-machine-learning-finds-your-new-music-19a41ab76efe

- Description: A very broad description of the ML components of Spotify recommendations (Discover weekly)
- Technologies: Colaborative Filtering, NLP (on text), CNN (audio)
- More: In a nutshell, the author depicts three main ML components of Spotify recommendations, namely: Collaborative filtering, NLP on text, and NLP on the audio itself. For the Collaborative filtering the idea is pretty straight-forward, one big 140x30 (mln) matrix of users-songs data is factorized into two matrices *X* (user vector) and *Y* (songs vector). Then the similarities are computed to get "the match". For the second one, it is a bit more interesting. The source for this model is track metadata, news articles, blogs, and other text around the internet. Spotify crawls the web constantly looking for blog posts and other written text about music to figure out what people are saying about specific artists and songs — which adjectives and what particular language is frequently used in reference to those artists and songs, and which other artists and songs are also being discussed alongside them. What happens then is that (most probably) data up into what they call “cultural vectors” or “top terms.” Each artist and song had thousands of top terms that changed on a daily. Each term had an associated weight, which correlated to its relative importance — roughly, the probability that someone will describe the music or artist with that term. Then these terms and weights are used to create a vector representation of the song that can be used to determine if two pieces of music are similar. And the third component - Raw audio data. It allows overcoming the main weakness of Collaborative filtering - lack of generalization (raw audio models take new songs into account). CNN is used with the spectrogram as input. After processing, the neural network spits out an understanding of the song, including signals like estimated time signature, key, mode, tempo, and loudness. Which are also used as features to compute similarities between songs.


## Trivago:

#### Machine Learning and Bathtubs - How Small Visual Changes Improve User Experience 
	
- Link: https://tech.trivago.com/2019/08/21/machine-learning-and-bathtubs-how-small-visual-changes-improve-user-experience/	
- Description: The idea is to adjust the main images of hotels to reflect the user intent coming from SEM ads containing spa concepts (concept-based main images)
- Technologies: AWS stack for pipelines, RNN, CNN with transfer learning. 
- More: Automated (with CV) image labeling of Trivago 100+ million active images for Spa & Wellness. For training, some public data has been used along with existing handpicked image tags from our trivago hoteliers. Questionnaires have been prepared based on Amazon Mechanical Turk to align the images semantically. The resulting dataset had 2,000 images for each of the categories of "Sauna", "Pool", "Gym", "Yoga", "Hot-tub" and "Massage". Five different CNN architectures (InceptionV3, VGG16, Xception, ResNet50, InceptionResnetV2) were evaluated with VGG16 chosen as the final model. Precision was used as an evaluation metric (to min False Positives). To deal with the images that had to be negated (out all classes that are beyond this concept) two additional (unbalanced) classes were introduced "Bedroom" and "Non-Spa". An average  Precision and Recall of ~85% and ~89% for the individual Spa & Wellness classes.



## Uber Engineering:

#### Forecasting at Uber: An Introduction

- Link: https://eng.uber.com/forecasting-introduction/
- Description: An intro to the Forecasting approach at Uber.
- Techinologies: statistical models (ARIMA), Regressions, Boostings, RNNs, Omphalos (a parallel, language-extensible backtesting framework)
- More: Uber leverages forecasting for several use cases, including "Marketplace Forecasting" (Spatio - temporal forecast), "Hardware capacity planning",
"Marketing" (to understand the marginal effectiveness of different media channels). Quantitative forecasting approaches in Uber can be grouped as follows: model-based or causal classical, statistical methods, and machine learning approaches. Model-based forecasting is the strongest choice when the underlying mechanism, or physics, of the problem is known, and as such it is the right choice in many scientific and engineering situations at Uber.
When the underlying mechanisms are not known or are too complicated it is usually better to apply a simple statistical model. Popular classical methods that belong to this category include ARIMA (autoregressive integrated moving average), exponential smoothing methods, such as Holt-Winters, and the Theta method, etc. Additionally, machine learning approaches are utilized as: including quantile regression forests (QRF), the cousins of the well-known random forest. Recurrent neural networks (RNNs) have also been shown to be very useful if sufficient data, especially exogenous regressors, are available. In practice. classical statistical algorithms tend to be much quicker and easier-to-use. Two major approaches to test forecasting models are "the sliding window" approach and "the expanding window" approach. Often best, to marry the two methods: start with the expanding window method and, when the window grows sufficiently large, switch to the sliding window method. For the evaluation besides of the common metrics like absolute errors and percentage errors, the comparison of the model performance against the naive forecast is also used. In the case of a non-seasonal series, a naive forecast is when the last value is assumed to be equal to the next value. "Prediction intervals" are also very important, in fact they are given the same importance as the point forecast itself and should always be included in your forecasts. Prediction intervals are typically a function of how much data we have, how much variation is in this data, how far out we are forecasting, and which forecasting approach is used.

