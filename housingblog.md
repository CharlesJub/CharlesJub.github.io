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
