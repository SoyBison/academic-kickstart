---
author: Coen D. Needell
title: Research Proposal on Urban Legends and the Internet
tags: ["Digital Archeology", "Cultural Patterns", 'Urban Legends']
draft: false
---

# Research Proposal on Urban Legends and the Internet

## Introduction

"Urban Legends" is a genre we often confer to fictional and semi-fictional stories that circulate through modern communities. Generally this describes stories that few people truly believe, but are still told and retold time and time again. These stories often have common features, they leverage the unintuitiveness of modern life, a sense of distant credibility ("This happened to a friend of a friend"), and in some cases a sociopolitical call-to-action. Prototypical Urban Legends include the story about a man meeting a woman in a hotel bar and waking up the next day missing a kidney in a bathtub full of ice, or the story where your uncle's friend went down into the sewers and encountered a bask of exotic crocodiles that had been flushed down by irresponsible pet owners. 

Despite their ubiquity, there is a relatively small amount of academic research on these stories. Most of the sources I've been able to find about them are either highly biased toward interpreting urban legends in the same way that one would interpret ancient mythology, or are written in a dismissive tone, treating these stories as unworthy of study. What books and articles I've found that aren't dismissive have been from the last five years or so. In short, this seems like an emerging area of research. The research I've found has been approaching questions of the genre: "what does it mean?". I'd like to instead ask about the dynamics of urban legends, why do some spread farther than others? Can we identify internal features that are associated with 'success' in this context? Or is it all about the substrate that they spread through? What about some combination of both?

## Possible Methodology

### Data Acquisition

This might be difficult. A lot of the internet early on was on Usenet, which is fairly well preserved by Google at this point, but this excludes the millions of private email chains that gave us hoaxes like the Neiman Marcus Cookie Recipe, as well as a lot of the more conspiracy theory leaning urban legends.

Another option is to utilize some of the wonderful internet archeology resources out there, like the internet archive as well as smaller servers that have been built to store troves of old forum posts and discussions. 

### Data Analysis

The analysis of this data will have to be split into two stages. First, an identification stage. I need to get some way to decompose instances of the urban legend into core components. There are a number of Natural Language Processing techniques that are built specifically for this. Part of the challenge will be identifying both the type-instances of these stories, and then studying how the token-instances differ over time, and how that relates to the environment that they're observed in. For example, we might expect the _Slenderman_ story to adopt different characteristics on the sub-reddit "/r/nosleep", a forum of scary stories, than if it instantiates on a forum focused on forest management.

The second stage of analysis will be focused on dynamics. We need to see how the features that we identified in the first stage relate to how the story spreads, it's level of "success" and how it mutates over time. This will likely take the form of some sort of tensor modeling. We can model an online community as a set of individual neurons, and see how the network mutates the story as it passes through the community, and between communities.

## Possible Challenges

The identification stage will be *hard*. I will likely need to write bespoke algorithms and utilize unconventional feature extraction methods. Luckily, the dynamics stage is better off. Network analysis and contagion theory are well developed, and have a lot of packages available for use to speed up that process.


## Annotated Bibliography
---
Frank, Russell, author. _Newslore: Contemporary Folklore on the Internet_. University Press of Mississippi, 2011. EBSCOhost, doi:10.14325/mississippi/9781604739282.001.0001.

- This will probably be fairly tangential to my research. He defines a subset of internet folklore that's built around "important" topics, the news, and so-on. This is definitely a subset of folklore that's worth discussion, especially when this was written in 2011, well before these stories were rebranded by the media as "fake news".

_Slender Man Is Coming : Creepypasta and Contemporary Legends on the Internet_. 2018. EBSCOhost, search.ebscohost.com/login.aspx?direct=true&db=edsbas&AN=edsbas.2F8D4139&site=eds-live&scope=site.

- I'm in the process of getting ahold of this, but based off of the abstract and title, this is probably going to form the bulk of by background. It is, however, a focus on the mythological analysis of these stories, but that may inform a memetic model of urban legend dynamics.
 
Dawkins, Richard. _The Selfish Gene_. New ed. Oxford ; New York: Oxford University Press, 1989.

- If I'm going to consider memetics I have to cite this. A re-read is probably in order. Even though it isn't an academic text, it is the origin of this conception of ideas spreading in a darwinian way.

Kronfeldner, Maria E. _Darwinian Creativity and Memetics_, 2014. http://proxy.uqtr.ca/login.cgi?action=login&u=uqtr&db=ebsco&ezurl=http://search.ebscohost.com/login.aspx?direct=true&scope=site&db=nlebk&AN=846618.

- This is a more modern and academic treatment of a Darwinian model of ideas. Hopefully my model will lean more towards this than Dawkins' original.