---
title: 'Using old training data or test sets'
date: 2020-12-14
permalink: /posts/2020/12/using-old-data/
tags:
  - machine translation
  - evaluation
  - best practices
  - bleu
---

In MT research there is a long-standing tradition of using old data sets when newer versions are available for the same language pair and domain.

Some particular data sets that people are fixated on are from the WMT14 news translation task. More precisely, English-German and English-French
from this task are used very often. I think that the original paper about Transformers ([Vaswani et al., 2017](https://arxiv.org/pdf/1706.03762.pdf)) started this frenzy, or at least
popularized those data sets.

There are several problems with this. First of all, many authors describe those 2014 data sets as "high-resource" and "large-scale" experiments.
This not true anymore. For instance, in 2014 the WMT EN-DE data had 4.5M sentence pairs. But in the 2020 edition, WMT had roughly 50M sentence pairs
for EN-DE, plus hundreds of millions of monolingual sentences in either language!

So, clearly, the notion of "high-resource" changes over time. It's not a fixed number of sentence pairs and "high-resource" from several years ago
ceases to be high-resource at some point. If you work with data ten times smaller than what would be available, what you are studying are not high-resource
models and you cannot simply extrapolate conclusions to such systems, for instance claim that they would behave similarly.

In [his blog](https://marian-nmt.github.io/2020/01/22/lexical-diversity.html), Marcin Junczys-Dowmunt coined a catchphrase that I think perfectly captures this sentiment:

> [Latest] WMT or it did not happen! ("Latest" added by myself)

In the blog post, he admonishes that people tend to study relatively weak models, but not show much restraint in their claims. At least implicitly,
many papers claim that the conclusions probably are valid also for stronger models. That may not be the case. For instance, one of the models discussed
in the blog post did not use a BPE model - in a study about lexical diversity! Almost all MT models currently in use have BPE which enhances their ability
to be lexically diverse I would argue, so that is a serious handicap.

A final, very subtle point about using old benchmarks is that the test sets are also old. Old testsets are not truly "unseen", authors had plenty of time
to study the "right answers". Even if they use the WMT14 EN-DE test set as proper held-out data in their experiments, it is a test set that has been poked
and butchered for years.


As with different variants of computing BLEU scores, many people would argue that testing on old data sets is done to compare to previous work.
And again, an obvious question to them is:

> Of course you can **also** evaluate on this old test set for comparison, but why **only** on this testset?

Recommendation
==============

Use the most recent training and test sets available for a particular language pair and domain.
The value of comparing to previous works on old data sets diminishes over time.
