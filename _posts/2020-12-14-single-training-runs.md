---
title: 'Single training runs and estimates of variance'
date: 2020-12-14
permalink: /posts/2020/12/single-training-runs/
tags:
  - machine translation
  - evaluation
  - best practices
  - randomness
  - variance
---

Consider a very simple example of a table reporting BLEU scores:

![simple BLEU table](/images/single-training-runs-1.png){: .align-center}

Is the number of encoder layers really the only relevant difference between those models? In an ideal experiment the treatment would
indeed be the only thing to change, but unfortunately that is not the case in MT experiments. Another noteworthy difference is random variation.

Random variation comes into play during neural network training because various steps use random number generators (RNGs).
Usually, RNGs are controlled by a random seed, which is an integer number. If the random seed is fixed, the behaviour of the RNG is
deterministic. Which parts of training an MT system are influenced by a particular random seed? At least the following:

* Initial values for all learnable parameters. The number of learnable parameters in an NMT systems is on the order of hundreds of millions.
* Batch construction and order in which batches are presented for model updates.
* For large data that is sharded, order in which shards (subsets of the entire training corpus) are loaded and used for training.
* Dropout, scheduled sampling and similar regularization techniques that make random changes to the model or training procedure.

This means that the same model trained on the same data with the same training procedure can lead to varying performance, depending on the
random seed. Now let's assume we did indeed train several models with different random seeds, which would allow us to report standard deviation:

![BLEU results of several runs with variance](/images/single-training-runs-2.png){: .align-center}

Now we are in a much better place. We can conclude that more encoder layers probably does not improve translation quality. By pure chance alone,
the baseline score could have been as high as 37.5.

Another way of looking at those results is saying that any particular BLEU score is taken from a distribution of possible BLEU scores (the distribution
we would get if we trained a system with every possible random seed). Based on two small samples from such distributions (by "sample" I mean, for instance,
3 BLEU scores obtained by training 3 baseline models with different random seeds), the question is: how likely is it that they come from the same underlying
distribution? In this case the answer is: very likely.

I should give concrete examples here I feel, and who better to call out than my past self? If you look closely at one of our recent publications:
[Müller et al. (2020)](https://www.aclweb.org/anthology/2020.amta-research.14/), you will notice: like many other papers, this one reports BLEU scores for single runs.
Now, very experienced MT researchers would point out the following: yes, it is true that only single runs are reported, but the absolute gains over the baseline
are between 1.5 and 3.0 --- which is probably more than one or even two standard deviations.

This view (of trusting BLEU gains above a certain threshold) has a long tradition in machine translation. Anecdotally, many people believe that an absolute
improvement over the baseline of 1 BLEU or more is significant ([Clark et al., 2011](https://www.aclweb.org/anthology/P11-2031.pdf)). But is this really true in general? I believe that is not the case.
Out-of-domain translation (the main focus of [Müller et al., 2020](https://www.aclweb.org/anthology/2020.amta-research.14/)) could indeed be an exception to this rule.

To prove my point (and to prove that not all my research is shady!), here is another recent paper of ours: [Rios et al. (2020)](https://www.statmt.org/wmt20/pdf/2020.wmt-1.64.pdf). The main goal of the paper
is improving zero-shot translation in multilingual systems. We report the results for three independent runs of the baseline:

![Numbers taken from Rios et al. (2020)](/images/single-training-runs-3.png){: .align-center}

What is truly baffling about this is that for the trained directions, the standard deviation is considerably below 1
BLEU, as expected, and you would certainly be right to trust improvements if they are above this threshold. But for zero-shot translation, the standard
deviation is thirty times higher! This means that for zero-shot translation, a gain of 1 BLEU over the baseline is well within one standard deviation of
the baseline and it would be ridiculous to claim victory.

This just goes to show that there are circumstances in which you cannot trust your well-calibrated gut feeling about what constitutes a significant gain
in BLEU. I have an inkling that this is especially true if MT models are used in unexpected settings such as out-of-domain or zero-shot translation.

Another fun fact: several training runs and accounting for "optimizer instability" was en vogue in the days of SMT ([Clark et al., 2011](https://www.aclweb.org/anthology/P11-2031.pdf))! There is no
reason it can't be brought back now.

Recommendation
==============

Train several models of the same kind with different random seeds, at least for the baseline. Report and discuss the resulting variance.
When discussing "gains" over the baseline, compare to the standard deviation caused by randomness alone.

Be extra careful if your MT systems are used in out-of-distribution settings such as for zero-shot translation or under domain shift.

FAQ
===

**Q: Isn't training several models with different random seeds even more expensive than it already is? What about the environment?**

A: Yes, several training runs are more expensive and have a higher environmental impact than single runs. Still, there is also a cost attached to tricking ourselves
into thinking we have achieved progress when we have not.

**Q: Is neural network training really deterministic, even if a fixed RNG seed is used?**

No, most likely it isn't. I am specifically saying that if the seed is fixed, the behaviour of (only) the RNG is deterministic. Other aspects of the training
procedure can still be non-deterministic, such as [summing values on GPU with Tensorflow](https://stackoverflow.com/questions/50744565/how-to-handle-non-determinism-when-training-on-a-gpu). We've seen cases where training runs with identical random seeds
become divergent.
