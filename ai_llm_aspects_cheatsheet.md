# Large Language Model (LLM) Architecture Cheatsheet

## 1. **Introduction to LLM**
Large Language Models (LLMs) are AI models designed to understand and generate human-like text based on a massive amount of data. LLMs use deep learning techniques, specifically **transformers**, to process and generate natural language efficiently.

---

## 2. **Core Components of LLM Architecture**

### 2.1 **Tokenization**
- **Definition**: Converts raw text into smaller units (tokens), which are usually words, subwords, or characters.
- **Types**:
    - **Word-level**: Entire words are treated as tokens.
    - **Subword-level**: Breaks words into meaningful subwords (e.g., Byte-Pair Encoding, WordPiece).
    - **Character-level**: Each character is treated as a token.

### 2.2 **Embedding Layer**
- **Purpose**: Converts tokens into dense vector representations (embeddings) in a continuous vector space.
- **Techniques**:
    - **Word2Vec** / **GloVe**: Traditional word embeddings.
    - **Contextual Embeddings**: Created dynamically for each token (e.g., BERT, GPT embeddings).

### 2.3 **Positional Encoding**
- **Definition**: Since transformers lack sequence awareness, positional encodings provide information about the token's position in the sequence.
- **Common Methods**:
    - Sinusoidal functions
    - Learnable embeddings

---

## 3. **Transformer Architecture (Foundation of LLMs)**

### 3.1 **Self-Attention Mechanism**
- **Purpose**: Allows each token to focus on different parts of the input, learning dependencies between tokens.
- **Key Concepts**:
    - **Queries (Q)**, **Keys (K)**, and **Values (V)**: Input tokens are projected into these three vectors.
    - **Attention Weights**: Computed by taking the dot product between queries and keys, determining how much attention each word should give to others.

### 3.2 **Multi-Head Attention**
- **Definition**: Multiple attention heads run in parallel, allowing the model to focus on different parts of the input simultaneously.
- **Formula**: Combines results from multiple heads via concatenation and a final linear transformation.

### 3.3 **Feed-Forward Network (FFN)**
- **Description**: A simple fully connected network applied to each token independently after the attention mechanism.
- **Architecture**:
    - Linear layer → Activation (e.g., ReLU) → Linear layer.

### 3.4 **Layer Normalization**
- **Purpose**: Stabilizes training by normalizing inputs to have mean zero and variance one within each layer.

### 3.5 **Residual Connections**
- **Description**: Shortcuts between layers that help gradients flow through the network, improving training stability.

---

## 4. **Training Process**

### 4.1 **Pretraining**
- **Definition**: LLMs are pretrained on vast corpora using self-supervised objectives (e.g., predicting missing words, next word, or masking tokens).
- **Common Methods**:
    - **Autoregressive (AR)**: Predicts next token (e.g., GPT series).
    - **Autoencoding (AE)**: Predicts masked tokens (e.g., BERT).

### 4.2 **Fine-Tuning**
- **Definition**: LLMs can be fine-tuned on specific datasets for downstream tasks (e.g., classification, question answering).
- **Objective**: Adjust weights to perform better on specific tasks while leveraging the knowledge gained from pretraining.

---

## 5. **Types of LLMs**

### 5.1 **Autoregressive Models (AR)**
- **Definition**: Generates text by predicting the next token based on previous tokens.
- **Examples**: GPT, GPT-2, GPT-3, GPT-4.

### 5.2 **Autoencoding Models (AE)**
- **Definition**: Learns to reconstruct the input with some parts (usually tokens) masked.
- **Examples**: BERT, RoBERTa.

### 5.3 **Seq2Seq Models**
- **Definition**: Used for tasks where input and output are sequences (e.g., translation, summarization).
- **Examples**: T5, BART.

---

## 6. **Loss Function**

### 6.1 **Cross-Entropy Loss**
- **Purpose**: Measures the difference between predicted probabilities and the actual label (token).
- **Formula**:

$$
L = -\sum_{i} y_i \log(\hat{y}_i)
$$

where $$\(y_i\)$$ is the true label and $$\(\hat{y}_i\)$$ is the predicted probability.

---

## 7. **Key Optimizations**

### 7.1 **Gradient Descent**
- **Definition**: Optimization algorithm to minimize the loss function by adjusting the model’s weights.

### 7.2 **Adam Optimizer**
- **Description**: A variant of gradient descent that uses momentum and adaptive learning rates for faster convergence.

### 7.3 **Regularization Techniques**
- **Dropout**: Randomly sets activations to zero during training to prevent overfitting.
- **Weight Decay**: Adds a penalty on large weights to the loss function to encourage simpler models.

---

## 8. **Popular LLMs**

### 8.1 **GPT Series (OpenAI)**
- **Type**: Autoregressive model.
- **Purpose**: Text generation, dialogue, and more.
- **Key Feature**: Scalable; uses many layers and attention heads for powerful text generation.

### 8.2 **BERT (Google)**
- **Type**: Autoencoding model.
- **Purpose**: Tasks like sentence classification, named entity recognition, and question answering.
- **Key Feature**: Bidirectional attention, meaning it considers both past and future tokens.

### 8.3 **T5 (Google)**
- **Type**: Seq2Seq.
- **Purpose**: Translation, summarization, and other NLP tasks.
- **Key Feature**: Treats all tasks as text-to-text problems.

---

## 9. **Inference in LLMs**

### 9.1 **Greedy Search**
- **Definition**: Selects the highest probability token at each time step, without considering future options.

### 9.2 **Beam Search**
- **Definition**: Keeps track of the top-k most likely sequences and selects the best one based on cumulative probability.

### 9.3 **Temperature Sampling**
- **Purpose**: Controls randomness in generation. Lower temperature makes outputs more deterministic, while higher values make them more random.

---

## 10. **Challenges in LLMs**

### 10.1 **Compute and Memory Costs**
- **Issue**: LLMs require significant hardware resources for training and inference, particularly as model sizes increase.

### 10.2 **Bias and Fairness**
- **Issue**: LLMs can learn biases present in their training data, potentially leading to unfair or harmful outputs.

### 10.3 **Interpretability**
- **Challenge**: LLMs, like most deep learning models, are often seen as "black boxes" due to their complexity.

---

## 11. **Scaling LLMs**
- **Trend**: Larger models with more parameters and training data tend to perform better but come with increased costs.
- **Example**: GPT-3 has 175 billion parameters, compared to GPT-2's 1.5 billion.

---

## 12. **Applications of LLMs**
- **Text Generation**: Chatbots, storytelling, email composition.
- **Translation**: Automatically translating text between languages.
- **Summarization**: Summarizing articles, legal documents, etc.
- **Code Generation**: Assisting in writing code (e.g., GitHub Copilot).
- **Question Answering**: Answering user queries in a natural language format.

---

## 13. **Future Directions**
- **Efficiency**: Developing smaller, more efficient models (e.g., DistilBERT).
- **Multimodal Learning**: Integrating text, images, and other modalities.
- **Fine-tuning and Adaptability**: Better techniques for adapting LLMs to specific tasks with minimal data.
