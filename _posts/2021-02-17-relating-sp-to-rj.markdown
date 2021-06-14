---
title: "Clustering: Relating Neighborhoods from São Paulo to Rio de Janeiro using unsupervised machine learning"
layout: post
date: 2021-02-17 22:10
tag: machine-learning, knn, clustering
image: #https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/pc.jpg
headerImage: false
projects: true
hidden: true # don't count this post in blog pagination
description: "Construction a model to relating neighborhoods in São Paulo and Rio de Janeiro"
category: project
author: emdemor
externalLink: false
---

# Relating Neighborhoods from São Paulo to Rio de Janeiro

[Original Post](https://emdemor.medium.com/applied-data-science-capstone-most-similar-neighborhood-in-another-city-a0b018ec98e1)

## 1 Introduction

### 1.1 Background

São Paulo and Rio de Janeiro are the two largest cities in Brazil. Although relatively close (given the continental dimensions of the country), they have very different characteristics. One of the factors that contribute to the existence of these discrepancies is the obvious geographical distinctions that naturally shape social behavior and, indirectly, the urban structural configuration. The beaches of Rio de Janeiro, for example, give residents a natural option of entertainment and the nearest commercial places have characteristics aimed at this purpose. On the other hand, in São Paulo, entertainment options are directly dependent on experiences that can be provided as a business model.
From a social point of view, Rio de Janeiro inherits aristocratic characteristics, for having long been the capital of the empire of Brazil. In contrast, the history behind São Paulo's growth is much more associated with commercial reasons. For this reason, the lifestyle in São Paulo tends to be much more pragmatic than in Rio de Janeiro. This characteristic also influences the business model, as there are many more establishments in São Paulo that provide what people do not have time to do.

We have two of the largest cities in the world with very distinct characteristics: São Paulo and Rio de Janeiro. Locally, each of these places acts like professional centers attracting professionals and companies. Despite the differences mentioned, it is expected that several specific neighborhoods of these cities have characteristics in common. One way to look for this similarity would be to consider the types of venues in each neighborhood. In this way, it would be possible to detect whether a neighborhood has characteristics more focused on commerce, leisure, sports, culture or housing. So, what we need here is a procedure capable of relating neighborhoods, not only from the same city, but also from different cities.

### 1.2 Interest

It is very common for people to have to move to another city. The reasons for this are quite diverse and can involve professional opportunities, personal reasons, among others. This process can be difficult for some people, as it involves adapting to a new and possibly different environment. Although two cities may be completely different, they may have neighborhoods with similar characteristics in common. Knowledge of this information can be crucial when choosing a new place to live in a new city. Thus, a person can choose to move to a neighborhood in a new city with similar characteristics to the neighborhood in the city where he lives in and is already acclimated.
Sometimes, a company in one of these cities is interested in a professional that lives in the other city. Certainly, if the professional finds a similar neighborhood, he will be more likely to accept an offer if it is professionally interesting.

## Data

The name of all neighborhoods of São Paulo and Rio de Janeiro are needed to solve the problem. The data given at the site www.guiamais.com.br is used. The respective URLs are:

* (São Paulo): https://www.guiamais.com.br/bairros/sao-paulo-sp

* (Rio de Janeiro): https://www.guiamais.com.br/bairros/rio-de-janeiro-rj

We can see an example of data scraped from the pages in Fig. 01.


<p align="center">
  <img src="https://raw.githubusercontent.com/emdemor/Coursera_Capstone/main/report/nb_example.png"/>
</p>
<p align="center" style="font-size:75%;">
  Figure 1: Example of neighbourhoods in São Paulo and Rio de Janeiro.
</p>


  As the next step, we need to get the latitude and longitude of all neighborhoods. It can be done using the Nominatim search API, from OpenStreetMaps. An example of data with coordinates can be see on Figure 2. Its possible to see the neighborhood positions in the maps of Figure 3.


  <p align="center">
  <img src="https://raw.githubusercontent.com/emdemor/Coursera_Capstone/main/report/coor_example.png"/>
</p>
<p align="center" style="font-size:75%;">
  Figure 2: Example of neighbourhoods in São Paulo and Rio de Janeiro with latitude and longitude imported from Nominatim.
</p>



<p align="center">
  <img src="https://raw.githubusercontent.com/emdemor/Coursera_Capstone/main/report/sp-rj-map.png"/>
</p>
<p align="center" style="font-size:75%;">
  Figure 3: Example of venues on neighbourhood with index nb_index = 0.
</p>
