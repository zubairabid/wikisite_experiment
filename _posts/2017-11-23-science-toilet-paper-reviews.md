---
title: Let's science the sh*t out of Toilet Paper Reviews 
description: Thousands of toilet paper reviews analyzed scientifically to determine the best quality products.
header: Let's Science The Sh*t Out Of Toilet Paper Reviews
duration: 7 minutes read
---

Toilet papers. Seems like an insignificant common household item. We all use them everyday, but how often do we pay attention to this paper that touches our everyday lives? If you look to the internet, you will find that there are several sources that have researched, analyzed and discussed this often rearly thought about subject. 

So, given the plethora of information out there, how exactly does one pick the right toilet paper to use - hopefully in a quantified, scientific way ?

The possible methods of evaluation:
* Physical tests
* Surveys
* Reviews

### Physical/Mechanical Tests
These often involve studing the physical characteristics of TP using tests like the following:
* Water absorption test
* Paper strength using mechanical puncturing device
* Tearing tests

[image of Instron]

The good part about these kind of evaluations is that it is completely objective. The test results (if conducted properly) can objectively and precisely measure the aspect being measured. 

The issue with this kind of evaluation, though, is that it is often impossible to arrive at tests that can objectively grade each and every aspect of a product - for eg. what kind of a test can be used to quantify "comfort" ? 


### Surveys
A possible solution to the above problem, is to perhaps involve the consumers in the grading process - after all who better to measure the product than the end users of the product itself!


But, in order to understand what a customer thinks about a product there needs to be a channel or medium of communication. And often the channel that is used for evaluation studies are Surveys and Questionnaiers.

Designing the right survey to incite unbiased responses is challenging. And of course, the well documented [Response Bias](https://en.wikipedia.org/wiki/Response_bias), which is a wide range of cognitive biases that influences the participants to respond inaccurately. 

Hypothetically, even if we were to be able to come up with a magical questionnaire that records participants true responses accross all aspects of the product, it would be very likely impossible to combine the results of all the tests and decide on the best product - Are all questions equally important ? How does one determine how important each aspect is and assign weights for each question ?

### Reviews
Reviews are the ubiquitous nuggets of free text that all of us rely on. By itself, a single review reflects an individual's experience. However, this becomes even more interesting when we start to look at repeated patterns across masses of reviews.  

> " People often talk about the things they care about "

... and the same is true for online reviews.

Our hypothesis is that topics mentioned in the reviews are the very aspects of the product that people care about. 

Using Natural Language Processing, it is possible to extract objective metrics for each aspect in the form of sentiment associated with each topic.

However, there are a bunch of gotchas need to be overcome:
* Sites like Amazon group reviews of a bunch of products into the same listing - thankfully, Amazon does provide a (somewhat hidden) option to filter the reviews by variant.
* Review spam - many brands and sellers create "fake" reviews of their products to help promote them. However, doing this without levaing behind a trace is extremely difficult. We use basic outlier detection on the reviewer history to identify products that have significant spammy reviews.

Once we jump through these hoops, we end up with 29574 reviews across 274 products (only considering upto 1000 most recent reviews for each product). We can look into the reviews and analyze them for patterns.

We start off by removing the unverified reviews and clustering the review sentences to extract the most spoken about aspects in the reviews. Following are the topics that start to emerge:

* Overall Product: *"the product was great", "did the job", etc.*
* Marketplace / Delivery related: *"was delivered on time", "doorstep delivery" etc.*
* Paper quality: "strong", "durable", "doesn't tear" etc.
* Comfort: "soft", "cushy", "its like wiping my fat bottom with angel tears" etc.
* Value For Money: "worth the price", "bargain", "rip off" etc.
* Lasts Long: "lasts forever", "ran out in a day" etc.
* Size: "not as big as expected", "just right in size" etc.
* Cleaning: "squeaky clean bum", "leaves quite a bit of fuzz behind" etc.
* Clogging: "clogs the sewer line", "gentle on the plumbing", "had to use the plunger" etc.
* Dispenser: "barely fit my holder" etc.

For now, we do not consider the top two topics in the above list - reason being that the "overall product" statements are too generic, loosely used and volume-wise dominates every other topic and the "marketplace / delivery related" topic is not directly related to the product.

<div class="show-only-small" align="center">
  <iframe width="314" height="194" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1811714180&amp;format=interactive"></iframe>
</div>

<div class="show-only-large" align="center">
  <iframe width="575.4219664768625" height="355.4349555051674" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1061894387&amp;format=interactive"></iframe>
</div>


Apart from the above, the other recurring patterns (that had very low volumes compared to the above) were:
* Purchase as a gag gift
* Eco-friendlyness
* Use while travelling and in public restrooms
* Perfumed TPs :S

We then break down the sentiment associated with each statement in these topics. We arrive at an overall rating using the following attributes:
* Ratio of positive / negative counts of a product with expected positive / negative counts for each topic.
* Absolute volume of the topic mentions

A very simple scoring function for positive mentions of a topic `topic1` can be given by

<span class="code">
topic1_pos_score = (num_pos_for_topic1 / expected_num_pos_for_topic1) * log10(num_pos_for_topic1)
</span>

where the <span class="code"> num_pos_for_topic1 </span> is the number of positive mentions of topic1 and <span class="code">expected_num_pos_for_topic1</span> is the expected number of positive mentions (based on overall positive mentions across all products). The ratio of the actual counts and expected counts quantifies the magnitude of positive (or negative) sentiment, and the log10 helps us factor in the volume. We sum up the postive topic scores and subtract the negative topic scores to arrive at the final scores for each product.


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


We can even get the top TPs for each aspect, like for eg. the top TPs to avoid a clog are:


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






And the most comfortable are:


[//]: # (Best 2 - Comfort)

<div class="show-only-small">
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1671651341&amp;format=interactive"></iframe>
  </div>
  
  <div align="center">
    <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1159011893&amp;format=interactive"></iframe>
  </div>
  
  
</div>

<div class="show-only-large">
  <div class="parent">
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1671651341&amp;format=interactive"></iframe>
    </div>
    
    <div align="center" style="width:50%">
      <iframe width="289.11044270195214" height="369" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vT5hb9t8AfkVUi_PRbPJYwLk7JCTr6JbWvr4b2Zo0q4Cllw-73chBJw5rg46gjwA5yrfaH1XHWrTGtl/pubchart?oid=1159011893&amp;format=interactive"></iframe>
    </div>
  </div>
</div>








Why stop at just toilet papers?

We at the<span class="fw-400">review</span>index believe that this can be used for all reviews - which is why we've just launched a tool that creates spam filtered review summaries for any Amazon.com electronic / gadget / appliance.

Shopping is hard, lets use machine learning!



