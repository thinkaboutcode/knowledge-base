# MLOps Pipeline Cheatsheet

## 1. **Problem Definition**
- **Business Objective**: Understand and clearly define the problem to be solved.
- **ML Objective**: Choose an appropriate machine learning task (e.g., classification, regression).
- **Success Metrics**: Define metrics (e.g., accuracy, precision, recall, MSE) and goals for the ML model.

## 2. **Data Engineering**
- **Data Collection**
    - Collect data from various sources (databases, APIs, logs).
    - Ensure data is reliable, consistent, and complete.

- **Data Storage**
    - Use scalable storage solutions (e.g., databases, data lakes).
    - Ensure data security and privacy (GDPR, HIPAA).

- **Data Validation**
    - Validate data for consistency, correctness, and missing values.
    - Check schema consistency across datasets.

- **Feature Engineering**
    - Transform raw data into features (scaling, encoding, feature selection).
    - Automate with feature stores (e.g., Feast, Tecton).
    - Track feature versions.

- **Data Preprocessing**
    - Handle missing values, outliers, and imbalanced data.
    - Split data into train/validation/test sets.
    - Apply normalization/standardization as needed.

## 3. **Model Development**
- **Model Selection**
    - Choose models based on the problem type (e.g., decision trees, neural networks).
    - Consider simple baselines and more complex models.

- **Model Training**
    - Implement version-controlled training scripts (e.g., in Python using `scikit-learn`, `TensorFlow`, `PyTorch`).
    - Use cross-validation to ensure model robustness.

- **Hyperparameter Tuning**
    - Use grid search, random search, or automated methods (e.g., Bayesian optimization, HyperOpt).
    - Track experiments and hyperparameters using tools like MLflow, Weights & Biases, or KubeFlow.

- **Model Evaluation**
    - Evaluate using performance metrics relevant to the problem (e.g., ROC-AUC for classification, RMSE for regression).
    - Ensure model generalizes well to unseen data (avoid overfitting).

## 4. **Model Versioning**
- **Model Version Control**
    - Use tools like DVC (Data Version Control) or Git to track model versions.
    - Store metadata (e.g., model architecture, hyperparameters, training dataset version).

- **Model Packaging**
    - Serialize models into portable formats (e.g., `joblib` for scikit-learn, `SavedModel` for TensorFlow).
    - Package dependencies and environment requirements (e.g., Docker, conda).

## 5. **Model Deployment**
- **Deployment Strategies**
    - Choose a deployment method: batch, real-time, or online.
    - Use serving platforms: TensorFlow Serving, TorchServe, FastAPI, Flask, or cloud services (AWS SageMaker, Azure ML).

- **CI/CD for ML**
    - Automate model deployment using CI/CD pipelines (GitLab CI, Jenkins, CircleCI).
    - Implement continuous training and deployment (CT/CD).

- **Model Monitoring**
    - Monitor model performance in production (drift detection, data quality).
    - Use tools like Prometheus, Grafana, Seldon, or cloud monitoring (AWS CloudWatch, Azure Monitor).

## 6. **Model Maintenance**
- **Model Retraining**
    - Set up triggers for retraining based on data drift, performance degradation, or scheduled intervals.
    - Automate retraining pipelines using Airflow, KubeFlow, or cloud orchestrators (e.g., AWS Step Functions).

- **Model Explainability**
    - Use explainability tools: LIME, SHAP, Captum to interpret model predictions.
    - Ensure models meet fairness and ethical AI guidelines.

- **Model Governance**
    - Ensure proper documentation and audit trails for models in production.
    - Set up access control and permissions for model modifications.

## 7. **Automation & Orchestration**
- **Pipeline Automation**
    - Use orchestration tools like Apache Airflow, Luigi, or cloud-native pipelines (AWS Step Functions, GCP Vertex AI).
    - Automate data ingestion, preprocessing, model training, evaluation, and deployment.

- **Experiment Tracking**
    - Use tools like MLflow, Kubeflow Pipelines, or Weights & Biases to track experiment metrics, code, and results.
    - Log model performance, data versions, and artifacts.

## 8. **Security & Compliance**
- **Data Security**
    - Encrypt data in transit and at rest.
    - Ensure compliance with regulations like GDPR or HIPAA.

- **Access Control**
    - Implement role-based access control (RBAC) for sensitive data and models.
    - Use tools like Vault for secret management.

- **Auditing & Compliance**
    - Track all model changes and data usage.
    - Implement model audit logs for future reference.

## 9. **Best Practices**
- **Reproducibility**
    - Ensure reproducibility of experiments by logging dependencies, versions, and random seeds.

- **Scalability**
    - Use distributed training and inference solutions (Horovod, Ray, Spark MLlib).
    - Scale infrastructure with cloud services (AWS, GCP, Azure).

- **Collaboration**
    - Facilitate collaboration between data scientists, engineers, and operations teams using tools like Git, JIRA, Confluence.

- **Testing**
    - Unit test data processing code and model logic.
    - Use tools like Pytest and assert model outputs for various edge cases.


# General-Purpose MLOps Pipeline on GitLab

## .gitlab-ci.yml

```yaml
stages:
  - setup
  - preprocess
  - train
  - evaluate
  - package
  - deploy

# 1. Setup stage: Install dependencies
setup:
  stage: setup
  image: python:3.9
  before_script:
    - pip install --upgrade pip
    - pip install -r requirements.txt  # Install necessary dependencies
  script:
    - echo "Environment setup complete."
  artifacts:
    paths:
      - venv/

# 2. Preprocess stage: Data preprocessing
preprocess:
  stage: preprocess
  image: python:3.9
  script:
    - python scripts/preprocess_data.py  # Data preprocessing script
  artifacts:
    paths:
      - data/processed/  # Save preprocessed data
  only:
    - main  # Only run on the main branch

# 3. Train stage: Model training
train:
  stage: train
  image: python:3.9
  script:
    - python scripts/train_model.py  # Model training script
  artifacts:
    paths:
      - models/  # Save trained model
    expire_in: 1 week  # Keep model artifact for a week
  only:
    - merge_requests
    - main

# 4. Evaluate stage: Model evaluation
evaluate:
  stage: evaluate
  image: python:3.9
  script:
    - python scripts/evaluate_model.py  # Evaluate model performance
  artifacts:
    paths:
      - reports/  # Save evaluation report (metrics, visualizations)
  only:
    - main

# 5. Package stage: Model packaging
package:
  stage: package
  image: python:3.9
  script:
    - python scripts/package_model.py  # Serialize model for deployment (e.g., pickle, ONNX)
  artifacts:
    paths:
      - package/  # Store packaged model
  only:
    - main

# 6. Deploy stage: Model deployment
deploy:
  stage: deploy
  image: python:3.9
  script:
    - python scripts/deploy_model.py  # Deployment script (e.g., Docker, FastAPI)
  environment:
    name: production
    url: https://my-model-service.example.com  # URL of deployed model
  only:
    - tags  # Only deploy on tagged commits
```
