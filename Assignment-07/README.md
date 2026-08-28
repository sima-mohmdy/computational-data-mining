# Exercise 07 — PageRank

## Overview

In this exercise, the **PageRank algorithm** is implemented from scratch to rank web pages based on the structure of their hyperlinks.

The main idea is that a page is considered more important when it is linked to by other important pages.

## Dataset

The dataset contains pairs of web pages and their hyperlinks:

* `page_url`: the source page.
* `link_url`: the page linked from the source page.

Each unique URL is considered a node in the directed graph.

The dataset is not included in this repository due to its size.
The dataset was provided as part of the exercise materials.
Please place the dataset in the appropriate path before running the notebook.

## Method

The PageRank algorithm was implemented through the following steps:

### 1. Build the Directed Graph

A directed graph is created from the source and destination URLs. Each hyperlink represents a directed edge between two pages.

### 2. Construct the Transition Matrix `Q`

The transition matrix represents the probability of moving from one page to another by following a hyperlink.

If a page has `N` outgoing links, each outgoing link receives probability:

$$
\frac{1}{N}
$$

The matrix is defined as:

$$
Q[\text{destination},\text{source}] = \text{probability}
$$

### 3. Handle Dangling Nodes and Construct `P`

A **dangling node** is a page with no outgoing links. Its corresponding column in `Q` contains only zeros.

To keep the matrix stochastic, the probability is distributed uniformly among all pages:

$$
P_{ij} = \frac{1}{n}
$$

for a dangling column.

As a result, every column of `P` sums to approximately `1`.

### 4. Construct the Google Matrix `A`

To model both following hyperlinks and randomly jumping to another page, the Google matrix is constructed as:

$$
A = \alpha P + (1-\alpha)\frac{1}{n}E
$$

where:

* $\alpha = 0.85$ is the damping factor.
* $P$ is the transition matrix.
* $n$ is the number of pages.
* $E$ is an $n \times n$ matrix of ones.

### 5. Power Iteration

PageRank scores are computed using the **Power Iteration** method.

The initial PageRank vector assigns the same score to every page:

$$
r_0 = \frac{1}{n}\mathbf{1}
$$

The ranking vector is repeatedly updated using:

$$
q_k = Ar_{k-1}
$$

and normalized using the L1 norm:

$$
r_k = \frac{q_k}{\|q_k\|_1}
$$

The iterations continue until the difference between two consecutive ranking vectors becomes smaller than:

$$
10^{-6}
$$

### 6. Analyze the Results

The final PageRank scores are stored together with their corresponding URLs in a Pandas DataFrame.

The pages are then sorted in descending order to identify:

* The highest-ranked page.
* The lowest-ranked page.
* The PageRank score of a specific page.

## Result

The implementation successfully computes PageRank scores for all pages in the dataset and produces a ranked list of the web pages.

## Technologies

* Python
* NumPy
* Pandas
* Google Colab

## Key Concepts

* Directed Graphs
* Transition Probability Matrix
* Stochastic Matrix
* Dangling Nodes
* Google Matrix
* Damping Factor
* PageRank
* Power Iteration
* L1 Norm

