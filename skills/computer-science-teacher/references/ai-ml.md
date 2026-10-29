# Playbook: artificial intelligence and machine learning

**Covers:** classical AI (search, heuristics, A*, adversarial search, constraint satisfaction, logic and knowledge representation, planning, probabilistic reasoning, Bayesian networks), machine learning (supervised, unsupervised, linear and logistic regression, k-NN, decision trees and ensembles, SVMs, naive Bayes, clustering, PCA), evaluation and generalization, neural networks and deep learning (backpropagation, optimization, regularization, CNNs, RNNs and LSTMs, attention, transformers), large language models, reinforcement learning (MDPs, value iteration, Q-learning, policy gradients), and the needed math (linear algebra, calculus, probability).

## What a complete answer contains

- **The problem formulation:** input space, output space, hypothesis class, loss function and objective. For classical AI, the state space, actions, transition model, goal test and cost.
- **The full math derivation,** not just the final formula:
  - the gradient of MSE, and the normal equation θ = (XᵀX)⁻¹Xᵀy derived from setting the gradient to zero;
  - the gradient of softmax with cross-entropy, simplifying to ŷ − y;
  - backpropagation via the chain rule for a two-layer network, writing the **shape of every matrix** at every step;
  - the bias–variance decomposition of expected squared error;
  - the Bellman equation, from the definition of the value function.
- **The probabilistic view:** minimizing MSE is maximum likelihood under Gaussian noise, cross-entropy is maximum likelihood for a categorical distribution, and L2 regularization is MAP estimation with a Gaussian prior. This view explains *why* the loss functions look the way they do.
- **A numeric example small enough to check by hand:** one gradient-descent step on three data points, one forward and backward pass through a tiny network, an attention computation with 2×2 matrices.
- **Code in three levels:** NumPy from scratch (so nothing is hidden), then the library equivalent (scikit-learn or PyTorch), noting what the library adds (numerical stability tricks, automatic differentiation, batching).
- **For deep learning architectures:**
  - convolution output size, ⌊(n + 2p − k)/s⌋ + 1, derived;
  - parameter counts;
  - the LSTM gate equations, and why gating fixes vanishing gradients;
  - scaled dot-product attention, softmax(QKᵀ/√d_k)V, including *why* √d_k (dot products of random vectors grow with dimension, which saturates the softmax);
  - multi-head attention, positional encodings, residual connections and layer normalization;
  - for LLMs: tokenization, the next-token prediction objective, pretraining versus fine-tuning, RLHF, and the limits of what the model actually does.
- **Evaluation done properly:** train, validation and test splits, cross-validation, data leakage, the confusion matrix with precision, recall, F1 and ROC/AUC computed from actual counts, calibration, and baselines.
- **For classical AI:** run the algorithm on a small graph or game tree (a BFS/DFS/UCS/A* expansion order table, minimax values with alpha-beta pruning shown), and prove properties (A* is optimal with an admissible heuristic for tree search, and with a consistent one for graph search).
- **Cite papers by authors, title and year** for the major ideas, because ML students are expected to read them.

## Comparison dimensions

Bias and variance, interpretability, data requirements, training and inference cost, assumptions about the data, behavior with high dimensions or outliers, and parametric versus non-parametric.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1763 | Thomas Bayes (published after his death) | Bayes' theorem |
| 1805 and 1809 | Adrien-Marie Legendre; Carl Friedrich Gauss | Least squares |
| 1847 | Augustin-Louis Cauchy | Gradient descent |
| 1901; 1933 | Karl Pearson; Harold Hotelling | Principal component analysis |
| 1943 | Warren McCulloch and Walter Pitts | The artificial neuron |
| 1950 | Alan Turing | "Computing Machinery and Intelligence" and the imitation game |
| 1956 | McCarthy, Minsky, Rochester and Shannon | The Dartmouth workshop, where "artificial intelligence" was coined (in the 1955 proposal) |
| 1950s | Richard Bellman | Dynamic programming and the Bellman equation |
| 1958 | Frank Rosenblatt | The perceptron |
| 1959 | Arthur Samuel | Self-learning checkers program, and the term "machine learning" |
| 1968 | Hart, Nilsson and Raphael | A* search |
| 1969 | Marvin Minsky and Seymour Papert | *Perceptrons*: the limits of single-layer networks, which contributed to the first "AI winter" |
| 1970; 1974; 1986 | Seppo Linnainmaa; Paul Werbos; Rumelhart, Hinton and Williams | Reverse-mode automatic differentiation; backpropagation for neural networks; the *Nature* paper that popularized it |
| 1982 | John Hopfield | Hopfield networks |
| 1984; 1986 | Breiman et al.; Ross Quinlan | CART decision trees; ID3 |
| 1989 | Chris Watkins | Q-learning |
| 1989 | George Cybenko | Universal approximation theorem |
| 1989 and 1998 | Yann LeCun et al. | Convolutional networks for digit recognition (LeNet) |
| 1995 | Corinna Cortes and Vladimir Vapnik | Support vector machines (soft margin) |
| 1997 | Sepp Hochreiter and Jürgen Schmidhuber | LSTM |
| 1997 | IBM | Deep Blue defeats Kasparov |
| 2001 | Leo Breiman | Random forests |
| 2009 | Fei-Fei Li et al. | The ImageNet dataset |
| 2012 | Krizhevsky, Sutskever and Hinton | AlexNet wins ImageNet, starting the deep learning era |
| 2013 | Tomas Mikolov et al. | word2vec |
| 2014 | Goodfellow et al.; Kingma and Ba; Bahdanau, Cho and Bengio; Srivastava et al. | GANs; the Adam optimizer; attention for neural machine translation; dropout |
| 2015 | Ioffe and Szegedy; He et al. | Batch normalization; ResNet and residual connections |
| 2016 | DeepMind | AlphaGo defeats Lee Sedol |
| 2017 | Vaswani et al.; Christiano et al. | "Attention Is All You Need" and the transformer; RL from human preferences |
| 2018 | Google; OpenAI | BERT; the first GPT |
| 2018 | Yoshua Bengio, Geoffrey Hinton and Yann LeCun | Turing Award for deep learning (announced 2019) |
| 2020; 2022 | OpenAI | GPT-3; InstructGPT and then ChatGPT (November 2022) |
| 2024 | John Hopfield and Geoffrey Hinton | Nobel Prize in Physics, for foundational work on neural networks |

This field moves fast. For anything after your knowledge cutoff, say so and point the student to current sources such as arXiv and the major conferences (NeurIPS, ICML, ICLR).

## Canonical sources

- Russell and Norvig, *Artificial Intelligence: A Modern Approach*
- Christopher Bishop, *Pattern Recognition and Machine Learning*
- Goodfellow, Bengio and Courville, *Deep Learning* (free online)
- Hastie, Tibshirani and Friedman, *The Elements of Statistical Learning* (free online)
- Kevin Murphy, *Probabilistic Machine Learning* (free online)
- Sutton and Barto, *Reinforcement Learning: An Introduction* (free online)
- Zhang, Lipton, Li and Smola, *Dive into Deep Learning* (free, with code)
- Andrej Karpathy's "Neural Networks: Zero to Hero" (builds backpropagation and GPT from scratch)

## Classic misconceptions

- "Neural networks work like the brain." The biological inspiration is loose; they are differentiable function approximators trained by gradient descent.
- "High accuracy means a good model." Not on imbalanced data: 99% accuracy on a 1%-positive problem can be the model that always predicts "negative".
- "More data always fixes the model." It can't fix a biased or mislabeled dataset, or a model class that is too simple.
- "Overfitting means high training error." Overfitting means low training error and high test error.
- "You can tune hyperparameters on the test set." That leaks information; use a validation set or cross-validation.
- "Correlation in the model means causation."
- "Gradient descent finds the global minimum." For non-convex losses it finds a local minimum or a saddle region; deep learning works anyway, for reasons that are still being researched.
- "LLMs look facts up in a database." They predict tokens from learned parameters, unless they are connected to retrieval tools.

## Question patterns

- Derive the gradient or the update rule, and do one step by hand.
- What are the shapes of every tensor in this network, and how many parameters does it have?
- Compute precision, recall and F1 from this confusion matrix.
- Is this model overfitting or underfitting? What would you change?
- Run A* or minimax with alpha-beta on this tree, and give the expansion order and the pruned branches.
- Compute the value function after k iterations of value iteration.
- Explain each line of this PyTorch training loop.

## Tools and artifacts to show

NumPy, scikit-learn, PyTorch, Jupyter notebooks, TensorBoard and other loss-curve plots, the TensorFlow Playground (playground.tensorflow.org), and attention visualizations.
