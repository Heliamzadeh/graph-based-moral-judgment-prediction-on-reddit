
# Graph-Based Moral Judgment Prediction on Reddit
high-level NLP + network science contribution &amp; language-mediated social reasoning via graph structure


## Overview
This project investigates how collective moral judgments emerge in online communities by modeling social interaction structures rather than textual content. Using data from Reddit’s *Am I the Problem?* (AITA) subreddit, we transform large-scale discussion threads into interaction graphs and apply graph-based machine learning and Graph Neural Networks (GNNs) to predict crowd-sourced verdicts.
Unlike conventional NLP approaches that rely on semantic text analysis, this project demonstrates that **social dynamics alone—captured through graph topology, centrality, and message-passing—contain sufficient signal to forecast moral judgments at scale**.

## Research Motivation
Most text analytics and NLP systems focus on *what* users say. This work shifts the analytical lens toward *how* users interact. By abstracting discourse into graph structures, we explore whether collective judgments can be predicted from:
- interaction patterns,
- network position,
- influence dynamics,
- and community structure,

without access to post or comment text.

This framing connects NLP, social network analysis, and graph representation learning.

## Data Collection
Data was collected using the Pushshift Reddit API, covering:
- Submissions from r/AmItheAsshole
- Associated comment trees and user interactions

Raw datasets included:
- ~9.2 GB of comment data
- ~414 MB of submission metadata

To manage scale, the pipeline employed chunked reading, sampling, and filtering to retain posts with clear verdict labels:

Balanced subsets were constructed to mitigate class imbalance and support robust evaluation.

## Graph Construction
Each Reddit thread was converted into a **user–post interaction graph**:
- **Nodes:** users
- **Edges:** reply and interaction relationships
- **Directionality:** preserved to capture conversational flow
- **Temporal structure:** incorporated via comment ordering

Graph-level and node-level features included:
- Tree depth and branching factor
- Clustering coefficients
- PageRank, betweenness, eigenvector centrality
- Temporal dynamics of participation

These features encode influence, visibility, and discussion density without relying on textual semantics.

## Modeling Approaches
Multiple modeling paradigms were evaluated:

### Classical Graph-Based ML
- Random Forest (robust, interpretable baseline)
- XGBoost (optimized performance, non-linear interactions)

### Graph Neural Networks
- Graph Neural Networks (GNNs)
- Graph Convolutional Networks (GCNs)

GNN-based models leveraged message passing to capture:
- spatial influence between users,
- local and global interaction patterns,
- structural dependencies across the discussion graph.

Both binary (YTA vs. NTA) and multi-class classification settings were explored.

## Community Detection & Network Effects
Louvain community detection was applied to uncover modular structures and echo chambers. Analysis revealed:
- High modularity networks were associated with stronger consensus formation
- Influential users (high PageRank / eigenvector centrality) disproportionately shaped verdict outcomes
- Early commenters benefited from structural positioning advantages

These findings highlight how **network topology mediates moral consensus formation**.

## Results
Key empirical findings include:
- XGBoost achieved the strongest binary classification performance (~71% accuracy, highest ROC-AUC)
- Binary classification (YTA vs. NTA) outperformed multi-class setups
- Interaction-based features alone rivaled and sometimes outperformed text-based and multimodal baselines
- Structural signals consistently predicted verdict polarization

Overall, the results validate the hypothesis that **social interaction structure is a powerful proxy for collective judgment**.

## Key Contributions
- Demonstrates verdict prediction without textual content
- Bridges NLP, graph learning, and social computing
- Applies GNNs to large-scale moral reasoning data
- Provides empirical evidence of influence asymmetry in online discourse

## Tools & Technologies
- Python
- NetworkX
- scikit-learn
- XGBoost
- Graph Neural Networks / GCNs
- Community detection (Louvain)
- Pushshift Reddit API

## Future Work
- Integrating textual embeddings as a secondary signal
- Dynamic / temporal GNNs for evolving discussions
- Cross-subreddit generalization
- Real-time moderation and debate outcome forecasting

## References
See the full project report for detailed methodology, evaluation, and discussion.
