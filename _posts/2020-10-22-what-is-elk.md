---
layout: post
title: ELK Stack Architecture
categories: ELK
tags: [ELK]
---

## What is the ELK Stack?
The ELK stack is a group of Open Source products designed for log’s monitoring,management and analytics.You can use the ELK Stack to manage all of your log data and analyze everything in real-time.

It is a collection of three open-source products — Elasticsearch, Logstash, and Kibana. They are all developed, managed ,and maintained by the company Elastic.

- E stands for ElasticSearch: used for storing logs
- L stands for LogStash : It is a log aggregator that collects and processes data from multiple sources, converts, and ships it to various destinations, such as Elasticsearch.
- K stands for Kibana: is a visutalization tool (a web interface) which is hosted through Nginx or Apache

![ELK](https://sysadminxpert.com/wp-content/uploads/2018/05/elk-stack.jpg)

![ELK]({{site.baseurl}}/assets/img/2020-10-22-what-is-elk/ELK.jpg)

## Small-sized Solution
For a small-sized development environment, the classic architecture will look as follows.One more component is needed or Data collection called Beats, which led to the stack being rebranded as the Elastic Stack. Beats is a family of lightweight data shippers that collect and send data from different machines and systems to the stack, in this case, to Logstash or Elasticsearch.

![ELK](https://logz.io/wp-content/uploads/2018/08/image21-1024x328.png)
## ELK Stack Architecture
However, for handling more complex pipelines built for handling large amounts of data in production, additional components are likely to be added into your logging architecture, for resiliency (Kafka, RabbitMQ, Redis) and security (nginx):
![ELK](https://logz.io/wp-content/uploads/2018/08/image6-1024x422.png)