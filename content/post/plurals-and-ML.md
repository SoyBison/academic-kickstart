---
title: "Plurals and ML"
date: 2020-01-24T16:39:07-06:00
draft: true
tags: ['Machine Learning', 'Natural Language']
---
# Plurals and Machine Learning

Using older machine learning models to conjugate English verbs produced rather silly results. These models performed at an acceptable level for many words, but when given nonsense words as an input these models would produce humorous conjugations. For [example](https://books.google.com/books?id=2cEuBgAAQBAJ&pg=PA144&lpg=PA144&dq=smeej+leefloag&source=bl&ots=y2F6Lge_uw&sig=ACfU3U0WPSRcA2Pwu8O0NqUm00dsExNyNw&hl=en&sa=X&ved=2ahUKEwiW4MbOqJ3nAhUDB50JHfvvB5wQ6AEwAHoECAsQAQ#v=onepage&q=smeej%20leefloag&f=false), we have:

|Verb | Human Generated Past-Tense | Machine Generated Past-Tense|
|-----|------------------|-------------------|
|mail|mailed|membled|
|conflict|conflicted|conflafted|
|wink|winked|wok|
|quiver|quivered|quess|
|satisfy|satisfied|sedderded|
|smairf|smairfed|sprurice|
|trilb|tribled|treelilt|
|smeej|smeejed|leefloag|
|frilg|frilged|freezled|

Naturally, my girlfriend and I found this hilarious. With the use of the [XTAG](https://www.cis.upenn.edu/~xtag/swrelease.html) database, we thought it would be fun to play around with a similar model to pluralize English nouns.

### Setup

The XTAG database is written in a flat ascii format, which doesn't play nice with modern systems, so it needs some cleaning up.

```python

```


### Plurals and Simple Deep Networks

To start we'll
