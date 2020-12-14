---
title: 'Seven recommendations for machine translation evaluation'
date: 2020-12-15
permalink: /posts/2020/12/seven-recommendations-for-mt-evaluation/
tags:
  - machine translation
  - evaluation
  - best practices
  - recommendations
---

Evaluating machine translation systems is not as obvious as it seems on first glance. I know this from countless discussions with fellow researchers.
From countless Twitter feuds I also know that subtle things about MT evaluation are very hard to explain. I am dissatisfied with my Twitter-length answers,
and that is the reason for writing a series of blog posts. What you are reading now is a summary of all those posts, with pointers to each of them.

There are of course recent efforts to clarify best practices when it comes to MT evaluation. Most notably, there are efforts to 1) standardize computing and
reporting BLEU scores and 2) standardize human evaluation. Those developments are examples of positive and impactful change in our field, and I think it is interesting
to learn about them.

Then there are other aspects of MT evaluation that I feel are not getting the attention and care they deserve. To give just one example: many papers on
low-resource MT work with artificial data sets. This may hamper scientific progress in our field, since the conclusions drawn from experiments on realistic
low-resource
data sets could have been different. But then, there is no set of recommendations for low-resource MT or standard methodology, so I believe there is a lot
of uncertainty about it among authors and reviewers. 

In the blog posts below, I tried to address both: highlight existing efforts to establish best practices MT evaluation, and areas where I think best practices are
currently missing, but would be needed as well.

As an overview, I am listing all recommendations here, with links to individual posts.

Recommendations
===============

1. [When reporting BLEU scores, compute with translations that are fully postprocessed, and pristine references that have not been tampered with at all.](https://bricksdont.github.io/posts/2020/12/computing-and-reporting-bleu-scores/)

2. [Train several models of the same kind with different random seeds. Report and discuss the resulting variance.](https://bricksdont.github.io/posts/2020/12/single-training-runs/)

3. [Work on realistic low-resource data sets instead of simulated ones.](https://bricksdont.github.io/posts/2020/12/simulating-low-resource/)

4. [Use the most recent training and test sets available for a particular language pair and domain.](https://bricksdont.github.io/posts/2020/12/using-old-data/)

5. [Don't rely too much on statistical significance testing for automatic metrics. Focus on gains in automatic translation quality beyond standard deviation, or
ideally human evaluation.](https://bricksdont.github.io/posts/2020/12/statistical-significance-testing/)

6. [When designing your human evaluation, follow current best practices, for instance the ones laid out
in Läubli et al. (2020).](https://bricksdont.github.io/posts/2020/12/designing-human-evaluations/)

7. [Do not succumb to the urge of ignoring best practices just for the sake of comparing to
previous work.](https://bricksdont.github.io/posts/2020/12/comparing-to-previous-work/)

Way forward
===========

Basically, we are routinely tricking ourselves and others into thinking that we achieve scientific progress, when in fact we do not. I think that a small step
forward would be to establish further best practices and standardized methodology, and make them easily accessible.

In any case, I think that we ought to do better in the future. I will certainly hold myself (and people who have the questionable honor of being
reviewed by me) to very high standards for ongoing and future experiments.

There are some broader issues that ail our field, in my view. For instance, I consider **reproducibility** to be an unsolved problem at the moment.
Published results are hard to reproduce because the source code is not always available.

If authors do publish code, the next problem is that by "releasing code" what many people mean is releasing the library used to train
the particular models in a paper. What is almost never released is the workflow, scripts etc. necessary to reproduce the actual experiments.
As a consequence, reproducibility experiments are rarely undertaken in our field.

Issues like these are an impediment to scientific progress and perhaps worth exploring in future blog posts.

<hr style="border:2px solid gray">

FAQ
===

**Q: I found your paper X that does not actually follow your best practices! How is that possible?**

A: I anticipate that some people will point out that I myself did not always adhere to those practices in my own publications. I am well aware of this, and it's
worth pointing out that 1) as a PhD student I was still learning the ropes of conducting proper research and 2) of course people are perfectly capable of changing
their mind over the course of their career. I am the first to admit that certainly my own publications do not withstand scrutiny by the very best people in our field.
I do not think that my own shortcomings as a researcher somehow interfere with this post. It is certainly not true that only they who are innocent shall cast the
first stone, and some of the stones in this post I am casting on myself.

**Q: What can I do as an author if reviewers threaten to reject my paper if I do not play by their rules?**

A: Be steadfast, explain in a calm manner, flag for area chair attention if you believe you are treated unfairly.

Acknowledgements
================

I am indebted to Marcin Junczys-Dowmunt who frequently tweets calls to reason in MT research. For a long time I suggested he turn his tweets into blog posts ---
which I now have done for him. :-)

Thanks also to Bram Vanroy and other people with whom I have sparred on Twitter for inspiring me to write this post.

Thanks to the wonderful people who somehow --- while also doing awesome research --- found time to read an early version of those posts and helped to improve them considerably:
Annette Rios, Marcin Junczys-Dowmunt, Nitika Mathur, Samuel Läubli, Rico Sennrich, Julia Kreutzer, Noëmi Aepli and Matt Post.
