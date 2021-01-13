---
title: "Memnet: Chapter 2"
date: 2020-12-18T10:18:02-05:00
draft: true
---

This is the continuation of my last post about MemNet, which can be read [here]({{< ref "/post/memnetch1.md">}}). We left off with talking about TripleMem, a neural network regression model that uses three seperate feature decomposition methods, a residual neural network, a convolutional neural network, and a semantic segmentation model. I mentioned that this was a very heavy model, and a lot of it's complexity comes from that semantic segmentation process, as well as the task of integrating its output into the fully connected section of the model.