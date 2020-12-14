---
title: 'Comparing to previous work'
date: 2020-12-14
permalink: /posts/2020/12/comparing-to-previous-work/
tags:
  - machine translation
  - evaluation
  - best practices
  - reimplementation
  - previous work
---

What is common between many of the questionable practices I blog about is that they are seemingly legitimized by saying

> We know that X (instead of best practice Y) is bad practice, but we wanted to compare to previous works A, B and C that all use X.

Which is a little nonsensical. Using this argument creates the impression that authors are forced to choose between practice X an Y.
In most cases, this is false and there is nothing stopping them from doing both Y (because it's a best practice) and X (to compare to previous work,
even if known to be flawed).

Best practice Y is the reference point for new experiments. If for any reason X and Y cannot be done both, then authors should consider very carefully
whether the comparison with previous work actually is valuable enough to justify deviating from Y. And whether a comparison using X is meaningful at all.

A concrete example without Xs and Ys: in a recent review I have pointed out that BLEU should not be computed on tokenized text.
The authors responded by saying that they do it to compare to previous work. If I had a chance to respond to their response, what I would ask is:

> Of course you can **also** compute BLEU on tokenized text for whatever reason, but why **only** on tokenized text?

Since tokenized BLEU implies non-standard, custom tokenization, the comparison will also be less meaningful. The only proper way to 
compare to previous work then is to reimplement that work and evaluate properly. Reimplementation of previous works can be a colossal effort of course,
but in many cases it is the only way to make fair comparisons.

Recommendation
==============

Follow current best practices, even if it means breaking with long-standing traditions. Be aware that the stated goal of wanting to compare to
previous work does not legitimize improper evaluation.

Reimplement previous works to make meaningful comparisons.
If reimplementation is not an option, it is perfectly acceptable to run a secondary evaluation to compare to previous work on its own terms.
