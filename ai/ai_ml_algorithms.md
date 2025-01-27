# Machine Learning Algorithms

- [Supervised Learning](#supervised-learning)
    - Linear Regression
    - Logistic Regression
    - Decision Trees
    - Random Forest
    - Support Vector Machines (SVM)
    - k-Nearest Neighbors (k-NN)
    - Naive Bayes

- [Unsupervised Learning](#unsupervised-learning)
    - k-Means Clustering
    - Hierarchical Clustering
    - Principal Component Analysis (PCA)
    - t-SNE (t-distributed Stochastic Neighbor Embedding)

- [Ensemble Methods](#ensemble-methods)
    - Gradient Boosting
    - Bagging

- [Neural Networks](#neural-networks)
    - Artificial Neural Networks (ANN)
    - Convolutional Neural Networks (CNN)
    - Recurrent Neural Networks (RNN)

- [Reinforcement Learning](#reinforcement-learning)
    - Q-Learning
    - Deep Q-Networks (DQN)

- [Dimensionality Reduction](#dimensionality-reduction)
    - LDA (Linear Discriminant Analysis)
    - Autoencoders


## **Supervised Learning**

- **Linear Regression**
    - Predict continuous values based on input features.
    - **Example**: Predicting house prices based on size.

      ```python
      import numpy as np
      from sklearn.linear_model import LinearRegression
      # Sample data: Size (sq ft) and Price (in $)
      X = np.array([[1500], [1600], [1700], [1800], [1900]])
      y = np.array([300000, 320000, 340000, 360000, 380000])
      model = LinearRegression().fit(X, y)
      predicted_price = model.predict([[1750]])  # Predict price for a 1750 sq ft house
      ```

- **Logistic Regression**
    - Classification algorithm for binary outcomes.
    - **Example**: Email spam detection (spam or not spam).

      ```python
      from sklearn.linear_model import LogisticRegression
      # Sample data: Features (word frequencies) and Labels (0: not spam, 1: spam)
      X = np.array([[1, 0], [0, 1], [1, 1], [0, 0]])
      y = np.array([1, 0, 1, 0])
      model = LogisticRegression().fit(X, y)
      predicted_class = model.predict([[1, 0]])  # Predict class for new email features
      ```

- **Decision Trees**
    - Non-parametric model; splits data based on feature values.
    - **Example**: Classifying whether a customer will buy a product.

      ```python
      from sklearn.tree import DecisionTreeClassifier
      # Sample data: Features (age, income) and Labels (0: not buy, 1: buy)
      X = np.array([[25, 50000], [45, 60000], [35, 80000], [50, 120000]])
      y = np.array([0, 1, 1, 1])
      model = DecisionTreeClassifier().fit(X, y)
      predicted_class = model.predict([[40, 70000]])  # Predict for a new customer
      ```

- **Random Forest**
    - Ensemble of decision trees; reduces overfitting.
    - **Example**: Classifying iris species based on petal features.

      ```python
      from sklearn.datasets import load_iris
      from sklearn.ensemble import RandomForestClassifier
      iris = load_iris()
      X = iris.data  # Features: petal length, petal width, etc.
      y = iris.target  # Labels: species (0, 1, 2 for different iris species)
      model = RandomForestClassifier().fit(X, y)
      predicted_species = model.predict([[5.1, 1.5, 0.2, 0.3]])  # Predict species for new flower
      ```

- **Support Vector Machines (SVM)**
    - Finds a hyperplane to separate classes.
    - **Example**: Handwriting recognition (digits).

      ```python
      from sklearn.datasets import load_digits
      from sklearn.svm import SVC
      digits = load_digits()
      X = digits.data  # Features: pixel values of images (8x8 grid flattened)
      y = digits.target  # Labels: digits (0-9)
      model = SVC().fit(X, y)
      predicted_digit = model.predict([digits.data[0]])  # Predict for the first digit
      ```

- **k-Nearest Neighbors (k-NN)**
    - Classifies based on majority class among k-nearest neighbors.
    - **Example**: Recommending products based on user preferences.

      ```python
      from sklearn.neighbors import KNeighborsClassifier
      # Sample data: Features (rating1, rating2) and Labels (0: not interested, 1: interested)
      X = np.array([[5, 3], [4, 2], [3, 4], [2, 1]])
      y = np.array([1, 1, 0, 0])
      model = KNeighborsClassifier(n_neighbors=2).fit(X, y)
      predicted_interest = model.predict([[4, 3]])  # Predict for a new user
      ```

- **Naive Bayes**
    - Probabilistic classifier based on Bayes' Theorem.
    - **Example**: Sentiment analysis (positive, negative).

      ```python
      from sklearn.naive_bayes import GaussianNB
      # Sample data: Features (word frequencies) and Labels (0: negative, 1: positive)
      X = np.array([[2, 1], [1, 1], [0, 2], [3, 3]])
      y = np.array([1, 0, 0, 1])
      model = GaussianNB().fit(X, y)
      predicted_sentiment = model.predict([[2, 2]])  # Predict sentiment for new review
      ```

## **Unsupervised Learning**

- **k-Means Clustering**
    - Partitions data into k clusters by minimizing variance.
    - **Example**: Customer segmentation based on purchasing behavior.

      ```python
      from sklearn.cluster import KMeans
      # Sample data: Features (age, spending score)
      X = np.array([[25, 60], [30, 80], [22, 70], [35, 90], [40, 50]])
      model = KMeans(n_clusters=2).fit(X)
      predicted_clusters = model.predict(X)  # Predict clusters for the existing data
      ```

- **Hierarchical Clustering**
    - Creates a hierarchy of clusters (agglomerative or divisive).
    - **Example**: Organizing a set of documents based on similarity.

      ```python
      from sklearn.cluster import AgglomerativeClustering
      # Sample data: Features (term frequencies)
      X = np.array([[1, 2], [2, 3], [3, 1], [8, 9], [8, 8]])
      model = AgglomerativeClustering(n_clusters=2).fit(X)
      predicted_clusters = model.labels_  # Get cluster labels for each point
      ```

- **Principal Component Analysis (PCA)**
    - Reduces dimensionality by projecting data to lower dimensions.
    - **Example**: Visualizing high-dimensional data.

      ```python
      from sklearn.decomposition import PCA
      # Sample data: High-dimensional data points
      X = np.random.rand(100, 5)  # 100 samples, 5 features
      pca = PCA(n_components=2)
      X_reduced = pca.fit_transform(X)  # Reduce to 2 dimensions
      ```

- **t-SNE (t-distributed Stochastic Neighbor Embedding)**
    - Visualizes high-dimensional data in 2D/3D.
    - **Example**: Visualizing clusters in image data.

      ```python
      from sklearn.manifold import TSNE
      # Sample data: High-dimensional data points
      X = np.random.rand(100, 50)  # 100 samples, 50 features
      tsne_results = TSNE(n_components=2).fit_transform(X)  # Reduce to 2D for visualization
      ```

## **Ensemble Methods**

- **Gradient Boosting**
    - Builds models sequentially to correct previous errors.
    - **Example**: Predicting churn in customer datasets.

      ```python
      from sklearn.ensemble import GradientBoostingClassifier
      # Sample data: Features and Labels
      X = np.array([[1, 2], [2, 3], [3, 1], [8, 9], [8, 8]])
      y = np.array([1, 0, 1, 0, 1])
      model = GradientBoostingClassifier().fit(X, y)
      predicted_class = model.predict([[3, 2]])  # Predict for a new point
      ```

- **Bagging**
    - Reduces variance by training models on random subsets of the data.
    - **Example**: Predicting loan approval.

      ```python
      from sklearn.ensemble import BaggingClassifier
      from sklearn.tree import DecisionTreeClassifier
      # Sample data: Features and Labels
      X = np.array([[1, 2], [2, 3], [3, 1], [8, 9], [8, 8]])
      y = np.array([1, 0, 1, 0, 1])
      model = BaggingClassifier(DecisionTreeClassifier(), n_estimators=10).fit(X, y)
      predicted_class = model.predict([[2, 2]])  # Predict for a new sample
      ```

## **Neural Networks**

- **Artificial Neural Networks (ANN)**
    - Network of nodes (neurons) that processes data in layers.
    - **Example**: Image recognition tasks.

      ```python
      from sklearn.neural_network import MLPClassifier
      # Sample data: Features (pixel values) and Labels (digits)
      X = np.random.rand(100, 64)  # 100 samples, 64 features
      y = np.random.randint(0, 10, 100)  # Labels: digits 0-9
      model = MLPClassifier(hidden_layer_sizes=(50,)).fit(X, y)
      predicted_digit = model.predict([[0.1] * 64])  # Predict for a new image
      ```

- **Convolutional Neural Networks (CNN)**
    - Special type of ANN that works well with image data.
    - **Example**: Object detection in images.

      ```python
      # CNN is implemented using libraries like TensorFlow or PyTorch
      # Example code would involve creating layers like Conv2D, MaxPooling2D, etc.
      ```

- **Recurrent Neural Networks (RNN)**
    - Handles sequential data like time series or text.
    - **Example**: Language translation.

      ```python
      # RNN is implemented using libraries like TensorFlow or PyTorch
      # Example code would involve creating layers like LSTM or GRU for sequential data
      ```

## **Reinforcement Learning**

- **Q-Learning**
    - Model-free algorithm that learns optimal actions for given states.
    - **Example**: Training a robot to navigate a maze.

      ```python
      # Pseudocode for Q-learning is often implemented with custom environments
      ```

- **Deep Q-Networks (DQN)**
    - Uses deep learning to approximate Q-values.
    - **Example**: Playing games like chess or Go.

      ```python
      # DQN involves using neural networks for action-value function approximation
      ```

## **Dimensionality Reduction**

- **LDA (Linear Discriminant Analysis)**
    - A supervised technique for dimensionality reduction with class separability.
    - **Example**: Classifying types of flowers.

      ```python
      from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
      X = np.array([[5.1, 3.5, 1.4], [4.9, 3.0, 1.4], [4.7, 3.2, 1.3]])  # Features
      y = np.array([0, 0, 1])  # Labels: flower types
      lda = LinearDiscriminantAnalysis(n_components=2).fit(X, y)
      X_lda = lda.transform(X)  # Reduce dimensionality
      ```

- **Autoencoders**
    - Neural networks that learn efficient representations of data.
    - **Example**: Denoising images.

      ```python
      # Autoencoder implementation using Keras or TensorFlow
      ```
