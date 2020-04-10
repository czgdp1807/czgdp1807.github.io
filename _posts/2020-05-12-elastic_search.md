---
title: Elasticsearch - An Insider View
layout: post
description: null
image: null
open_blog: false
suburl: "2020/05/12/elastic_search.html"
---

Elasticsearch, which was originally intended to be a recepie search engine for Shay Bannon's wife turned out to be one of the most popular open source project on Github more than 1400 contributors and currently being used by Github, Facebook and [a lot of other tech giants](https://www.elastic.co/customers/).

A few days back, my project mentor told me about Elasticsearch and it's capabilities and here I am sharing the knowledge which I have gained after reading some material about it. Basically, Elasticsearch is nothing but, elastic search i.e., a search which was elastic enough to scale up and down according to the requirements of the situation and that too without much efforts. It is an abstraction layer over a somewhat complex Lucene library. In this blog, I will be writing about the following insider aspects of Elasticsearch i) Data model; ii) Architecture; iii) Concurrency control; iv) Use cases.

### Data model

Elasticsearch stores data in JavaScript Object Notation(JSON) format. Anologous to a row in a table in relational database, we have JSON documents in elastic search with each document having some pre-defined fields a.k.a meta-fields which are used in retrieval of the documents relevant to the parameters in the search request. According to [1], the meta-fields are divided into following catagories,

**Identity meta-fields**

As the name suggests, these fields help in uniquely identifying a document in the data store. `_index`(specifies the index to which the document belongs), `_type`(specifies the document's mapping type or something analogous to table in RDBMS) and `_id`(simply the document's id) belong to this category.

**Document source meta-fields**

These are the fields which describe the content of the document. Value of the `_source` field is the useful content and `_size` is the size of the content in bytes.

**Indexing meta-field**

These are the fields which are handy at the time of indexing. `_field_names` contains the names of fields which contain anything but null and `_ignored` contains those fields in the document that have been ignored at the time of indexing.

**Routing meta-field**

`_route` is the only meta-field which belongs to this category. As the name suggests, it routes the document to a particular shard.

**Other meta-field**

An example of this category is `_meta` which contains application specific meta-data.

Now, let's move on to see how all the documents are organized to give lightening fast information retrival from the Elasticsearch's data store.

### Architecture

Elasticsearch is somewhat a heriarchy of the following concepts, mentioned in bottom-up manner,

**Documents**

As discussed before, we can say that, smallest piece of information along with it's metadata stored in JSON format can be termed as document in our context.

**Index**

Index is a logical entity specifying the control

**Shards**

Popular definition of shard is

4) Nodes
5) Cluster