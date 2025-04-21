+++
title = "Geocoding RSS Feeds"
slug = "geocoding-rss-feeds"
date = "2025-04-20 19:07:56 UTC-07:00"
tags = "google-genai, python, LLM, geocoding"
category = "generative-ai"
link = ""
description = "Using LLMs to Geocode RSS news feeds"
type = "text"
+++
San Diego was the first site settled by Europeans on the West Coast of the United States and is now the 8th largest city, with a population around 1.3 million.
There is a lot of news, events and activites and a wide variety of news sources reporting on them.
Can LLMs help to summarize all of this content and provide an overview what has happened and is happening around the city? 
This project utilizes Google's Gemini models, and their features, to process San Diego news feeds for food and arts articles,
and create a map them.

This project is my Capstone Project submission for 
[Kaggle's Gen AI Intensive Course](https://www.kaggle.com/learn-guide/5-day-genai).
This 5 day program covers prompt engineering, embeddings, vector stores, agents, and a bit of MLOps for Generative AI.
It is also a fantastic introducton to 
[Google's genai python API](https://ai.google.dev/gemini-api/docs/quickstart?lang=python).

The project notebook can be found here: https://www.kaggle.com/code/fourfourdigits/georeferencing-local-news

There are two phases to this project:

- Evaluate Gemini models and their ability to extract perntinant details from RSS feeds
- Utilize the best model, found above, to process RSS and ATOM feeds from San Diego publications and plot them on a map

## Phase I: Evaluate Models ##

The prompt used to processess article feeds utilizes multiple prompting techniques:

    A structured JSON response is requested.
    One-shot prompting provides the model an example of the output.
    Function-calling is also used to obtain the lat/lon coordinates of each place, using the Google Maps API. [2]

References:

    https://en.wikipedia.org/wiki/San_Diego
    https://developers.google.com/maps/documentation/geocoding/


Write your post here.
