---
title: 'Simulating low-resource experiments'
date: 2020-12-14
permalink: /posts/2020/12/simulating-low-resource/
tags:
  - machine translation
  - evaluation
  - best practices
  - low-resource
---

Low-resource machine translation has been an active area of research for years. On a high level, what many papers on low-resource MT have in common is that they
**simulate low-resource scenarios**.

What I mean is that many papers take a data set for a high-resource language pair (such as DE-EN) and randomly subsample until they arrive at the desired size.
As an example, consider [Gu et al. (2018)](https://www.aclweb.org/anthology/N18-1032.pdf). I believe I can single them out here because the paper makes very strong
claims about "very low-resource machine translation".
As they state in the abstract:

> Our approach is able to achieve 23 BLEU on Romanian-English WMT2016 using a tiny parallel corpus of 6k sentences.

Of course,  6K is not all the data available for RO-EN in WMT16. For instance, [Europarl had 400k sentence pairs](http://www.statmt.org/wmt16/pdf/W16-2301.pdf) for this language pair back then.
A different language pair for which the total number of available sentence pairs [appears to be actually 6K is German-Yiddish](https://github.com/Helsinki-NLP/Tatoeba-Challenge/blob/master/subsets/lowest.md).

Now, why am I making a big deal of  RO-EN being downsampled to 6K, compared to DE-YI for which 6K is the total amount? There is reason to believe
that simulated low-resource scenarios lead to different conclusions and insights.

I think nobody really knows the extent to which this is a problem, but consider the following. A small collection of 6K sentences for DE-YI is not an i.i.d.
sample of a large pool of sentences. It is likely that all of them come from the same source, hence a single text domain. On the other hand, a 6K sample of RO-EN
sentences is much more representative of a larger population of sentences since samples are drawn at random.

This means that phenomena on all levels of linguistic organization have a very skewed distribution in our DE-YI data, while again, the RO-EN sample should be more
representative in terms of lexical choice, syntax and so on. Models probably benefit greatly from representative training examples. For instance, a BPE model could
be more reliable if learned on diverse surface forms. Transformer attention could learn syntactic dependencies much better if a variety of them occurs in the training
data. Those are just conjectures, I believe there is no proof. I do hope I am wrong about this.

If the conclusions from simulated low-resource experiments turn out to be different from realistic ones, then unfortunately, all those papers suddenly lose their
target audience. DE-YI users would not be interested since the insights from the RO-EN paper do not apply to DE-Yi which is really low-resource, and RO-EN users
can of course rely on systems trained on much more data that are certainly better.

Other than that it is convenient for researchers, there really is no need to simulate low-resource settings. There are plenty of language pairs for which training
data is actually scarce. Such low-resource scenarios are a real challenge, as people from the [Masakhane community](https://www.masakhane.io/) can tell you. What they can also tell you is that
**low-resource is not only about data** - and working on low-resource problems does not merely mean data acquisition.

Most languages that are low-resource in NLP are also low-resource in other ways. For instance, there might not be much text online simply because there is no
keyboard to type ([for Fon, now there is](https://bonaventuredossou.github.io/clavierfongbe/)!). Writing in that language might not have standardized spelling. Most texts that exist might be traditional stories,
hardly any news, technical writing or every-day conversation. Do such languages also have few people that speak them? Not necessarily. Some have millions of
speakers. This should give you a sense of the kind of work needed to address low-resourcedness in a holistic way.

A recent and very laudable effort to encourage research on real low-resource data sets is the Tatoeba Challenge, spearheaded by Jörg Tiedemann ([Tiedemann, 2020](http://www.statmt.org/wmt20/pdf/2020.wmt-1.139.pdf)).
The repository has data for a large number of language pairs - many of them real low-resource cases - and also provides baseline models. On top of that, data and
models are also available in Huggingface.

Of course there are also concerns about Tatoeba (e.g. too many language pairs for a benchmark, data versioning, train-dev-test domain mismatches), but I think we
are moving in the right direction. If you can, help Jörg collect data on Tatoeba, or brainstorm ideas how to make the challenge better. Check out [Masakhane's recent
WMT keynote](https://slideslive.com/38940745/lowresourcedness-beyond-data) for ways to contribute to Masakhane.

Recommendation
==============

Work on realistic low-resource data sets instead of simulated ones. Think of low-resourcedness as more than a data problem only.

FAQ
===

**Q: Isn't training models with different subsets of my training data useful to see impact of adding data?**

A: Yes it is. But do not call it a "low-resource experiment". Call it a "high-resource experiment where some training data was withheld".
