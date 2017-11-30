---
title: Let's science the sh*t out of Toilet Paper Reviews 
description: Thousands of toilet paper reviews analyzed scientifically to determine the best quality products.
header: Let's Science The Sh*t Out Of Toilet Paper Reviews
duration: 7 minutes read
---

Toilet papers. Seems like an insignificant common household item. But, did you know that there are over fifty brands of toilet paper on just Amazon.com - with over 9000 products listings?

So, how exactly does one pick the right toilet paper to use - hopefully in a quantified, scientific way?

Lets look at the possible methods of evaluation:
* Physical / Mechanical tests
* Surveys
* Reviews

### Physical / Mechanical Tests
These often involve analyzing the physical characteristics of TP using tests such as the following:
* Water absorption test
* Paper strength using mechanical puncturing device
* Tearing tests

<img src="img/instron.jpg">
<div align="center" class="fs-08"><i><small> Instron - an electomechanical tension / compression device (Image credit: https://instron.us) </small></i></div>


&nbsp;

The good part about such types of evaluations is that they can be completely objective. The tests (if conducted properly) can objectively and precisely measure the aspect. 

The issue with this kind of evaluation, though, is that it is often impossible to arrive at tests that can objectively grade each and every aspect of a product - for eg. what kind of a test can be used to quantify "comfort" ? 

### Surveys
A possible solution to the above problem, is to perhaps involve the consumers in the grading process - after all who better to measure the product than the end users of the product itself!

Surveys work great if designed right. However, designing the right survey to incite unbiased responses can be challenging due to factors like [Response Bias](https://en.wikipedia.org/wiki/Response_bias). Even if we were to be able to come up with a questionnaire that records participants true responses across all aspects of the product, keeping it updated over time can get challenging. 

### Reviews
Reviews are informative nuggets of free text and are already available for most products that are sold on the internet. They are the voice of the consumers in a public forum. 

> " People often talk about the things they care about "

... and the same is true for online reviews. 

By itself, a single review represents an individual's experience - but these become even more interesting when we start to look at repeated patterns across many reviews.

What if we could use this information to scientifically come up with conclusions about the product?

Using Neural Networks + Natural Language Processing, it is possible to extract the topics and sentiment and attempt to quantify objective metrics for the product.

Lets take a look at how we can use this to analyze TP reviews from Amazon.com.

We crawl Amazon.com to gather reviews and do preprocessing to address the following issues:
* Unverified reviews - These are reviews by people who have not bought the product from the marketplace. Since there is no evidence that these buyers are genuine, we do not consider them.
* Old reviews - Consumer expectations and products change over time. Keeping this in mind, we remove reviews that are more than a couple of years old.
* Review spam - many brands and sellers create "fake" reviews or incentivize reviewers by giving away free samples of their products. This results in significant biases creeping into the review data of a product. We can mitigate this using outlier detection on the reviewer history to identify products that have significant spammy reviews.
* Product variant reviews - Some websites like Amazon group reviews of a bunch of products into the same listing - thankfully, Amazon does provide a (somewhat hidden - "show only this format") option to filter the reviews by variant.
* Too few reviews - it is difficult to draw meaningful conclusions based on a small number of reviews, hence for this exercise, we discard products with fewer than 200 reviews.

After the above clean ups, we ended up with 29574 reviews across 274 products (only considering upto 1000 most recent reviews for each product). 

We cluster the review sentences to extract the most spoken about topics in the reviews. Following are the recurring topics that start to emerge:

* Overall Product: *"the product was great", "did the job", etc.*
* Marketplace / Delivery: *"was delivered on time", "doorstep delivery" etc.*
* Paper Quality: "strong", "durable", "doesn't tear" etc.
* Comfort: "soft", "cushy", "its like wiping my fat bottom with angel tears" etc.
* Value For Money: "worth the price", "bargain", "rip off" etc.
* Lasts Long: "lasts forever", "ran out in a day" etc.
* Size: "not as big as expected", "just right in size" etc.
* Cleaning: "squeaky clean bum", "leaves quite a bit of fuzz behind" etc.
* Clogging: "clogs the sewer line", "gentle on the plumbing", "had to use the plunger" etc.
* Dispenser: "barely fit my holder" etc.

Some other low volume clusters are:
* Purchase as a gag gift
* Eco-friendlyness
* Use while travelling and in public restrooms
* Perfumed TPs :S

For the purpose of this exercise, we will not consider the top two topics in the above list - reason being that the "Overall Product" statements are too generic, loosely used and volume-wise dominates every other topic, and the "Marketplace / Delivery" topic is not directly related to the product. We discard the low volume clusters as well.

Let's look at the volume distribution for the number of sentences in each of the remaining clusters:

<div class="show-only-small" align="center">
  <iframe width="314" height="194" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1811714180&amp;format=interactive"></iframe>
</div>

<div class="show-only-large" align="center">
  <iframe width="575.4219664768625" height="355.4349555051674" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1061894387&amp;format=interactive"></iframe>
</div>



Each sentence is then passed to a sentiment classifier to arrive at the positive and negative polarity. This gives us a topic-wise polarity of the products. We can now start to compare topics across products to arrive at an overall product ranking.

The best products, according to our analysis are:

[//]: # (Best 2 - Overall)

<div class="show-only-small">
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=699489827&amp;format=interactive"></iframe>
  </div>
  
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=291609438&amp;format=interactive"></iframe>
  </div>
  
  
</div>

<div class="show-only-large">
  <div class="parent">
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=699489827&amp;format=interactive"></iframe>
    </div>
    
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=291609438&amp;format=interactive"></iframe>
    </div>
  </div>
</div>

... and the worst products on our list are:

[//]: # (Worst 2 - Overall)

<div class="show-only-small">
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1405553136&amp;format=interactive"></iframe>

  </div>
  
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=151801927&amp;format=interactive"></iframe>
  </div>
  
  
</div>
<div class="show-only-large">
  <div class="parent">
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1405553136&amp;format=interactive"></iframe>
    </div>
    
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=151801927&amp;format=interactive"></iframe>
    </div>
  </div>
</div>


Note that we not only have a ranking, but also a justification - for eg. the worst product is a Tubeless TP, which seems to have a lot of holder / dispenser related compaints.

We can even sort by any topic and pick the topic-wise best products, for eg. the best TPs for preventing clogging are:


[//]: # (Best 2 - Clog)

<div class="show-only-small">
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=883957297&amp;format=interactive"></iframe>
  </div>
  
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1522105939&amp;format=interactive"></iframe>
  </div>
  
  
</div>

<div class="show-only-large">
  <div class="parent">
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=883957297&amp;format=interactive"></iframe>
    </div>
    
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1522105939&amp;format=interactive"></iframe>
    </div>
  </div>
</div>

Why stop at just toilet papers?

We at the<span class="fw-400">review</span>index believe that similar techniques can be used for analyzing all kinds of reviews - which is why we've just launched a tool that creates spam filtered review summaries for any Amazon.com electronic / gadget / appliance.

You can try the tool out here: https://thereviewindex.com and let us know what you think in the comments section below.

<img src="img/shopping.jpg">



