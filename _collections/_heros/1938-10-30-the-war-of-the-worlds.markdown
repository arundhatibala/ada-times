---
layout: post
title:  "EPFL's BiasBusters Untangle Movie Triumph"
author: BiasBusters
# date:   2023-12-02 20:20:35 +0200
image: 'assets/images/oscar-hero-bw.jpg'
image_caption: Through a meticulous analysis of over 40,000 plot summaries using state-of-the-art NLP techniques, the Bias Busters have dissected the very essence of plot characteristics that differentiate movies with critical acclaim, audience recognition, and commercial success.
position: center
---

Acclaimed screenwriter Woody Allen famously said that “If my films don’t show a profit, I know I’m doing something right.” Contrasting the financial success stories of recent Marvel movies, Allen’s perspective prompts a fundamental question: are cultural and commercial successes inherently different from critical acclaim, or are there more overlaps than one might anticipate? In short - what makes a successful film, succesful?

<br>

### Understanding our datasets 

For our analysis, we incorporate the following sources:
1. CMU Movie Corpus dataset with 40 000 plot summaries
2. IMDb non-commercial dataset + 50.000 scraped movie reviews
3. Budget and revenue numbers from Box Office Mojo
4. Audience and critic review scores from Rotten Tomatoes


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
<br><br>

Community detection in network analysis involves identifying groups of nodes or entities within a network that are more densely connected to each other than to the rest of the network. To explore genre-genre-associations, we constructed an undirected, weighted network with unique CMU movie genres as nodes. Each edge signifies that the two nodes (genres) are appearing together at least once in the dataset, and their weights were obtained by counting the total number of pair-occurrences in the dataset.
<br><br>

![Network Communities](images/network.png)
<br><br>


A popular choice for community detection, the <strong>Louvain algorithm</strong>, is based on the idea of optimizing modularity. Modularity quantifies the quality of a community structure by comparing the number of edges within communities to the expected number of edges if the network were randomly connected. The algorithm aims to maximize modularity score, indicating a strong community structure. An advantage of the algorithm is that it finds appropriate non-overlapping communities without having to specify the number of communities in advance. 
<br><br>

![Communities](images/communities.png)
<br><br>

For our network, the algorithm detected five communities. But how does one interpret community 0 to 4?

From the unsupervised, hierarchical clustering of the Louvain algorithm, we learnt a genre-community mapping without having to specify any hyperparameters. To interpret and label the communities, we observe the top 10 genres within each community (ranked on occurrence-count in the dataset). 
<br><br>

![Genres](images/genres.png)
<br><br>

### Put your Money where your Mouth is
<br><br>
To understand the commercial success of a movie, we can choose between a variety of metrics, like Return-on-Investment (ROI), Box-Office Revenue and Budget of the movie. However, the best analyses are simple. 

We establish a connection between the dimensions in the data by creating scatter plot. Of these, the two most interesting (in our opinion), are the following graphs.
<br><br>

<div class="container">
  <iframe class="responsive-iframe" src="budget_revenue.html"></iframe>
</div>
<br><br>

When we compare the budget and revenue, we see that higher investment in the production budget does not necessarily make the movie a commercial success. We see from the graph (and the data) that most movies are concentrated in the 0-50M budget category with a revenue between 0-0.5B.

Lighthearted movies are on average lower in budget but have a higher yield at the box office. We also see that that category contains the most expensive budgets.

If we apply a temporal axes, we can see how the budget changes for movies over the years.
<br><br>

<div class="container">
  <iframe class="responsive-iframe" src="year_budget2.html"></iframe>
</div>
<br><br>

We see that the budget stabilises over the years, inspite of inflation and overall increase in production cost and the size of the team working on a single movie.
<br><br>

So, what could be the cause of this? Lately, there has been wave of <strong>microbudgeting</strong>. Producers often fund indie films that don't require as much resources, but have a unique plot characteristic that makes them stand out in the crowd.
Movies from Everything Everywhere All at Once (not plotted) to Sister Act have shown to investors that it doesn't take much to make a movie that's commercially successful.

<div class="container">
  <iframe class="responsive-iframe" src="revenue_distribution_by_target_audience.html"></iframe>
</div>
<br><br>

Movies in the 'exciting' mood category have a median revenue of approximately 37 million, suggesting a strong box office performance for this type of film. The interquartile range of 12 million to 93 million indicates that while some films achieve outstanding financial success, there is variability in the revenue performance within this category. The presence of outliers above the upper whisker shows that some 'exciting' movies significantly outperform others in terms of revenue

<div class="container">
  <iframe class="responsive-iframe" src="revenue_heatmap_by_target_audience_and_mood.html"></iframe>
</div>
<br><br>

In this graph, what we see is that films for families tend to be more review-generating. 

Moreover, here is a clear indication that movies targeting teenagers tend to generate higher revenue on average, with 'exciting' and 'fantastical' moods standing out. This might reflect teenagers' preferences for genres such as action, adventure, or fantasy.

<!-- #### Plot Characteristics -->
<br><br>

### Playing to the Gallery
<br><br>

To understand our plot summaries better, we used <code>gpt-3.5-turbo</code> to categorise the plot summaries into new metrics, which include:
<br>

- Topic Identification: Categories like Romance, Adventure, Mystery, Comedy, etc.
- Mood Identification: Options such as Exciting, Dark, Romantic, etc.
- Target Audience Identification: Children, Teenagers, Adults, Families, Elderly.
- Temporal Setting Identification: Past, Modern, Future.
- Location Setting Identification: Real or Fictional.
<br>

The choice of these features was a careful balance between granularity and dataset size, aiming to capture the most significant elements of movie plots. Analyzing movie plots using ChatGPT 3.5 for feature generation revealed its knack for handling hefty data tasks. We smoothly processed large datasets, extracting valuable features without breaking a sweat. 

<br>

#### Getting Demo-Graphic

A standing ovation at Cannes is a dream of every filmmaker. Audience reception is perhaps one of the most important metrics in determining a movie's success. But are all audiences the same?
<br><br>

![boxplots](images/boxplots.jpg)
<br>
<br>

In our initial analysis, we compare the average audience rating with the category of target audience. Our most surprising find? Movies that have elderly people as a target demographic <strong> on average have a higher rating<strong> than other audience demographics!
<br>
<br>

![correlation](images/correlation.jpeg)
<br>
<br>

When considering the sentiments of the reviews in our IMDB dataset, we see that movies with a historical or past setting also has higher positive correlation with average review scores, and its statistically signficant!
So next time you're watching a period piece or a WW2 movie, remember, you're only proving our point :)
<br>

#### We're a bit sentimental

Finally, we conducted aspect-based sentiment analysis on the movie reviews we scraped using the IMDB ID. How's it different from regular sentiment analysis, you may ask?
<br>

Aspect-based sentiment analysis is like zooming in on a painting to appreciate the intricate brushstrokes instead of just admiring the whole masterpiece. It's a methodical approach that dissects text into specific elements—characters, themes, or topics—to understand the sentiments associated with each. While standard sentiment analysis offers an overall emotional tone, this approach digs deeper, like unearthing treasures hidden within the words. It's a way to decode the sentiments linked to particular aspects, giving a nuanced understanding and colorful insights into diverse emotions within the text.
<br>
<br>

![aspect](images/aspect.jpeg)
<br>
<br>

Analysing this plot, we see:
<br>
- Mixed: the mixed-label indicates a conflicted/nuanced opinion portrayed in the movie review. It appears most often for plot, originality and cast. Keep in mind that it is quite rare in the dataset.
- Neutral: this label indicates factual/descriptive language towards the topic. It is the most frequently associated with production.
- Not discussed: this label indicates that an aspect was not touched upon in the review. We clearly see that soundplay, visuals and production is dominating this sentiment, suggesting that audiences may care less about these aspects.
- Negative: the negative-label indicates movie critique on the associated aspect. We observe that movies are most frequently critiqued for their plot, lack of originality or dialogue
- Positive: this label indicates positive emotions towards the associated aspect. This is most often the case for cast and plot.



<!-- ####  -->

### Reaching critical mass

Finally, our critics are the ones' responsible for the red carpet reverie. These critics can make our break a movie, even when its well-received by the audience and a commerical success. For this metric, we used the RottenTomatoes TomatoMeter, which consists of ratings of movies assigned by movie critics, not the audience itself.

The average score given by critics, known as the TomatoMeter score, is used here to gauge how positively movies were received.
<div class="container">
  <iframe class="responsive-iframe" src="average_critic_scores_with_variance.html"></iframe>
</div>
<br><br>

Initially, we see higher scores on average, which may indicate that only the best-rated movies were reviewed or captured in the data during those early years. It could also reflect fewer movies being made or less complete data from that time.
After 1990, there's a clear rise in the number of movies reviewed, with a greater spread in how critics rated them. This suggests a more varied and representative collection of movie ratings to analyze from this period onward.

<div class="container">
  <iframe class="responsive-iframe" src="average_tomato_scores_by_community.html"></iframe>
</div>
<br><br>

To dive deeper into critical acclaim, it can be seen that movies with historical themes score highest among films released after the 1990s, likely due to their rich storytelling and production quality. This is similar to what we see in the audience recognition section as well. In contrast, horror films tend to have lower scores, possibly reflecting a tougher critic stance or the genre's niche appeal.
<br><br>
<!-- ### Locations and Our Metrics
<br><br>
<div class="container">
  <iframe class="responsive-iframe" src="final_map_revenue.html"></iframe>
</div>
<br><br> -->
In conclusion, we see that a film's performance can, in fact, be optimised to be at the box office level.