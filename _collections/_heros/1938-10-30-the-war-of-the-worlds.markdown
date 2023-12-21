---
layout: post
title:  "EPFL's BiasBusters Untangle Movie Triumph"
author: BiasBusters
date:   2023-12-02 20:20:35 +0200
image: 'assets/images/oscar-hero-bw.jpg'
image_caption: Through a meticulous analysis of over 40,000 plot summaries using state-of-the-art NLP techniques, the Bias Busters have dissected the very essence of plot characteristics that differentiate movies with critical acclaim, audience recognition, and commercial success.
position: center
---

Acclaimed screenwriter Woody Allen famously said that “If my films don’t show a profit, I know I’m doing something right.” Contrasting the financial success stories of recent Marvel movies, Allen’s perspective prompts a fundamental question: are cultural and commercial successes inherently opposed in the movie industry, or is this merely artistic disillusionment? 

### Understanding our datasets 

For our analysis, we incorporate the following sources:
1. CMU Movie Corpus dataset with 40 000 plot summaries
2. IMDb non-commercial dataset + 50.000 scraped movie reviews
3. Historic awards data from Academy Awards, Golden Globe & BAFTA
4. Budget and revenue numbers from Box Office Mojo
5. Audience and critic review scores from Rotten Tomatoes


Despite what most people think about genres, they may be ineffective in comparative multivariate analysis. In the CMU Movie Corpus dataset alone, there are 322 unique genre names, ranging from generic “Comedy” and “Drama” to hyper-specific “Beach Party Film” and “Kitchen Sink Realism” (what?). By limiting ourselves to the top 15 genres (based on label-count), we would preserve 57.09% of the preprocessed CMU dataset, potentially discarding important variability in niche-genres. The solution: unsupervised community detection in a genre-network.