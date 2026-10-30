# AI Service

Python FastAPI service that predicts the category and priority of a ticket from its text.

Current approach: TF-IDF features with Logistic Regression (scikit-learn), trained on synthetic samples.

Planned layout:

```
ai-service/
  main.py             FastAPI app
  train.py            Training script
  data/               Training data (synthetic now, real LAMISPlus data later)
  models/             Saved model files (not committed)
  requirements.txt    Python dependencies
```

Notes:

- Install the dependencies listed in requirements.txt inside a virtual environment.
- The service runs on port 8000.
- Newer scikit-learn versions removed the multi_class argument from LogisticRegression, so leave it out.
- Do not commit patient data. Any real dataset must be de-identified before it goes into this repository.
- DistilBERT is a possible upgrade once the dataset is large enough.
