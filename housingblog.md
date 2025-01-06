# Predicting House Prices with the Script of House Tours

- everyone has a youtube rabbit hole they have found themselves in, my rabbit hole is expensive properties.
- 

## Transforming Tour Scripts into Data Points

- extracted data from youtube api in python
- gathered only from Enes Yimliazer youtube channel. reasons for only using one channel:
  - he has a decent catelog of differently priced homes
  - will be easier for models to catch on to language changes for one person
  - he includes price of home in almost all video description, title, or thumbnail
- had to get numeric dollar amount from messy text representation like $8 million, $20,000,000, and sometimes only in the thumbnail
- did text processing to standardize text
  - removed articulation markings like [music playing] or [Enes]
  - removed filler words
  - removed stop words
  - lemmatized
  - removed all number in the script to not leak data into model. ideally would only remove dollar amounts, but to simplify removed all numbers

## Seperating traditional and non-traditional assets

- the youtube channel mostly highlights traditional luxury homes, but sometimes covers other assets.
- would have to create labels for this manually, so instead I used clustering
- Used a wide array of clustering methods combined with different ways to standardize the data
  - found that bisecting k-means with no transformation on TF-IDF data did the best job of seperating traditional homes and non-standard assets.
  - captured all non-traditional assets, but also captured two traditional homes
    - the traditional homes included are not like Enes' other videos. they both contain less talking then standard videos and cover multiple houses

## Predicting House Prices

- started by just using the tf-idf with a max of 1000 features to minimize overfiting, with no transformations to the target variable
  - tried Linear Regression, LASSO, RIDGE, Random Forest, XGBoost, LightGBM, SVD, and an ensemble of all
  - LASSO preformed the best on these simple inputs with a mape of _______
- tried adding new features to capture different information
  - added word count: videos tend to be longer when there is more sq footage
  - added location flags: tried to capture general location of home by creating flags for common house locations like california, new york, or florida
  - added sentiment to test if a summary of the word meaning mattered
  - these only improve the model slightly
- then tried to log transform because the data had some outlier house prices in the 200+ millions
  - improved the model substantially
  - best model was ____ with a mape of
- used pca to test if model would do better with *___________*
- best model overall was a ensemble model with a ape of _______

## Conclusion

- it was challenging to get the data in a format that was able to model on
- after getting the data in the right format, I was able to model on the data rather successfully 
- the future plan
    - create a dashboard that will try to predict if a video is a traditional house or a different type of asset. Will also try to predict the value of the house. Recognizing that the model will only do well on videos made by Enes because models look at the vocabulary he uses in these 
    - model on more house tour channels. Difficult because they all have different ways of talking about homes, and will require different cleaning techniques to capture house prices automatically better. Maybe use an LLM to ask what the house price is based on title, description, and script. 
