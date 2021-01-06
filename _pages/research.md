---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

{% include base_path %}


My research revolves around usupervised problems in Computer Vision. Following,
you will find some projects I worked on in the past.

### Spectral Image Segmentation
Improving graph-based segmentation algorithms using long range neighborhoods
Graph based segmentation methods constantly rely on solving cut problems on graphs
whose pixel information is local, i.e., its color data only interacts with that of
its neighbours. The necessary insertion of global information is then given by the
user, who provides either the desired color distributions on each region, seeds or
bounding boxes, or it is learned through iterative algorithms, such as Grabcut 
(which still requires some supervision).

In my research over the past year, we were able to develop new global spectral
algorithms for graph based image segmentation that did not require any user
interaction. We did so by adding new edges to the usual image grid graph, which
brought up a notion of long range neighbours. We compensated the increase in the
number of edges by developing faster approximate solvers for this problem by using
importance sampling on the edge set. With that, we were able to improve established
results in Graph Cuts segmentation and Random Walk algorithms. 

### Direct Estimation of Apearence Models for Segmentation
Image segmentation can be easily accomplished if one knows the color
distributions of the regions they want to segment (background and foreground,
for example). With that information, methods like graph cuts and random walker
algorithms can effortlessly output the desired segments. Since the distributions
are not known a priori, solutions for image segmentation usually require some
kind of supervision, i.e., it depends on additional information from the user
about the desired regions.

In this project, we aimed at solving the image segmentation problem in an
unsupervised manner, posing it as a distribution estimation problem. Having the
image as our only source of information and assuming that the boundary between
the regions to be segmented is short, we notice that neighboring pixels almost
always fall into the regions. That fact lead us to consider the distributions of
neighboring pixel intensities, i. e., how often the colors appear next to each
other in the image. In this project, we showed that one can then recover the
region distributions using a tensorial Method of Moments estimator. Since the
proposed algorithm's time and memory complexity just scales with the number of
colors in the image, it is also very efficient for gray scale images.

### Data clustering with multi-way relationships
Data clustering consists in partitioning a dataset in $K$ groups of similar
points given a notion of similarity. Usually, the research in such a field tend
to focus in pairwise similarities relationships, which is the the base for the
most broadly used algorithms such as $K$-means. On the other hand, data that
have multi-way relationships, i.e., the similarities are computed over subsets
of three or more points, hasn't been studied very deeply over time. An example
of an application of this framework is what it is called Subspace Clustering.

The first step towards a solution for that problem is model the dataset as a
hypergraph $G$ and have the multi-way relationships be the weights on its
hyperedges. Taking the hypergraph to be $d$-uniform for simplicity (each
hyperedge contains precisely $d$ vertices) and defining a multi-way similarity
function $D$, the objective function $f$ we wish to minimize is the sum of
$d$-way similarities within each cluster. With that, we can start solving the
clustering problem in two ways:
* <em>Pose the it as an inference problem</em>. Assume that each vertex is a
  random variable with $K$ possible states and that $G$ represents a factor
  graph that relates these variables among themselves. Having $D$ to be part of
  the factors and defining a joint distribution on the variables accordingly,
  use belief propagation to find the marginal distributions of each vertex.
  Finally, take assign each point to the most probable state.
* <em>Pose the it as an optimization problem</em>. It can be shown that the
  minimization of $f$ can be modeled as an integer program that is a combination
  of Max-$K$-Cut and Max Set-Splitting problems. This program can be relaxed to
  a Semidefine Program (SDP) and solved using interior point methods, bearing
  good approximation ratios. For the case when $d = 2$, the SDP can also be
  solved iteratively using ADMM.

### SAR Image Segmentation
The aim of this project was initially to explore more robust methods for
segmenting the maps computed from the SAR data, but it ended up leading us to
developing new Level Set algorithms worth publications of their own. Level Set
methods are based on the propagation of a front that carries out the
optimization of a given cost function. Choosing this function is tricky since if
has to obey certain differential geometric properties and its computation has to
be efficient.

As it turns out, a simple generalization the objective function present in
Otsu's segmentation algorithm can be used to drive the Level Set segmentation
front, as it is shown in \cite{jeova2017otsu}. Furthermore, the use of an
infinite number of statistical moments in this framework, instead of only one,
can lead to even better results and can be applied to SAR Image Segmentation

### Level Sets for Image Segmentation
This particular project was attractive because it relied in first and foremost
statistically modeling the image data. From that model, it was possible to
extract more informative knowledge from the image, which can be the input for
the application of traditional segmentation algorithms. This approach to dealing
with SAR imagery was inspired by the fact that this kind of image, on one hand,
is famously hard to process due to its inherent noise type (called speckle) and,
on the other, its pixel intensities are well categorized by a family of
probability distributions called $\mathcal{G}^0$.

Our work showed that translating the image intensities to maps of statistics,
one computed for each pixel, can lead to much clearer segmentations, even using
simple algorithms such as Otsu's. Two maps were used in this research: an
estimated $\mathcal{G}^0$ parameter called roughtness and the Renyie Entropy.
