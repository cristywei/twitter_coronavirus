# Coronavirus twitter analysis

**Learning Objectives:**

1. work with large scale datasets
1. work with multilingual text
1. use the MapReduce divide-and-conquer paradigm to create parallel code

## Background

Approximately 500 million tweets are sent everyday.
Of those tweets, about 1% are *geotagged* with the user's location information about where the tweets were sent from.
Drawing from a dataset containing approximately 1.1 billion tweets sent in 2020, I used the [MapReduce](https://en.wikipedia.org/wiki/MapReduce) procedure to analyze the tweets.

n total, there are about 1.1 billion tweets in this dataset.
The tweets are stored as follows.
The tweets for each day are stored in a zip file `geoTwitterYY-MM-DD.zip`,
and inside this zip file are 24 text files, one for each hour of the day.
Each text file contains a single tweet per line in JSON format.
JSON is a popular format for storing data that is closely related to python dictionaries.
MapReduce is a famous procedure for large scale parallel processing that is widely used in industry.
It is a 3 step procedure summarized in the following image:

<img src=mapreduce.png width=100% />

## Process

1. Modified map.py to track the usage of hashtags on both a country and language level.

1. Created a shell script `run_maps.sh` to run map.py on each zip file in the dataset.
    These files were sent to the `outputs` folder.

1. Reduced all .lang files into a single file `reduced.lang`, and reduced all .country files into a single file `reduced.county`.

1. Using visualize.py on `reduced.lang` and `reduced.country`, created files counting the usage of certain hashtags.
    These files were sent to the `viz` filder.

## Results

I analyzed the following list of hashtags related to covid-19:
```
hashtags = [
    '#코로나바이러스',
    '#コロナウイルス',
    '#冠状病毒',
    '#covid2019',
    '#covid-2019',
    '#covid19',
    '#covid-19',
    '#coronavirus',
    '#corona',
    '#virus',
    '#flu',
    '#sick',
    '#cough',
    '#sneeze',
    '#hospital',
    '#nurse',
    '#doctor',
    ]
```
The `viz` folder contains files that list the top 10 countries or languages and number of occurrences of each hashtag.
For example, in the file `#coronavirus.country`, you can see that there were 225402 mentions of "#coronavirus" from tweets geotagged in the United States, followed by 89063 mentions from tweets geotagged in India and 66803 mentions from tweets geotagged in Great Britain.
Similarly, in the file `#coroanvirus.lang`, there were 422,394 mentions of "#coronavirus" from tweets in English, followed by 137,714 mentions from tweets in Spanish, and 103,249 mentions from tweets that were "undefined", meaning Twitter could not determine the language of the tweet.
