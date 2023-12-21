---
layout: post
title:  "EPFL's BiasBusters Untangle Movie Triumph"
author: BiasBusters
date:   2023-12-02 20:20:35 +0200
image: 'assets/images/oscar-hero-bw.jpg'
image_caption: Through a meticulous analysis of over 40,000 plot summaries using state-of-the-art NLP techniques, the Bias Busters have dissected the very essence of plot characteristics that pave the way to cinematic triumph.
position: center
---
### Understanding our datasets

Despite what most people think about genres, they may be ineffective in comparative multivariate analysis. In the CMU Movie Corpus dataset alone, there are 322 unique genre names, ranging from generic “Comedy” and “Drama” to hyper-specific “Beach Party Film” and “Kitchen Sink Realism” (what?). By limiting ourselves to the top 15 genres (based on label-count), we would preserve 57.09% of the preprocessed CMU dataset, potentially discarding important variability in niche-genres. The solution: unsupervised community detection in a genre-network.