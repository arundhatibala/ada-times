---
layout: post
title:  "EPFL's BiasBusters Untangle Movie Triumph"
author: BiasBusters
# date:   2023-12-02 20:20:35 +0200
image: 'assets/images/oscar-hero-bw.jpg'
image_caption: Through a meticulous analysis of over 40,000 plot summaries using state-of-the-art NLP techniques, the Bias Busters have dissected the very essence of plot characteristics that differentiate movies with critical acclaim, audience recognition, and commercial success.
position: center
---

Acclaimed screenwriter Woody Allen famously said that “If my films don’t show a profit, I know I’m doing something right.” Contrasting the financial success stories of recent Marvel movies, Allen’s perspective prompts a fundamental question: are cultural and commercial successes inherently opposed in the movie industry, or is this merely artistic disillusionment? 

<br>

### Understanding our datasets 

For our analysis, we incorporate the following sources:
1. CMU Movie Corpus dataset with 40 000 plot summaries
2. IMDb non-commercial dataset + 50.000 scraped movie reviews
3. Historic awards data from Academy Awards, Golden Globe & BAFTA
4. Budget and revenue numbers from Box Office Mojo
5. Audience and critic review scores from Rotten Tomatoes


Despite what most people think about genres, they may be ineffective in comparative multivariate analysis. In the CMU Movie Corpus dataset alone, there are 322 unique genre names, ranging from generic “Comedy” and “Drama” to hyper-specific “Beach Party Film” and “Kitchen Sink Realism” (what?). By limiting ourselves to the top 15 genres (based on label-count), we would preserve only 57.09% of the preprocessed CMU dataset, potentially discarding important variability in niche-genres. The solution: unsupervised community detection in a genre-network.

<br><br>

### Explaining our layers

This datastory functions on the foundation of multivariate analysis. The three layers of analysis are critical acclaim, audience recognition, commercial success. 

Critical acclaim delves into the qualitative evaluation of a movie's artistic merits, encompassing expert reviews and accolades. Audience recognition captures the pulse of public reception, including ratings, and reviews. 
Meanwhile, the commercial success layer scrutinizes financial metrics like box office revenue and profitability.

We believe this approach, that intertwined the three metrics, provides us with a comprehensive understanding of what makes a movie successful.

Ultimately, we believe this multivariate approach could empower industry stakeholders to make informed decisions, guiding marketing strategies, audience targeting, and future project selections based on a holistic understanding of a movie's performance at the box office.
<br><br>

### Introducing Communities

Community detection in network analysis involves identifying groups of nodes or entities within a network that are more densely connected to each other than to the rest of the network. To explore genre-genre-associations, we constructed an undirected, weighted network with unique CMU movie genres as nodes. Each edge signifies that the two nodes (genres) are appearing together at least once in the dataset, and their weights were obtained by counting the total number of pair-occurrences in the dataset.

![Network Communities](images/network.png)


A popular choice for community detection, the <strong>Louvain algorithm</strong>, is based on the idea of optimizing modularity. Modularity quantifies the quality of a community structure by comparing the number of edges within communities to the expected number of edges if the network were randomly connected. The algorithm aims to maximize modularity score, indicating a strong community structure. An advantage of the algorithm is that it finds appropriate non-overlapping communities without having to specify the number of communities in advance. 

![Communities](images/communities.png)

For our network, the algorithm detected five communities. But how does one interpret community 0 to 4?

From the unsupervised, hierarchical clustering of the Louvain algorithm, we learnt a genre-community mapping without having to specify any hyperparameters. To interpret and label the communities, we observe the top 10 genres within each community (ranked on occurrence-count in the dataset). 

![Genres](images/genres.png)
<br><br>

### Time to put your Money where your Mouth is

To understand the commercial success of a movie, we can choose between a variety of metrics, like Return-on-Investment (ROI), Box-Office Revenue and Budget of the movie. However, the best analyses are simple. 

We establish a connection between the dimensions in the data by creating scatter plot. Of these, the two most interesting (in our opinion), are the following graphs.

<div class="container">
  <iframe class="responsive-iframe" src="budget_revenue.html"></iframe>
</div>

When we compare the budget and revenue, we see that higher investment in the production budget does not necessarily make the movie a commercial success. We see from the graph (and the data) that most movies are concentrated in the 0-50M budget category with a revenue between 0-0.5B.

Lighthearted movies are on average lower in budget but have a higher yield at the box office. We also see that that category contains the most expensive budgets.

If we apply a temporal axes, we can see how the budget changes for movies over the years.
<br>

<div class="container">
  <iframe class="responsive-iframe" src="year_budget.html"></iframe>
</div>
<br>

We see that the budget stabilises over the years, inspite of inflation and overall increase in production cost and the size of the team working on a single movie.
<br>

So, what could be the cause of this? Lately, there has been wave of <strong>microbudgeting</strong>. Producers often fund indie films that don't require as much resources, but have a unique plot characteristic that makes them stand out in the crowd.
Movies from Everything Everywhere All at Once (not plotted) to Sister Act have shown to investors that it doesn't take much to make a movie that's commercially successful.

<div class="container">
  <iframe class="responsive-iframe" src="fig_bubble.html"></iframe>
</div>

#### Plot Characteristics

### Playing to the Gallery

A standing ovation at Cannes is a dream of every filmmaker. Audience reception is perhaps one of the most important metrics in determining a movie's success. But are all audiences the same?

In our initial analysis, we compare the 

#### 

### Reaching critical mass