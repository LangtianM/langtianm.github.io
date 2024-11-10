---
layout: post
title: A Note on Mutual Information 
date: 2023-04-09
tags: Statistics Information_Theory Machine_Learning 
categories: Notes
citation: true
---

> This is a personal note I took a year ago when I was learning about the concept of Mutual Information for the first time. It was my initial encounter with information theory, and the materials I found didn’t provide clear definitions of the notations explicitly, which made it a bit challenging for me to follow. I rewrote everything in slightly more rigorous language, and in the end, I managed to understand it thoroughly from start to finish. Here, I’m sharing those notes from back then.



## Kullback–Leibler Divergence
> Note: $\log$ refers to $\log_{2}$ here.

A type of statistical distance to measure how one probability distribution $P$ is different from a second, reference probability distribution $Q$, denoted by $D_{KL}(P \mid\mid Q)$.

**Definition**: For  probability distributions $P$ and $Q$ defined on the same sample space $\mathcal{X}$ , let $X\sim P$, the Kullback–Leibler divergence (relative entropy) **from $Q$ to $P$** is defined as:
$$D_{KL}(P\mid\mid Q) = \mathbb{E}\left[ \log\left( \frac{P(X)}{Q(X)} \right) \right]  $$
This is only defined in the way if $Q(x) = 0$ implies $P(x) = 0$. When $P(x) = 0$, the corresponding term is interpreted as $0$ because $\lim_{ x \to 0^{+} }x\log(x)=0$.

- Interpretation 1 :
  $$
	 D_{KL}(P\mid\mid Q)= \mathbb{E}[\log(P(X) - \log Q(X))] $$
    which is the expected difference in log-likelihood
- Interpretation 2:$$ D_{KL}(P \mid\mid Q) = H(P, Q) - H(P) $$ 
which is the difference of cross entropy of $(P, Q)$ and the entropy of $P$

**Definition** (Entropy)  The entropy of a random variable $X$ is defined as: 
$$H(X) = \mathbb{E}[-\log p(X)]$$ 

**Definition** (Cross entropy) The cross entropy of the distribution $Q$ relative to a distribution $P$ is defined as: $$ H(P, Q) = -\mathbb{E}_{X \sim P}[\log Q(X)] $$ 
where $\mathbb{E}_{P}$ is the expected value operator with respect to the distribution $P$.

## Mutual Information
The mutual information of two random variable is a measure of the mutual dependence between the two variables. It quantifies the "amount of information" obtained about one random variable by observing the other random variable.

**Definition**: Let $(X, Y)$ be a pair of random variables over the space $\mathcal{X}\times \mathcal{Y}$ . If their joint distribution is $P_{(X, Y)}$ and the marginal distributions are $P_{X}$ and $P_{Y}$, the mutual information is defined as 
$$I(X;Y) = D_{KL}(P_{(X, Y)}\mid\mid P_{X} P_{Y}) = \mathbb{E}_{Y}[D_{KL}(P_{(X|Y)}\mid\mid P_{X})].$$ 
It is a measure of the price for encoding $(X, Y)$ as a pair of independent random variables when in reality they are not.

Note that MI is more general than correlation coefficient, which can only depict the linear relationship.

## Evaluation of Clustering Results
Let $X$ be a random variable indicating the label of a data point given by a clustering algorithm, $Y$ be a random variable indicating the true label of a data point. Then we can calculate their sample mutual information by: 
$$I(X, Y) = \sum_{i=1}^{k}\sum_{j=1}^{k}{\frac{|X_i\cap Y_j|}{N} \log_2\frac{N|X_i\cap Y_j|}{|X_i|\cdot |Y_j|}} $$ 
where $|X_i\cap Y_j|$ denote the number of data points with true label $j$ and be assigned with label $i$. 
The normalized mutual information is: $$ NMI(X, Y) = \frac{2I(X, Y)}{H(X)+H(Y)}, $$where $H(X)$, $H(Y)$ are entropies of $X$ and $Y$.
