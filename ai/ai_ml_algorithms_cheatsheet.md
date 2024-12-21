# Machine Learning Algorithms Cheatsheet

## 1. **Supervised Learning**

- **Linear Regression**
    - Predict continuous values based on input features.
    - **Example**: Predicting house prices based on size.
      ```python
      import numpy as np
      from sklearn.linear_model import LinearRegression
  
      # Sample data: Size (sq ft) and Price (in $)
      # X: 2D array with each row representing a house size
      # y: 1D array representing the corresponding prices
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
      # X: 2D array where each row represents the frequency of words in an email
      # y: 1D array representing whether the email is spam (1) or not (0)
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
      # X: 2D array where each row represents a customer's age and income
      # y: 1D array representing whether the customer bought the product (1) or not (0)
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
      # X: 2D array where each row represents ratings given by a user for two products
      # y: 1D array representing whether the user is interested (1) or not (0)
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
      # X: 2D array where each row represents frequencies of words in a review
      # y: 1D array representing sentiment (0 for negative, 1 for positive)
      X = np.array([[2, 1], [1, 1], [0, 2], [3, 3]])
      y = np.array([1, 0, 0, 1])
      
      model = GaussianNB().fit(X, y)
      predicted_sentiment = model.predict([[2, 2]])  # Predict sentiment for new review
      ```

## 2. **Unsupervised Learning**

- **k-Means Clustering**
    - Partitions data into k clusters by minimizing variance.
    - **Example**: Customer segmentation based on purchasing behavior.
      ```python
      from sklearn.cluster import KMeans
  
      # Sample data: Features (age, spending score)
      # X: 2D array where each row represents a customer's age and spending score
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
      # X: 2D array where each row represents term frequencies of a document
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
      # X: 2D array with 100 samples and 5 features each
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
      # X: 2D array with 100 samples and 50 features each
      X = np.random.rand(100, 50)  # 100 samples, 50 features
      
      tsne_results = TSNE(n_components=2).fit_transform(X)  # Reduce to 2D for visualization
      ```

## 3. **Ensemble Methods**

- **Gradient Boosting**
    - Builds models sequentially to correct previous errors.
    - **Example**: Predicting churn in customer datasets.
      ```python
      from sklearn.ensemble import GradientBoostingClassifier
  
      # Sample data: Features (age, tenure) and Labels (0: churn, 1: stay)
      # X: 2D array where each row represents a customer's age and tenure
      # y: 1D array representing whether the customer churned (0) or stayed (1)
      X = np.array([[25, 1], [45, 3], [35, 2], [50, 5]])
      y = np.array([0, 1, 1, 1])
      
      model = GradientBoostingClassifier().fit(X, y)
      predicted_churn = model.predict([[40, 4]])  # Predict churn for a new customer
      ```

- **Bagging**
    - Trains multiple models on subsets of the data to reduce variance.
    - **Example**: Credit approval prediction.
      ```python
      from sklearn.ensemble import BaggingClassifier
      from sklearn.tree import DecisionTreeClassifier
  
      # Sample data: Features (income, credit score) and Labels (0: not approved, 1: approved)
      # X: 2D array where each row represents an applicant's income and credit score
      # y: 1D array representing approval (1) or not (0)
      X = np.array([[50000, 700], [60000, 720], [45000, 680], [70000, 750]])
      y = np.array([1, 1, 0, 0])
      
      model = BaggingClassifier(base_estimator=DecisionTreeClassifier()).fit(X, y)
      predicted_approval = model.predict([[55000, 720]])  # Predict for a new applicant
      ```

## 4. **Neural Networks**

- **Artificial Neural Networks (ANN)**
    - Composed of layers of neurons; suitable for complex functions.
    - **Example**: Predicting stock prices.
      ```python
      from keras.models import Sequential
      from keras.layers import Dense
  
      # Sample data: Features (previous day prices) and Labels (current day price)
      # X: 2D array where each row represents the previous day's prices
      # y: 1D array representing the current day's price
      X = np.array([[100], [101], [102], [103], [104]])
      y = np.array([101, 102, 103, 104, 105])
      
      model = Sequential()
      model.add(Dense(1, input_dim=1))  # Single input feature
      model.compile(optimizer='adam', loss='mean_squared_error')
      model.fit(X, y, epochs=10)
      predicted_price = model.predict([[105]])  # Predict for a new price
      ```

- **Convolutional Neural Networks (CNN)**
    - Specializes in image recognition.
    - **Example**: Classifying images (e.g., cats vs. dogs).
      ```python
      from keras.models import Sequential
      from keras.layers import Conv2D, Flatten, Dense
  
      # Sample data: 64x64 RGB images
      # X: 4D array with shape (number of images, height, width, channels)
      # y: 1D array with binary labels (0: cat, 1: dog)
      X = np.random.rand(100, 64, 64, 3)  # 100 images
      y = np.random.randint(0, 2, size=(100,))  # Labels: 0 for cats, 1 for dogs
      
      model = Sequential()
      model.add(Conv2D(32, (3, 3), activation='relu', input_shape=(64, 64, 3)))
      model.add(Flatten())
      model.add(Dense(1, activation='sigmoid'))
      model.compile(optimizer='adam', loss='binary_crossentropy')
      model.fit(X, y, epochs=10)
      ```

- **Recurrent Neural Networks (RNN)**
    - Designed for sequential data (e.g., time series, NLP).
    - **Example**: Predicting the next word in a sentence.
      ```python
      from keras.models import Sequential
      from keras.layers import LSTM, Dense
  
      # Sample data: Sequences of words (encoded as integers)
      # X: 3D array where each row is a sequence of word encodings
      # y: 1D array representing the next word in the sequence
      X = np.random.rand(100, 10, 50)  # 100 sequences, 10 time steps, 50 features
      y = np.random.randint(0, 1000, size=(100,))  # Next word (integer encoding)
      
      model = Sequential()
      model.add(LSTM(50, input_shape=(10, 50)))
      model.add(Dense(1000, activation='softmax'))
      model.compile(optimizer='adam', loss='sparse_categorical_crossentropy')
      model.fit(X, y, epochs=10)
      ```

## 5. **Reinforcement Learning**

- **Q-Learning**
    - Learns action-value function for optimal actions.
    - **Example**: Training an agent to play a game.
      ```python
      import numpy as np
  
      # Sample data: Q-table initialization
      # Q: 2D array representing state-action values
      Q = np.zeros((5, 2))  # 5 states, 2 actions
      alpha = 0.1  # Learning rate
      gamma = 0.9  # Discount factor
  
      # Update Q-value for a state-action pair
      Q[0, 1] = Q[0, 1] + alpha * (reward + gamma * np.max(Q[1]) - Q[0, 1])
      ```

- **Deep Q-Networks (DQN)**
    - Combines deep learning with Q-learning.
    - **Example**: Playing Atari games.
      ```python
      from keras.models import Sequential
      from keras.layers import Dense
  
      # Sample data: Q-values for actions in the current state
      # model: Sequential neural network
      model = Sequential()
      model.add(Dense(24, activation='relu', input_shape=(state_space,)))  # Input: state features
      model.add(Dense(2, activation='linear'))  # Output: Q-values for 2 actions
      model.compile(optimizer='adam', loss='mean_squared_error')
      ```

## 6. **Dimensionality Reduction**

- **LDA (Linear Discriminant Analysis)**
    - Supervised method to reduce dimensions while preserving class separability.
    - **Example**: Facial recognition systems.
      ```python
      from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
  
      # Sample data: Features (pixel values) and Labels (faces)
      # X: 2D array with samples as rows and pixel values as columns
      # y: 1D array with labels corresponding to the identities of faces
      X = np.random.rand(100, 20)  # 100 samples, 20 features
      y = np.random.randint(0, 5, size=(100,))  # 5 different faces
      
      lda = LinearDiscriminantAnalysis(n_components=2).fit(X, y)
      X_reduced = lda.transform(X)  # Reduce to 2D
      ```

- **Autoencoders**
    - Neural network for unsupervised dimensionality reduction.
    - **Example**: Denoising images.
      ```python
      from keras.models import Sequential
      from keras.layers import Dense
  
      # Sample data: Noisy images
      # X: 2D array with samples as rows and pixel values as columns (flattened images)
      X = np.random.rand(1000, 784)  # 1000 samples of 28x28 images (flattened)
      
      model = Sequential()
      model.add(Dense(64, activation='relu', input_shape=(784,)))  # Encoder
      model.add(Dense(784, activation='sigmoid'))  # Decoder
      model.compile(optimizer='adam', loss='binary_crossentropy')
      model.fit(X, X, epochs=10)  # Train to reconstruct input
      ```

