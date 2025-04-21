+++
title = "Geocoding RSS Feeds"
slug = "geocoding-rss-feeds"
date = "2025-04-20 19:07:56 UTC-07:00"
tags = "google-genai, python, genai, geocoding"
category = "generative-ai"
link = ""
description = "Using GenAI to Geocode RSS news feeds"
type = "text"
+++
San Diego was the first site settled by Europeans on the West Coast of the United States and is now the 8th largest city, with a population around 1.3 million.
There is a lot of news, events and activites and a wide variety of news sources reporting on them.
Can LLMs help to summarize all of this content and provide an overview what has happened and is happening around the city? 
This project utilizes Google's Gemini models, and their features, to process San Diego news feeds for food and arts articles,
and create a map them.

<!--TEASER_END-->

This project is my Capstone Project submission for 
[Kaggle's Gen AI Intensive Course](https://www.kaggle.com/learn-guide/5-day-genai).
This 5 day program covers prompt engineering, embeddings, vector stores, agents, and a bit of MLOps for Generative AI.
It is also a fantastic introducton to 
[Google's genai python API](https://ai.google.dev/gemini-api/docs/quickstart?lang=python).

The project notebook can be found here: https://www.kaggle.com/code/fourfourdigits/georeferencing-local-news

There are two phases to this project:

1. Evaluate Gemini models and their ability to extract perntinant details from RSS feeds
1. Utilize the best model, found above, to process RSS and ATOM feeds from San Diego publications and plot them on a map

## Initialization ##

Three main functions are used in this project:

- `get_feed()`: download the feed represented by the given url
- `geocode_place()`: geocode the given placename using the [Google Geocoding API](https://developers.google.com/maps/documentation/geocoding/), assuming the place is in San Diego.
- `get_airesponse_reviewarticles()`: give the given prompt, with RSS feed, to the given model and return the JSON response

The prompt asks the model to filter an XML feed of news articles,
select those that fall within a given list of categories (arts or food), and remove any duplicates.
The model is also tasked with review the article summary and determining if the article pertains to a particular point location
in San Diego, and what the location is.
`genai`'s **function Calling** is used to obtain the lat/lon coordinates of the article's location utilizing Google's Geocoding API.
The prompt also utilizes some prompt engineering techniques:

- **Structured Output**: the prompt request the output in JSON and provides the fields to be provides
- **Few-shot prompting**: the prompt provides multliple examples of inputs and the output expected


## Phase I: Evaluate Models ##
Three models are examined in the Evaluate phase.
Using the Pointwise text quality prompt (1) the quality of the output from each model is evaluated and scored.
The pointwise evaluation produces a score from one to five, with five being the best.
The `gemini-2.0-flash` model is used for the evaluation.

1. https://cloud.google.com/vertex-ai/generative-ai/docs/models/metrics-templates#pointwise_question_answering_quality

## Phase 2: Geocode Feeds ##
The best performing model from the above Phase is used to process all of the RSS news feeds.
All feeds are downloaded and given to the model with the geocoding prompt.
The JSON output from each request is concatenated and the final array of articles plotted on a map
using the Folium Python library.

## Conclusion ##
Geocoding news articles is a difficult problem.
While it may be possible to simply search an article for place names, this is clumsy solution and does not utilize any context.
Articles may also refer to a place as an example of a much larger subject.
The quality of the geocoding is improved with an understanding of the article being geocoded.

This project demonstrated that GenAI is a useful tool for geocoding news articles.
The model utilized the context of the articles, understood detailed instructions, formatted the output as requested,
and was able to incorporate data from external APIs.

