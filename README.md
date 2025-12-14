# CraveBot
## Intelligent Food Classification Hybrid RAG Chatbot and Calorie Awareness Engine

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![MachineLearning](https://img.shields.io/badge/Machine%20Learning-Random%20Forest-green)
![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-MIT-lightgrey)
![CI](https://img.shields.io/badge/CI-GitHub%20Actions-orange)

---

## Overview

CraveBot is an end-to-end machine learning system designed to classify food products
based on calorie awareness using nutritional information from the OpenFoodFacts dataset.
The project follows an industrial machine learning workflow and is built to be extended
into a production-ready API service.

---

## Objectives

- Build a scalable food classification system
- Process large-scale nutritional datasets
- Implement a reproducible ML pipeline
- Enable API-based inference for deployment

---

## System Architecture

OpenFoodFacts Dataset
        |
        v
Data Cleaning and Preprocessing
        |
        v
Feature Engineering
        |
        v
Model Training (Random Forest)
        |
        v
Evaluation and Inference
        |
        v
API and Deployment Layer

---

## Features

- Large-scale dataset ingestion
- Nutritional feature engineering
- Binary calorie classification
- Random Forest machine learning model
- Model evaluation using accuracy and confusion matrix
- API-ready inference design

---

## Dataset

Source: OpenFoodFacts

Access Method:
```python
from datasets import load_dataset
dataset = load_dataset("openfoodfacts/product-database", split="food")
```

Selected Features:
- fat_100g
- carbohydrates_100g

Target Label:
- low_calorie (boolean)

---

## Machine Learning Pipeline

1. Load dataset
2. Handle missing values
3. Select nutritional features
4. Train-test split (80/20)
5. Train Random Forest classifier
6. Evaluate model performance
7. Generate predictions

---

## Installation

Prerequisites:
- Python 3.8 or higher
- pip
- Jupyter Notebook

Install dependencies:
```bash
pip install -r requirements.txt
```

Example requirements.txt:
```text
datasets
pandas
polars
pyarrow
scikit-learn
fastapi
uvicorn
joblib
```

---

## Usage

Launch notebook environment:
```bash
jupyter notebook
```

Open:
```text
cravebot.ipynb
```

Execute all cells sequentially.

---

## API Documentation

Endpoint:
```text
POST /predict
```

Request body:
```json
{
  "fat_100g": 3.5,
  "carbohydrates_100g": 12.0
}
```

Response:
```json
{
  "low_calorie": true,
  "confidence": 0.87
}
```

Minimal FastAPI example:
```python
from fastapi import FastAPI
import joblib

app = FastAPI()
model = joblib.load("model.joblib")

@app.post("/predict")
def predict(data: dict):
    prediction = model.predict([[data["fat_100g"], data["carbohydrates_100g"]]])
    return {"low_calorie": bool(prediction[0])}
```

Run API:
```bash
uvicorn app:app --reload
```

---

## CI CD Pipeline

GitHub Actions configuration:
```yaml
name: CraveBot CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.10
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: echo "Add unit tests here"
```

---

## Model Evaluation

Metrics:
- Accuracy
- Confusion Matrix

Evaluation code:
```python
from sklearn.metrics import confusion_matrix
confusion_matrix(y_test, y_pred)
```

---

## Example Predictions

Fat(g) | Carbs(g) | Prediction
-------|----------|-----------
3.5    | 12.0     | Low Calorie
20.0   | 45.0     | Not Low Calorie

---

## Troubleshooting

Dataset loading failure:
- Verify internet connectivity

Memory issues:
- Use filtered dataset or higher RAM machine

Low accuracy:
- Add more nutritional features
- Tune hyperparameters

---

## Limitations

- Binary classification only
- Limited nutritional features
- Notebook-based training
- No hyperparameter optimization

---

## Future Improvements

- Multi-class nutrition classification
- Deep learning models
- Model explainability
- MLflow experiment tracking
- Docker and Kubernetes deployment

---

## Dependencies

```text
datasets
pandas
polars
pyarrow
scikit-learn
fastapi
uvicorn
joblib
```

---

## Contributors

```text
Your Name
```

---

## License

```text
MIT License

Copyright (c) 2025 Arafat Zaman Ratul

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
