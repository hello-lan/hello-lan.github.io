---
layout: post
title: 主题模型
categories: Tech
tags: 自然语言处理
---

* content
{:toc}





## 一、什么是主题模型

主题模型是处理非结构化数据的一种常用方法，从名字中就可以看出，该模型的主要功能就是从文本数据中提取潜在的主题信息。主题模型不同于其他的基于规则或字典的搜索方法，它是一种无监督学习的方法。

主题可以由语料库中的共现词项所定义，一个好的主题模型的拟合结果应该如下所示：“health”、“doctor”、“patient”、“hospital”构成医疗保健主题，而“farm”、“crops”、“wheat”则构成农业主题。

主题模型的适用领域有：文档聚类、信息提取和特征选择。比如，纽约时报利用主题模型的结果来提升文章推荐引擎的功能。许多专家将主题模型应用到招聘领域中，利用主题模型来提取工作要求中的潜在信息，并用模型的拟合结果来匹配候选人。此外，主题模型还被用于处理大规模的非结构化数据，如邮件、顾客评论和用户社交数据。



## 二、LDA

LDA是目前最流行的主题模型，由Blei, David M.、Ng, Andrew Y.、Jordan于2003年提出，用来推测文档的主题分布。它可以将文档集中每篇文档的主题以概率分布的形式给出，从而通过分析一些文档抽取出它们的主题分布。

LDA模型的参数：

- 超参数alpha和beta：alpha表示"文档－主题"的密度，beta表示“主题－词语”密度。alpha越大，表示文档中包含更多的主题，而beta越大，表示主题中包含更多的词语。
- 主题个数：文档集合的主题个数，根据实际情况来设置，比如设为100。
- 主题中词语的个数：这个参数取决于你的真实需求，如果你的目标是提取主题信息，那么你最好选择较多的词语。如果你的目标是提取特征，那么你应该选择较少的词项。
- 迭代次数：算法的迭代次数



在python中，我们用[gensim](https://radimrehurek.com/gensim/)来使用主题模型



## 三、在主题空间中比较相似度

主题经常会被当做是一种实现另外一个目标的中间工具。根据主题模型，我们可以对每篇文档预估它来自每个主题的可能性，由此，可以在主题空间中比较两篇文档。这意味着，我们要根据两个文档是否描述相同的主题来判断它们是否相似，而不是通过词与词的比较。这是很有威力的，因为两个只有少量公共词语的文本文档实际上可能是在说明同一个主题，只是用了不同的阐述方式（例如：一个人在说美国总统，而其他人使用了巴拉克*奥巴马这个名字）。

我们把文档映射到主题空间，这就是说，我们要构造一个主题向量来概括这个文档。由于主题的个数（通常设为100）比可能的词语的个数要小，所以这相当于我们把维度降低了。这给计算带来了优势，因为比较100维的主题权重向量，要比比较词表大小的向量要快得多（词标中可能包含成千上万的词语）。

在训练主题模型的时候，可以设置主题个数为100，这是个随意的值，我们也可有设为20或200个。对多数用户来讲，这个值并不重要。例如你只把这些主题的使用当做一个中间步骤，那么系统的最终表现极少会对主题的个数敏感。这意味着，只要你使用了足够的主题，不管是100个主题还是200个主题，这个过程中得到的推荐并没有太大区别。100通常是个比较好的值(20对于一般的文档集合来说太少)。
