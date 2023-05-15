# Causality, Causal Inference, and Causal Machine Learning
This repository contains my notes, highlights, and codes in my self-study process of learning about causality, causal inference, and finally causal machine learning.

## Causality videos of [Shawhin Talebi](https://www.youtube.com/watch?v=WqASiuM4a-A&list=PLz-ep5RbHosVVTz9HEzpI4d6xpWsc8rOa) from Youtube

**What is causality?** X causes Y if when all confounders are adjusted, an interevention in X results in a change in Y, but the vice versa is not true.

**How to formulate causality?** We cannot use basic algebra to formulate causality because algebra is symmetric and causality effect does not follow symmetric rules. Therefore, we should use an asymmetric formulation. To this end, we use *Structural Causal Models (SCMs)*. SCMs include the following models:
- Directed Acyclic Graphs (DAGs): In these graphs, edges are directed. It means that information through edges flow in one direction. Also, they called acyclic becuase if we move toward edges, we cannot return back to the same vertex.
- Structural Equation Models (SEMs): In these equations we use ":=" sign for demonstrating causality. This mathematical sign just works from left to right, not vice versa. For instance, $Y := f(X)$ means an intervention in X results in a change in Y, not vice versa.

**What is causal inference?** Answering questions based on causal connections.

**What is observation?** $P(Y|X)$ means probability distribution of $Y$ given the observation of $X$.

**What is Do-Operator?** it simulates and represents physical intervention in specific variable. For example, $do(X)$ means physical intervention in X. If we intervent physically in $X$, all causes effects on $X$ will be deleted. It means that if $X := f(Z)$ and we $do(X)$, $X := f(Z)$ is no longer true. Most of the time, physical intervention is not feasible or is not ethical.

**Rules of Do-calculus**
- Insertion/Deletion of observations 
$$P(Y|do(X),Z,W) = P(Y|do(X),Z)$$ if $W$ is irrelevant to $Y$.
- Action/Observation exchange
$$P(Y|do(X),Z) = P(Y|X,Z)$$ if $Z$ blocks all back-door paths from $X$ to $Y$.
- Insertion/Deletion of actions
$$P(Y|do(X)) = P(Y)$$ if there is no causal path from $X$ to $Y$.

**What is Confounding?** A confounding factor is anything that makes $P(Y|do(X))$ different than $P(Y|X)$. Confoundings are variables that inherently affect our observed variable. We should always discover our confounding variables to formulate and optimize our problem in the best way.

**What is causal effect?** It means quantifying causal impact of $X$ on $Y$. We can do this by doWhy + enonml Python packages. For instance, [see this code](causal_inference/Causal_inference.ipynb).

**What is causal discovery?** It means how to find causal model of data from its statistics. Causal discovery is a kind of inverse problem. In the following, I mention there tricks for causal discovery. A sample of practical causal discovery can be found in [this page](causal_discovery/causal_discovery.ipynb).
- Conditional independence testing: It means $X \mathrel{\unicode{x2AEB}} Y \Leftrightarrow P(X,Y) = P(X)P(Y)$. Conditional independence testing works like constraint-based approaches. This trick is being used in _PC algorithm_, _Fast Causal Inference (FCI)_, and _Inductive Causation_.
- Greedy search of DAG space: In this approaches, we can start with either a full-connected graph, or a graph without any edges, and continue towards greedy search in these spaces. This trick is being used in _Greedy Equivalence Search (GES)_, _Greedy Interventional Equivalence Search (GIES)_, and _Concave Penalized Coordinate Descent with Reparametrization (CCDr)_.
- Exploiting Asymmetries: In the following, I mention three flavors of asymetries. This trick is being used in _Linear Non-Gaussian Acyclic Model (LiNGAM)_, _Nonlinear Additive Noise Model_, _Post-nonlinear Causal Model (PCM)_, and _Granger Causality_.
    + Time asymetry
    + Complexity
    + Functional
- Hybrid approaches: This trick is being used in _Structural Agnostic Modeling (SAM)_, _Causal Additive Model (CAM)_, and _Causal Generative Neural Network (CGNN)_.

**Granger Causality**: Granger causality is a statistical hypothesis test used to determine whether one time series is useful in forecasting another. Granger Causality is based on the idea that if a time series $X$ can provide statistically significant information about the future values of time series $Y$, then $X$ is said to Granger-cause $Y$.
