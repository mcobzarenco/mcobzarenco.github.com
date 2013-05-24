---
layout: post
title: "The log-sum-exp trick"
date: 2011-04-29 15:24
comments: true
published: false
categories:
---

Probabilities

When dealing with Hidden Markov Models (HMMs), but in other cases as well, one often needs to compute quantities of the form:

$$ a = \log\sum_t e^{b_t} $$

with $b_i$ extremely small so that the above computation easily underflows. The trick also works when $b_t$ is large. For instance, in the classic problem of filtering, the posterior of ht is computed recursively:

$$ p(h_t\vert v_{1:t}) \equiv \alpha(h_t) = p(v_t\vert h_t)\sum_{h_t}\alpha(h_{t-1})p(h_t\vert h_{t-1})$$

The alphas above can get very small and one way of guarding against underflow is to work in log-space:

$$ \log \alpha(h_t) = \log p(v_t\vert h_t)+ \log \sum_{h_t}\exp(\log \alpha(h_{t-1}) + \log p(h_t\vert h_{t-1})) $$

Generically,

logsumexp({at})=log∑teat
And

log∑teat=log∑teateA−A=A+log∑teat−A
Where A=max{at}. The overhead paid for extra numerical accuracy is one maximisation operation and an extra subtraction for each element of the vector.
