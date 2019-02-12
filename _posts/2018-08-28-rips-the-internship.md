---
title: 'RIPS at IPAM, UCLA: The Internship'
date: 2018-08-28
permalink: /posts/2018/08/rips-the-internship/
tags:
  - internship
  - Praedicat
  - research
  - IPAM
  - life
  - knowledge
---
Research in Industrial Projects for Students (RIPS) is a summer undergraduate research program crossed with an industrial internship.  At the RIPS program, We all were given a problem faced by different industries, and our aim was to come up with a novel solution to fix that problem or to complete the model. Although, we were jolting down Math equations & numbers on a chalkboard all day, we could see a direct impact of those equations and those numbers on the industry. This is what makes the concept of the RIPS Program so unique; we were able to see the impact that we were creating in the industry through our research.

We were sponsored by the industry, [Praedicat Inc.](http://www.praedicat.com) which is an Insur-Tech company working towards assigning litigation risks to unforeseen chemical hazards. They achieve this feat through a complex chain of data analysis, prediction models and historical litigations. We, at Praedicat were given the task of working on one of the preliminary foundational portions of this complex chain - to mine credible data from the web for data analysis.

Our work was divided into three milestones:

![Three-Tier System Architecture, the Web Crawling framework, Information Classification & Aggregation and, Computational Fact-Checking using Knowledge Graphs](https://github.com/himahuja/pcatxcore/blob/master/img/EntireArchitecture.png?raw=true)

1. **Web Crawling Framework** *(From data to information)*: The modules contained in this component regulate the extraction of data from various sources on the Internet, and parse them into text formatted information.
2. **Information Classification & Aggregation** *(From information to knowledge)*: The textual information extracted using the Web Crawling Framework is pipelined into the Classification and Aggregation modules, which filter and prioritise the information into a master document for the analysts.
3. **Computational Fact-Checking using Knowledge Graphs** *(From knowledge to Wisdom)*: Even though, we were able to accumulate usable knowledge, the system was not yet intelligent to act upon that knowledge. To tackle this, we utilised computational fact-checking algorithms, which would allow the analysts to query a knowledge graph about the veracity of triples-based statements. As an advancement, we devised our own fact-checking algorithm, StreamMiner which had at par performance with the state-of-the-art methods.

We duly provided Praedicat Inc. and IPAM, the deliverables under the project. The data we accumulated for Praedicat through the above discussed architecture will make the process of data analysis faster, and more accurate.

The code is available publicly at [Github](https://www.github.com/himahuja/pcatxcore). We are still working on the StreamMiner algorithm. The code and paper for the algorithm will be made available soon.

Our report, results and outputs are available on request. Please mail at himahuja8[at]gmail[dot]com.
