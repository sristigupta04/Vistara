# Vistara — Data Science & Machine Learning

> **Data Science and ML research, development, and deployment for Vistara**

Vistara is an intelligent accommodation and destination exploration platform.  
This repository section contains **only the Data Science / Machine Learning work**.

The ML system is designed to help users make better accommodation decisions through:

- Personalized recommendations
- Smart property ranking
- Trust and risk analysis
- Review intelligence
- Property/photo verification
- Explainable recommendations

---

## 1. Data Science Objective

The objective of the Vistara Data Science team is to build ML systems that convert platform data into useful, measurable intelligence.

### Main question

> **Given a user's requirements and available property information, how can Vistara identify, rank, explain, and assess the most suitable options?**

The Data Science work focuses on:

```text
Data
 ↓
Cleaning
 ↓
EDA
 ↓
Feature Engineering
 ↓
Model Development
 ↓
Evaluation
 ↓
FastAPI ML Service
 ↓
Vistara Application
```

---

## 2. ML Modules

### 2.1 Recommendation System

Purpose:

Recommend properties that are relevant to an individual user.

Potential inputs:

- Destination
- Budget
- Guests
- Stay duration/type
- Amenities
- Property type
- Location
- Reviews
- Ratings
- User preferences
- Previous interactions
- Search behaviour

Output:

```text
Property ID
Recommendation Score
Recommendation Reason
```

---

### 2.2 Smart Search & Ranking

The system should rank available properties according to the user's current requirements.

Possible ranking signals:

- Location relevance
- Price fit
- Amenities
- Property quality
- Reviews
- Rating
- Availability
- User preferences
- Stay type
- Trust/risk indicators

The ranking system should be measurable and explainable.

Example:

```text
Property A
Score: 0.91

Why recommended:
✓ Within budget
✓ Close to selected location
✓ Matches preferred amenities
✓ Strong review performance
```

---

### 2.3 Trust / Risk Analysis

Purpose:

Identify listings or activities that may require additional attention.

Possible signals:

- Unusual listing behaviour
- Review patterns
- Rating anomalies
- Listing information inconsistencies
- Image similarity
- Suspicious activity patterns

Output may include:

```text
Risk Score
Risk Level
Risk Indicators
```

The system is intended to **support human/admin review**, not automatically make irreversible decisions.

---

### 2.4 Review Intelligence

Purpose:

Convert large amounts of reviews into useful information.

Planned capabilities:

- Sentiment analysis
- Aspect extraction
- Aspect-level sentiment
- Common positive themes
- Common negative themes
- Review quality signals

Example:

```text
Cleanliness     → Positive
Location        → Positive
Communication   → Positive
Check-in        → Mixed
Value           → Positive
```

---

### 2.5 Property / Photo Verification

Purpose:

Provide signals that help identify potentially duplicated or suspicious property images.

Possible approaches:

- Image hashing
- Perceptual hashing
- Image embeddings
- Similarity comparison

Output:

```text
Similarity Score
Potential Duplicate
Verification Signal
```

---

### 2.6 Explainable Recommendations

Recommendations should not be treated as unexplained predictions.

The system should provide understandable reasons such as:

- Matches budget
- Matches destination
- Matches amenities
- Suitable for selected stay duration
- Strong reviews
- Good location relevance

---

## 3. ML Architecture

```text
                    VISTARA BACKEND
                          │
                          ▼
                   ML / FastAPI API
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
 Recommendation      Trust / Risk      Review Intelligence
     Model               Model               Model
        │                 │                 │
        └─────────────────┼─────────────────┘
                          │
                          ▼
                   Prediction / Score
                          │
                          ▼
                    Backend Response
                          │
                          ▼
                     Application
```

---

## 4. Recommendation Flow

```text
User Request
     ↓
Location
Budget
Guests
Amenities
Stay Type
Preferences
     ↓
Candidate Properties
     ↓
Feature Engineering
     ↓
Recommendation / Ranking Model
     ↓
Property Scores
     ↓
Top-K Results
     ↓
Explanation
     ↓
API Response
```

Example API response:

```json
{
  "property_id": 1024,
  "score": 0.91,
  "reasons": [
    "Matches budget",
    "Close to destination",
    "Matches preferred amenities"
  ]
}
```

---

## 5. Data Science Workflow

### Step 1 — Data Collection

Identify suitable datasets and data sources.

Potential data:

- Property/listing data
- Availability/calendar data
- Reviews
- Ratings
- Location data
- Amenities
- Price
- Property type
- User interaction data
- Booking behaviour

---

### Step 2 — Data Cleaning

Tasks:

- Missing-value analysis
- Duplicate detection
- Incorrect-value detection
- Data-type correction
- Outlier investigation
- Text cleaning
- Image/data validation

---

### Step 3 — EDA

Study:

- Data distributions
- Price distribution
- Rating distribution
- Property types
- Location patterns
- Amenities
- Review patterns
- Availability
- Relationships between important variables

---

### Step 4 — Feature Engineering

Create useful model features.

Examples:

```text
price_per_guest
distance_to_destination
review_count
average_rating
amenity_match_score
budget_difference
location_match
stay_type
availability_score
review_sentiment
trust_score
```

---

### Step 5 — Baseline Models

Before complex models, establish simple baselines.

Examples:

- Popularity-based recommendation
- Content-based recommendation
- Logistic Regression
- Decision Tree
- Random Forest
- Linear models where appropriate

Baselines provide a reference point for later models.

---

### Step 6 — Model Development

Potential approaches:

#### Recommendation

- Content-based filtering
- Collaborative filtering
- Hybrid recommendation
- Learning-to-rank approaches where appropriate

#### Risk

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient boosting where justified

#### Review Intelligence

- NLP preprocessing
- TF-IDF
- Sentiment classification
- Aspect-based analysis
- Transformer models if justified by data and resources

#### Image Verification

- Perceptual hashing
- Image embeddings
- Similarity models

The final algorithm should be selected based on data, evaluation results, explainability, and project constraints.

---

## 6. Model Evaluation

### Recommendation

Possible metrics:

- Precision@K
- Recall@K
- MAP
- NDCG
- Hit Rate

### Classification / Risk

Possible metrics:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion matrix
- ROC-AUC where appropriate

### Review Analysis

Possible metrics:

- Accuracy
- Precision
- Recall
- F1-score

### Image Similarity

Possible evaluation:

- Similarity threshold analysis
- Precision/recall for duplicate detection
- False-positive analysis
- False-negative analysis

Model selection should be based on measured performance rather than model complexity.

---

## 7. Data Strategy

A candidate research source is **Inside Airbnb**, which provides regional datasets including listings, calendar, reviews and neighbourhood-related information.

Before using any external dataset, verify:

- Relevance
- Data quality
- Availability
- Data dictionary
- Licensing
- Privacy considerations
- Feature coverage
- Label availability

Dataset selection will be finalized during the research phase.

---

## 8. Cold Start Problem

Recommendation systems may face limited information for:

### New User

There is little or no historical behaviour.

Possible solution:

Use explicit preferences:

```text
Destination
Budget
Guests
Amenities
Stay Type
Property Type
```

### New Property

There are few or no interactions.

Possible solution:

Use:

- Property metadata
- Location
- Price
- Amenities
- Images
- Reviews when available

This is one reason a hybrid recommendation approach may be useful.

---

## 9. ML API

The trained models will be exposed through a Python API service.

### Technology

```text
Python
FastAPI
Scikit-learn / other selected ML libraries
```

Example structure:

```text
ml-service/
│
├── api/
│   ├── main.py
│   └── routes/
│
├── models/
│
├── data/
│
├── notebooks/
│
├── src/
│   ├── preprocessing/
│   ├── features/
│   ├── recommendation/
│   ├── risk/
│   ├── reviews/
│   └── images/
│
├── tests/
│
└── requirements.txt
```

---

## 10. Example ML API Endpoints

Potential endpoints:

```text
POST /recommend
POST /rank
POST /risk-score
POST /review-analysis
POST /image-similarity
GET  /health
```

Example recommendation request:

```json
{
  "location": "Delhi",
  "budget": 3000,
  "guests": 2,
  "amenities": [
    "wifi",
    "air_conditioning"
  ],
  "stay_type": "overnight"
}
```

Example response:

```json
{
  "results": [
    {
      "property_id": 101,
      "score": 0.93,
      "reasons": [
        "Within budget",
        "Matches amenities",
        "Strong review performance"
      ]
    }
  ]
}
```

---

## 11. ML Quality Requirements

Every production-oriented model should consider:

- Input validation
- Missing data handling
- Consistent preprocessing
- Reproducibility
- Model versioning
- Error handling
- API response format
- Latency
- Monitoring
- Logging
- Evaluation metrics

The ML service should fail safely when required data is unavailable.

---

## 12. Research Phase — 14 Days

**Status: Completed**

All 14 days of the Data Science / ML Phase 1 research have been completed.

| Day | Data Science / ML Research | Status |
|---|---|---|
| 1 | AI/ML Research | Completed |
| 2 | AI/ML Competitor Comparison | Completed |
| 3 | ML / Data Gap Analysis | Completed |
| 4 | User Preference & Behaviour Data | Completed |
| 5 | ML Problem & Objectives | Completed |
| 6 | Recommendation / Trust / Review Intelligence | Completed |
| 7 | ML Differentiation | Completed |
| 8 | MVP ML Scope | Completed |
| 9 | ML Functional Requirements | Completed |
| 10 | Model / API Quality Requirements | Completed |
| 11 | Algorithm / Approach Research | Completed |
| 12 | Dataset & Data-Source Research | Completed |
| 13 | Final ML Research Conclusions | Completed |
| 14 | Lock ML Scope + Phase 1 Review | Completed |

### Phase 1 Outcome

The Data Science / ML research phase has now established:

- ML problem definitions
- User preference and behaviour signals
- Recommendation and ranking approach
- Trust/risk analysis scope
- Review intelligence scope
- Property/photo verification scope
- Explainability requirements
- MVP ML scope
- ML functional requirements
- Model evaluation requirements
- Algorithm research
- Dataset/data-source strategy
- ML API direction
- Final ML scope and Phase 1 decisions

**Phase 1 is complete and the Data Science / ML track is ready to move into implementation and system design.**

---

## 13. Current ML Scope

### MVP / Core

- Recommendation system
- Smart ranking
- Trust/risk analysis
- Review intelligence
- Property/photo verification
- Explainable recommendations
- FastAPI ML service
- Model evaluation

### Future Scope

These should not expand the MVP unless time and data justify them:

- Advanced dynamic pricing
- AI travel assistant
- Advanced personalization
- More sophisticated ranking models
- Automated regulatory/compliance intelligence

---

## 14. What Is Not Part of the ML Scope

The following are intentionally excluded from the current ML scope:

- Website identity-document upload verification
- Full Stack UI development
- Backend business logic
- PostgreSQL implementation
- Payment implementation
- Authentication
- Frontend implementation

ML only provides the intelligence/services required by the application.

---

## 15. Repository Structure

```text
ml-service/
│
├── README.md
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── external/
│
├── notebooks/
│   ├── EDA/
│   ├── recommendation/
│   ├── risk/
│   ├── reviews/
│   └── images/
│
├── src/
│   ├── preprocessing/
│   ├── features/
│   ├── recommendation/
│   ├── ranking/
│   ├── risk/
│   ├── reviews/
│   └── image_verification/
│
├── models/
│
├── api/
│   ├── main.py
│   ├── schemas/
│   └── routes/
│
├── tests/
│
├── requirements.txt
└── README.md
```

---

## 16. Data Science Development Principle

> **Start simple → establish a baseline → evaluate → improve → deploy.**

Do not choose a complex model simply because it is more advanced.

Every ML feature should have:

1. A clearly defined problem
2. Suitable data
3. Defined inputs
4. Defined outputs
5. A baseline
6. Evaluation metrics
7. Error analysis
8. A practical reason for inclusion

---

## 17. Final Data Science Goal

The Vistara Data Science system should transform raw platform data into reliable decision-support signals.

```text
RAW DATA
   ↓
CLEAN DATA
   ↓
FEATURES
   ↓
ML MODELS
   ↓
PREDICTIONS / RANKINGS
   ↓
EXPLANATIONS
   ↓
FASTAPI
   ↓
VISTARA
```

### Core ML Vision

> **Help Vistara understand users, properties, reviews and risk so that users can make better-informed accommodation decisions.**

---

## Status

**Track:** Data Science & Machine Learning  
**Current Phase:** Phase 1 — Research & Planning  
**Current Focus:** ML/Data Gap Analysis and research completion  
**Next Stage:** ML system design → dataset preparation → feature engineering → baseline models → model development
