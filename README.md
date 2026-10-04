# VIKAS: multimodal disaster response from social media

Smart India Hackathon 2022, problem statement GS900 from the National Disaster Response Force (NDRF): extract text, images, voice and video from social media posts in disaster-struck areas. Team gitinitrepo from Manipal Institute of Technology finished as a Grand Finalist and presented to the NDRF. The work was later published as [VIKAS: A Multimodal Framework to Aid in Effective Disaster Management](https://doi.org/10.1007/978-981-99-2264-2_22) (ATIS 2022, Springer CCIS vol. 1804).

**Team:** [Gautham Prabhu](https://github.com/GauthamPrabhuM) (team lead), [Anurag Chowdhury](https://github.com/canurag17), [Soumya A R](https://github.com/omnomsom), [Anshita Palorkar](https://github.com/anshita-palorkar), [Tanay Gupta](https://github.com/s1ri1337), [MV Srujan](https://github.com/mvsrujan). The commit history is the team's original history, imported from [s1ri1337/SIH2K22](https://github.com/s1ri1337/SIH2K22).

Project page: https://vikas-066f8f.webflow.io/

# Abstract

<b>VIKAS</b> is a real-time, multimodal system linking disaster victims and first responders from NDRF: streamlining support to the most vulnerable.

In the event of a disaster, many people turn to social media to seek support, both material and mental. The data from these posts aids in increasing situational awareness as soon as possible. Text, images, videos, and audio extracted in real-time from these social media posts play a crucial role in identifying appropriate emergency responses to a particular disaster. Once irrelevant information is filtered out, deep-learning-based classification, object identification and natural language processing methods are used to expedite emergency response decision-making
processes. Easy-to-interpret visualizations then help the distribution of resources and dispatch required personnel to affected areas.

<img src="https://i.imgur.com/78tP0Gk.png">



<br>

The system has three parts:

1) Data extraction- Realtime extraction of raw data 
2) Analysis of extracted data
3) Visualization for data
   
# Data Extraction

Our project mainly deals with data that is available from tweets. This generally comprises <b>texts</b> and <b>images</b> extracted from the respective tweets.

## Text extraction
Our solution uses the Twitter API to access tweets in realtime during the occurrence of a disaster. The We used Tweepy:

```bash
pip install tweepy
```

Using the API, A keyword and stream time are entered, and data is streamed real-time in a database framework. This data may include the text content and geolocations of the tweets along with links to images and videos.

For cleaning of data and preprocessing our model does the following:

- Remove non alphanumeric characters (ex. punctuation)
- Remove emoticons, URLs, emails, ‘RT’ using regular expression.
- Duplicated tweets are placed in a different pandas dataframe.
- Irrelevant tweets are filtered out using Natural Language Processing.

 <img src="https://i.imgur.com/q4BZpG0.png"> 

 ### Tweets filtered for the keyword 'Flood' 
<br>
We also developed a Word Cloud which generates a collection of words which are associated with the disaster. These words are generated according to the frequency of their usage and their relevance with respect to the disaster.<br>

To run the word cloud you need to first install the python library by the following command

    pip install wordcloud

<br>

<img src="https://i.imgur.com/wEtRtGh.png"> 


<img src="https://i.imgur.com/oLqYSNT.png"> 

### An illustration of the word cloud for the tweets relevant to Japan bombings 


For determining the relevancy of a tweet, we used the [Crisis NLP dataset](https://crisisnlp.qcri.org/). We use a BERT based model to analyze this text which is described in the next section.

## Image extraction

Images are extracted from image links present after the relevant tweets are filtered. These images are then analysed later using Computer Vision models.


# Analysis of extracted data


## Analysing text


Tweets and text posts often contain crucial information about the locations affected by a particular disaster and the amount of resources required. Hence after the extraction of text, we make word embeddings. These word embeddings are then classified as disaster and non disaster related.<br><br>

<img src="https://i.imgur.com/zOwCUQ6.jpg"> 
<br>
<br>
<img src="https://i.imgur.com/4Xm9jRQ.jpg"> 
<br>
<br>

We also made an LSTM based RNN model which helps us obtain important statistics with respect to a particular disaster. These statistics often include important landmarks and locations which we can represent in a map.
<br><br>
Demo: https://view-awesome-table.com/-NAOX2coHuKs-_YWPfhy/view
<br><br>
<img src="https://i.imgur.com/0b08Trq.jpg"> <br><br>



## Analysing audio

Speech Recognition using the Google Speech API. 
Audios will be extracted from videos and converted into text using Speech-to-Text. 
The text is further analysed using the models mentioned above.

## Analysing photos and videos

We use CNN-based classification and object detection models to classify images and detect disaster-related labels.

We first classify images as relevant or irrelevant depending on the disaster. In this model we fine tune an existing model, the Resnet50. This refined model is built on fastai.
Further the relevant images are then taken and classified based on severity and the type of disaster. 

DL models are used for this classification. Types of damage include fire damage, natural damage, infrastructure damage, and flood damage and severity ranges from mild to severe.

<img src="https://i.imgur.com/xUyJCeG.png"> <br><br>

<img src="https://i.imgur.com/JbDHIzW.png"> <br><br>


# Visualizations

Dashboard designs (Figma). They show the data made available after applying various ML techniques described above.

https://www.figma.com/file/QMKn8FxcbEtSY5KKajtXLF/Vikas-Dashboard?node-id=301%3A2872 (English)
https://www.figma.com/file/yGQMVaYngLebKpmQoXTl8y/Vikas-Dashboard-(Hindi)?node-id=0%3A1 (Hindi)

# Future scope and limitations

## Language
More research into Indian language processing, pre-trained models, and corpora collection will help us expand our project to a diverse range of localities.

## More Data Sources
Higher level access to public APIs, and access to APIs that are not currently public (ex. Facebook, Koo) could provide us with more information to improve our accuracy, redundancy checks, and account for outliers.

## Location Data
With better documentation of local landmarks, we can refine the search space and improve map visualisation.

## Cloud Computing Resources
MLaaS and PaaS will increase processing power, reduce model training time, make it easier to manage storage and updates.

## Note on credentials

API keys that appeared in early commits have been replaced with placeholders. Set your own Twitter and RapidAPI credentials in `Data Extraction/SIH/app.py` and `botcheck.py` before running. The Twitter v1.1 streaming API this was built on has since been retired.
