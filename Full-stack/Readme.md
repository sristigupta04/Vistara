
## Vistara — Monorepo Structure

```text
Vistara/
│
├── apps/
│   │
│   ├── web/                         # Next.js frontend
│   │   ├── app/
│   │   │   ├── (auth)/
│   │   │   │   ├── login/
│   │   │   │   └── register/
│   │   │   │
│   │   │   ├── (guest)/
│   │   │   │   ├── page.tsx         # Home
│   │   │   │   ├── search/
│   │   │   │   ├── properties/
│   │   │   │   ├── wishlist/
│   │   │   │   ├── trips/
│   │   │   │   └── profile/
│   │   │   │
│   │   │   ├── host/
│   │   │   ├── admin/
│   │   │   └── api/
│   │   │
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   ├── navbar/
│   │   │   ├── search/
│   │   │   ├── property/
│   │   │   ├── map/
│   │   │   ├── booking/
│   │   │   └── trust/
│   │   │
│   │   ├── lib/
│   │   ├── hooks/
│   │   ├── types/
│   │   └── public/
│   │
│   ├── api/                         # Node.js + Express backend
│   │   ├── src/
│   │   │   ├── modules/
│   │   │   │   ├── auth/
│   │   │   │   ├── users/
│   │   │   │   ├── properties/
│   │   │   │   ├── search/
│   │   │   │   ├── availability/
│   │   │   │   ├── bookings/
│   │   │   │   ├── payments/
│   │   │   │   ├── cancellations/
│   │   │   │   ├── reviews/
│   │   │   │   ├── wishlist/
│   │   │   │   ├── notifications/
│   │   │   │   └── admin/
│   │   │   │
│   │   │   ├── middleware/
│   │   │   ├── routes/
│   │   │   ├── controllers/
│   │   │   ├── services/
│   │   │   ├── utils/
│   │   │   └── config/
│   │   │
│   │   └── package.json
│   │
│   └── ml-service/                  # Python + FastAPI
│       ├── app/
│       │   ├── api/
│       │   ├── models/
│       │   │   ├── recommendation/
│       │   │   ├── ranking/
│       │   │   ├── risk/
│       │   │   ├── review/
│       │   │   └── photo/
│       │   │
│       │   ├── features/
│       │   ├── pipelines/
│       │   ├── services/
│       │   ├── schemas/
│       │   └── main.py
│       │
│       ├── notebooks/
│       ├── tests/
│       └── requirements.txt
│
├── packages/
│   │
│   ├── database/                    # Prisma + PostgreSQL
│   │   ├── prisma/
│   │   │   ├── schema.prisma
│   │   │   ├── migrations/
│   │   │   └── seed.ts
│   │   └── package.json
│   │
│   ├── types/                       # Shared TypeScript types
│   ├── api-contracts/               # API request/response contracts
│   ├── config/                      # Shared configuration
│   └── ui/                          # Shared UI components if needed
│
├── docs/
│   ├── research/
│   ├── architecture/
│   ├── api/
│   ├── database/
│   ├── ml/
│   └── decisions/
│
├── scripts/
│
├── .env.example
├── .gitignore
├── docker-compose.yml
├── package.json
├── turbo.json
├── README.md
└── LICENSE
```



### Architecture

* **Web** — Next.js, TypeScript and Tailwind CSS
* **API** — Node.js, Express and TypeScript
* **ML Service** — Python, FastAPI and ML models
* **Database** — PostgreSQL with Prisma
* **Storage** — S3-compatible object storage
* **Shared Packages** — Types, API contracts, configuration and UI
* **Documentation** — Research, system architecture, database, API and ML documentation

### Application Modules

The backend is organized into modules for:

* Authentication
* Users & Roles
* Properties
* Search & Filters
* Availability
* Bookings
* Payments
* Cancellations
* Reviews
* Wishlist
* Notifications
* Admin

### ML Modules

The ML service contains:

* Recommendation
* Smart Ranking
* Personalization
* Trust & Risk Analysis
* Review Intelligence
* Photo / Property Verification
* Explainable Recommendations

The platform follows a **modular monolith + separate ML service** architecture.
The Node.js API handles the core marketplace while the FastAPI service provides
ML predictions and intelligence.

```

**Important:** Abhi isko implementation mein split mat karo. Pehle **Day 15–21 architecture/design freeze** ke according structure lock karna better hai. :contentReference[oaicite:1]{index=1}
```
