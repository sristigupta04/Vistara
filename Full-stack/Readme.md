
# Vistara — Final Monorepo Structure

```text
Vistara/
│
├── apps/
│   │
│   ├── web/                              # Main Guest + Host Web App
│   │   ├── app/
│   │   │   │
│   │   │   ├── (auth)/
│   │   │   │   ├── login/
│   │   │   │   └── register/
│   │   │   │
│   │   │   ├── (guest)/
│   │   │   │   ├── page.tsx              # Home
│   │   │   │   ├── search/
│   │   │   │   ├── properties/
│   │   │   │   ├── wishlist/
│   │   │   │   ├── trips/
│   │   │   │   └── profile/
│   │   │   │
│   │   │   ├── host/
│   │   │   │   ├── dashboard/
│   │   │   │   ├── properties/
│   │   │   │   ├── bookings/
│   │   │   │   └── profile/
│   │   │   │
│   │   │   └── api/                       # Only if frontend-specific
│   │   │
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   ├── navbar/
│   │   │   ├── search/
│   │   │   ├── property/
│   │   │   ├── map/
│   │   │   ├── booking/
│   │   │   ├── review/
│   │   │   └── trust/
│   │   │
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── services/                      # API client calls
│   │   ├── types/
│   │   ├── public/
│   │   └── package.json
│   │
│   │
│   └── admin/                             # Admin Dashboard
│       ├── app/
│       │   ├── dashboard/
│       │   ├── users/
│       │   ├── properties/
│       │   ├── bookings/
│       │   ├── reviews/
│       │   ├── risk/
│       │   └── verification/
│       │
│       ├── components/
│       ├── services/
│       ├── hooks/
│       └── package.json
│
│
├── services/
│   │
│   ├── api-gateway/
│   │   ├── src/
│   │   │   ├── routes/
│   │   │   ├── middleware/
│   │   │   ├── proxy/
│   │   │   ├── config/
│   │   │   └── index.ts
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── auth-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   ├── middleware/
│   │   │   ├── validators/
│   │   │   └── index.ts
│   │   ├── prisma/
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── user-service/
│   │   ├── src/
│   │   ├── prisma/
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── property-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   ├── repositories/
│   │   │   ├── validators/
│   │   │   ├── events/
│   │   │   └── index.ts
│   │   ├── prisma/
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── search-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   ├── filters/
│   │   │   ├── ranking/
│   │   │   └── index.ts
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── availability-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   └── index.ts
│   │   └── package.json
│   │
│   ├── booking-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   ├── repositories/
│   │   │   ├── events/
│   │   │   └── index.ts
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── payment-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   ├── gateways/
│   │   │   ├── webhooks/
│   │   │   └── index.ts
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── cancellation-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   └── index.ts
│   │   └── package.json
│   │
│   ├── review-service/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── routes/
│   │   │   ├── services/
│   │   │   ├── repositories/
│   │   │   └── index.ts
│   │   ├── tests/
│   │   └── package.json
│   │
│   ├── wishlist-service/
│   │   ├── src/
│   │   └── package.json
│   │
│   ├── notification-service/
│   │   ├── src/
│   │   │   ├── consumers/
│   │   │   ├── producers/
│   │   │   ├── services/
│   │   │   └── index.ts
│   │   └── package.json
│   │
│   └── verification-service/
│       ├── src/
│       │   ├── controllers/
│       │   ├── routes/
│       │   ├── services/
│       │   └── index.ts
│       └── package.json
│
│
├── ml/
│   │
│   └── ml-service/
│       ├── app/
│       │   ├── api/
│       │   │   ├── recommendation.py
│       │   │   ├── ranking.py
│       │   │   ├── risk.py
│       │   │   ├── review.py
│       │   │   └── photo.py
│       │   │
│       │   ├── models/
│       │   │   ├── recommendation/
│       │   │   ├── ranking/
│       │   │   ├── personalization/
│       │   │   ├── risk/
│       │   │   ├── review/
│       │   │   └── photo/
│       │   │
│       │   ├── features/
│       │   │   ├── user/
│       │   │   ├── property/
│       │   │   └── interaction/
│       │   │
│       │   ├── pipelines/
│       │   │   ├── recommendation/
│       │   │   ├── risk/
│       │   │   ├── review/
│       │   │   └── photo/
│       │   │
│       │   ├── explainability/
│       │   ├── services/
│       │   ├── schemas/
│       │   ├── utils/
│       │   └── main.py
│       │
│       ├── datasets/
│       ├── notebooks/
│       ├── experiments/
│       ├── models/
│       ├── tests/
│       ├── requirements.txt
│       └── Dockerfile
│
│
├── packages/
│   │
│   ├── database/
│   │   ├── prisma/
│   │   │   ├── schema.prisma
│   │   │   ├── migrations/
│   │   │   └── seed.ts
│   │   └── package.json
│   │
│   ├── types/
│   │   ├── user.ts
│   │   ├── property.ts
│   │   ├── booking.ts
│   │   ├── review.ts
│   │   ├── payment.ts
│   │   └── index.ts
│   │
│   ├── api-contracts/
│   │   ├── auth/
│   │   ├── property/
│   │   ├── search/
│   │   ├── booking/
│   │   ├── payment/
│   │   ├── review/
│   │   └── ml/
│   │
│   ├── config/
│   │   ├── environment/
│   │   ├── constants/
│   │   └── index.ts
│   │
│   └── ui/
│       ├── Button/
│       ├── Input/
│       ├── Modal/
│       └── ...
│
│
├── infrastructure/
│   │
│   ├── docker/
│   │   ├── web/
│   │   ├── services/
│   │   └── ml/
│   │
│   ├── postgres/
│   ├── redis/
│   ├── rabbitmq/
│   └── storage/
│
│
├── docs/
│   │
│   ├── research/
│   │   ├── day-01/
│   │   ├── day-02/
│   │   ├── day-03/
│   │   └── ...
│   │
│   ├── architecture/
│   │   ├── system-architecture.md
│   │   ├── service-architecture.md
│   │   ├── ml-architecture.md
│   │   ├── data-flow.md
│   │   └── communication.md
│   │
│   ├── api/
│   │   ├── gateway.md
│   │   ├── auth.md
│   │   ├── property.md
│   │   ├── booking.md
│   │   └── ml-api.md
│   │
│   ├── database/
│   │   ├── er-diagram.md
│   │   ├── schema.md
│   │   └── data-dictionary.md
│   │
│   ├── ml/
│   │   ├── recommendation.md
│   │   ├── ranking.md
│   │   ├── risk.md
│   │   ├── review-intelligence.md
│   │   ├── photo-verification.md
│   │   └── explainability.md
│   │
│   └── decisions/
│       ├── ADR-001-architecture.md
│       ├── ADR-002-database.md
│       └── ADR-003-ml-service.md
│
│
├── scripts/
│   ├── setup.ts
│   ├── seed.ts
│   ├── migrate.ts
│   └── test-all.ts
│
├── .env.example
├── .gitignore
├── docker-compose.yml
├── package.json
├── turbo.json
├── README.md
└── LICENSE
```

---

# Ab iska actual meaning samjho

## 1. `apps/` vs `services/` vs `ml/`

Ye teen sabse important hain.

### `apps/`

**User kya dekhta hai.**

```text
apps/web
apps/admin
```

Frontend applications.

---

### `services/`

**System ka business logic.**

```text
Auth
Property
Search
Booking
Payment
Review
...
```

Har service ka apna responsibility.

---

### `ml/`

**Intelligence layer.**

```text
Recommendation
Ranking
Personalization
Risk
Review Intelligence
Photo Verification
Explainability
```

Ye Python + FastAPI mein separately run hoga.

---

# 2. Request ka flow

Example: Guest Goa mein property search karta hai.

```text
                USER
                  │
                  ▼
          ┌───────────────┐
          │  apps/web     │
          │   Next.js     │
          └───────┬───────┘
                  │
                  ▼
          ┌───────────────┐
          │ API Gateway   │
          └───────┬───────┘
                  │
                  ▼
          ┌───────────────┐
          │ Search Service│
          └───────┬───────┘
                  │
            Search/filter
                  │
                  ▼
          ┌───────────────┐
          │  ML Service   │
          │   FastAPI     │
          └───────┬───────┘
                  │
       ┌──────────┼───────────┐
       ▼          ▼           ▼
 Recommendation Ranking  Personalization
       │          │           │
       └──────────┼───────────┘
                  ▼
           Ranked Results
                  │
                  ▼
          Search Service
                  │
                  ▼
             API Gateway
                  │
                  ▼
              Next.js
                  │
                  ▼
        Property Cards + Map
```

Ye tumhare roadmap ke end goal se match karta hai: actual guest action → ML service → useful/explainable result. 

---

# 3. `services/` mein modules kyun alag hain?

Tumhare original structure mein:

```text
apps/api/
    modules/
       auth/
       users/
       properties/
       search/
       bookings/
```

Ye **single Node backend ke andar modules** hain.

Agar tum microservices architecture lock kar rahe ho, to better structure hai:

```text
services/
├── auth-service/
├── user-service/
├── property-service/
├── search-service/
├── booking-service/
└── payment-service/
```

Matlab:

> **Module → Service**

Har service independently run/deploy/test ho sakti hai.

---

# 4. API Gateway ka role

Frontend ko ye nahi pata hona chahiye:

```text
auth-service:3001
property-service:3002
booking-service:3003
payment-service:3004
```

Instead:

```text
Next.js
   ↓
API Gateway
   ↓
Correct service
```

Example:

```text
/api/auth/login
      ↓
Auth Service

/api/properties
      ↓
Property Service

/api/search
      ↓
Search Service

/api/bookings
      ↓
Booking Service
```

---

# 5. `packages/database/`

Yahan ek important architecture decision hai.

Tumhare Day 16 design mein 14+ tables, `USER_EVENT`, trust-score field aur photo-hash metadata jaise data requirements hain. 

So:

```text
packages/database/
└── prisma/
    ├── schema.prisma
    ├── migrations/
    └── seed.ts
```

Yahan database schema centrally maintain ho sakta hai.

Example entities:

```text
User
Property
PropertyImage
Booking
Payment
Review
Wishlist
UserEvent
Notification
...
```

Lekin **service ownership clearly define karna zaroori hai**. Shared Prisma schema ko simply har service ke andar arbitrary access dena microservices boundaries ko weak karega.

Isliye Day 15–21 mein ye specifically document karna chahiye ki **kaunsi service kis data ko own/read/write karegi**.

---

# 6. `packages/types/`

Frontend aur backend ko same TypeScript structures chahiye.

Example:

```ts
Property
```

instead of:

```text
web → apna Property type
search → doosra Property type
admin → teesra Property type
```

common:

```text
packages/types/property.ts
```

Then:

```text
web
 ↓
shared Property type

search-service
 ↓
shared Property type

admin
 ↓
shared Property type
```

---

# 7. `packages/api-contracts/`

Ye aur important hai.

Suppose Search Service response:

```json
{
  "properties": [],
  "total": 20
}
```

To API contract define karega ki request/response ka exact format kya hoga.

ML ke liye bhi:

```text
packages/api-contracts/ml/
```

Example conceptual contract:

```text
POST /recommend

Input:
userId
location
budget
guests
filters

Output:
propertyId
score
reasons
```

Day 17 mein REST contracts aur **ML service API contract** explicitly planned hai. 

---

# 8. ML folder ko properly samjho

Tumhare partner ka main workspace:

```text
ml/ml-service/
```

### `models/`

Actual ML models.

```text
models/
├── recommendation/
├── ranking/
├── personalization/
├── risk/
├── review/
└── photo/
```

### `features/`

Raw data ko ML-ready features mein convert karna.

```text
features/
├── user/
├── property/
└── interaction/
```

Example:

```text
User:
age/preferences/history/events

Property:
price/location/amenities/rating

Interaction:
click/save/booking
```

Roadmap mein `USER_EVENT`, booking, property aur review data ko ML/data pipeline ke liye collect karna explicitly planned hai. 

---

### `pipelines/`

End-to-end ML workflow.

```text
Data
 ↓
Cleaning
 ↓
Features
 ↓
Model
 ↓
Prediction
 ↓
Explanation
```

Separate pipelines:

```text
recommendation/
risk/
review/
photo/
```

---

### `explainability/`

ML result ko human-readable banana.

Instead of:

```text
score: 0.87
```

Return:

```text
Why recommended?

• Within your budget
• Matches preferred location
• Strong cleanliness reviews
• Suitable for family stay
```

Roadmap mein explainability specifically Phase 8 ka deliverable hai. 

---

# 9. `infrastructure/`

Code nahi — **system ko run karne wali infrastructure**.

```text
infrastructure/
├── docker/
├── postgres/
├── redis/
├── rabbitmq/
└── storage/
```

### PostgreSQL

Permanent application data.

### Redis

Fast cache / temporary data.

### RabbitMQ

Async service communication.

Example:

```text
Booking Service
      ↓
RabbitMQ
      ↓
Notification Service
```

### Storage

Property images etc.

Tumhare roadmap mein S3-compatible storage explicitly core platform phase mein planned hai. 

---

# 10. `docs/` ko seriously maintain karna

Tumhare project mein documentation sirf README nahi hogi.

```text
docs/
├── research/
├── architecture/
├── api/
├── database/
├── ml/
└── decisions/
```

### `research/`

Day 1–14.

```text
day-01
day-02
...
day-14
```

### `architecture/`

Day 15–21 ka actual output.

```text
system-architecture
service-architecture
ml-architecture
data-flow
communication
```

### `decisions/`

Yahan **why** store hoga.

Example:

```text
ADR-001-architecture.md
```

Content:

> Why Vistara uses microservices?

Another:

```text
ADR-003-ml-service.md
```

> Why ML is a separate FastAPI service?

Ye viva/presentation ke time kaafi useful rahega.

---

# 11. `apps/web/api/` ke baare mein ek correction

Tumhare original structure mein:

```text
apps/web/app/api/
```

tha.

Microservices architecture mein is folder ko **main backend banane ke liye use mat karna**.

Agar required ho to yahan sirf:

* Next.js-specific API routes
* frontend callbacks
* lightweight frontend-specific handlers

rakho.

Actual business APIs:

```text
services/
```

mein rahengi.

---

# 12. `verification-service` ka scope

Iska naam dekhkar future mein confusion ho sakta hai.

Tumhare project ka current scope **ID-upload identity verification nahi hai**. Roadmap explicitly usko out of scope rakhta hai. 

Current verification focus:

```text
Property / Photo Verification
        +
Trust / Risk Signals
        +
Review Intelligence
```

Isliye service ko **property/trust verification workflows** ke liye define karna better hai, not Aadhaar/passport-style identity verification.

---

# 13. Full architecture in one picture

```text
                         VISTARA
                            │
             ┌──────────────┴──────────────┐
             │                             │
        apps/web                       apps/admin
        Next.js                         Next.js
             │                             │
             └──────────────┬──────────────┘
                            │
                            ▼
                    ┌──────────────┐
                    │ API GATEWAY  │
                    └───────┬──────┘
                            │
       ┌────────────────────┼─────────────────────┐
       │                    │                     │
       ▼                    ▼                     ▼
 Auth/User             Property/Search       Booking/Payment
 Services               Services              Services
       │                    │                     │
       └────────────────────┼─────────────────────┘
                            │
                ┌───────────┴───────────┐
                │                       │
                ▼                       ▼
           PostgreSQL               Redis
                │
                │
                ▼
             RabbitMQ
                │
      ┌─────────┼──────────┐
      ▼         ▼          ▼
 Notification  Events    Async Tasks
 Service
                            
                            │
                            ▼
                    ┌───────────────┐
                    │  ML SERVICE   │
                    │    FastAPI    │
                    └───────┬───────┘
                            │
          ┌─────────────────┼─────────────────┐
          ▼                 ▼                 ▼
    Recommendation       Risk/Trust       Review Intelligence
          │                 │                 │
          ▼                 ▼                 ▼
       Ranking        Photo Verification  Personalization
          │                 │                 │
          └─────────────────┼─────────────────┘
                            ▼
                    Explainability
                            │
                            ▼
                    API / Frontend
                            │
                            ▼
                   User sees result
```

---

# 14. Team responsibility bhi clear rahega

Tumhare two-person setup ke according platform aur intelligence separate responsibilities hain, but integration/testing shared hai. 

### Tum — Full Stack

Main focus:

```text
apps/
services/
packages/
infrastructure/
API
Database
Frontend
Authentication
Booking
Payment
Maps
```

### Partner — Data Science / ML

Main focus:

```text
ml/
├── datasets
├── features
├── models
├── pipelines
├── evaluation
└── FastAPI
```

### Both

```text
packages/api-contracts/
docs/
integration
testing
deployment
final demo
```

---

# 15. Abhi kya LOCK karna hai?

Day 15–21 ke architecture/design freeze ke liye **abhi implementation start nahi karna**. Roadmap bhi Day 21 ko design freeze rakhta hai. 

Abhi ye 7 cheezein lock karo:

```text
1. Monorepo structure
        ↓
2. Service boundaries
        ↓
3. Database ownership
        ↓
4. API contracts
        ↓
5. ML API contract
        ↓
6. RabbitMQ / Redis communication
        ↓
7. Frontend ↔ Gateway ↔ Services ↔ ML flow
```

**Mere hisaab se final repo mein `apps/api` ko hata kar `services/` rakhna chahiye**, because tumhara current decision microservices hai. Baaki tumhare diye structure ka content preserve ho sakta hai.

Aur ek important point: **14+ database tables, `USER_EVENT`, trust score, photo-hash metadata, atomic availability, requirement snapshot, Google Maps, aur ML API contract** architecture freeze mein explicitly document hone chahiye, kyunki ye tumhare Day 16–20 design decisions ka part hain. 
