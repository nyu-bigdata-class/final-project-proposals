---
title: "Thistle"
author:
  - Brad Windsor <bwindsor22@gmail.com>
  - Kevin Choi <kc2296@nyu.edu>
---


For our Big Data and Machine Learning final project we plan to develop a vector database.

# Motivation
 
Most text search works off of the BM-25 algorithm, including [Elastic Search](https://www.elastic.co/blog/practical-bm25-part-2-the-bm25-algorithm-and-its-variables) and 
[Vespa](https://docs.vespa.ai/en/reference/bm25.html). This algorithm is an old variation on TF-IDF, largely based on term counts.

More recently, the advent of large-scale language models like [BERT](https://blog.google/products/search/search-language-understanding-bert/) have led 
to impovements on NLP benchmarks and [in search at Google](https://blog.google/products/search/search-language-understanding-bert/). One way of preprocessing text to
take advantage of language models is to feed the text throught the neural network and store the embeddings from the final layer.

Inspired by [Pinecone DB](https://www.pinecone.io/), this project aims to create a vector database that can mimic some of the features of elasticsearch while
taking advantage of vector representations.

# Proposed Solution


### Basic Design
Development will take place in Rust, using [oozie](https://docs.rs/oozie/0.1.2/oozie/index.html) or an equivalent library for vector operations.

The database will accept text data input, and accept text queries, and return query results based on rank.

### Sample Queries

Given the following dataset:

```
{
    'id': 1,
    'text': 'Do not go gentle into that good night',
    'author': 'Dylan Thomas',
    'era': 'Welsh early 1900s'
},
{
    'id': 2,
    'text': 'Shall I compare thee to a summer's day',
    'author': 'Shakespeare',
    'era': 'Old English'
},
{
    'id': 3,
    'text': 'What happens to a dream deferred?',
    'author': 'Langston Hughes',
    'era': 'American early 1900s'
},
```
Each of the following queries should return the expected result as its first hit:
```
// returns ID 1
{
  'text': 'stay strong as you grow older',
}

// returns ID 3
{
  'text': 'asleep',
  'era': 'United States'
}
```

### Research Topics
Some of the avenues for exploration in this project include:
* Building indexes of vectors, including [ANN](https://github.com/ZJULearning/efanna) search or [KD Trees](https://graphics.stanford.edu/papers/gkdtrees/gkdtrees.pdf)
* Building indexes when there are multiple vectors per entry, as with 'text' and 'era' tags above 
* Implementing a learn to rank feature so that vector rankings change over time
* Experimenting how [BERT](https://github.com/nghuyong/bert-classification-tf-serving) or [USE](https://arxiv.org/abs/1803.11175) should extract data with RUST as the operating code
* An [attention](https://arxiv.org/pdf/1706.03762.pdf) query as a means of comparing vectors
* Changing of vector clusters based on the addition of new metadata or of data streaming in
* Sharding across hosts 


This aims to be a database which can support a few sample queries, and progress can be evaluated based on the ability to support greater number of queries or return better examples.



# Timeline

* Checkin I (03/30): Ability to run RUST, familiarity with RUST vector libraries, and ability to extract embeddings from text
* Checkin II (04/20): Simple queries are working, an exploration of indexes is done
* Final Handin (05/11): Database is fully working, with one or two research topics broadly explored
