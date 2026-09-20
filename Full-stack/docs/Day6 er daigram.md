                                  ┌─────────────────┐
                                  │      USER       │
                                  ├─────────────────┤
                                  │ PK user_id      │
                                  │ name            │
                                  │ email           │
                                  │ password_hash   │
                                  │ role            │
                                  │ phone           │
                                  │ created_at      │
                                  └────────┬────────┘
                                           │
                 ┌─────────────────────────┼─────────────────────────┐
                 │                         │                         │
                 │                         │                         │
                 ▼                         ▼                         ▼
        ┌─────────────────┐      ┌─────────────────┐       ┌─────────────────┐
        │   HOST_PROFILE  │      │  GUEST_PROFILE  │       │    WISHLIST     │
        ├─────────────────┤      ├─────────────────┤       ├─────────────────┤
        │ PK host_id      │      │ PK guest_id     │       │ PK wishlist_id  │
        │ FK user_id      │      │ FK user_id      │       │ FK user_id      │
        │ host_status     │      │ preferences     │       └────────┬────────┘
        └────────┬────────┘      └─────────────────┘                │
                 │                                                  │
                 │ 1:N                                              │ N:M
                 ▼                                                  ▼
        ┌─────────────────┐                                ┌─────────────────┐
        │    PROPERTY     │◄───────────────────────────────│ WISHLIST_ITEM   │
        ├─────────────────┤                                ├─────────────────┤
        │ PK property_id  │                                │ PK item_id      │
        │ FK host_id      │                                │ FK wishlist_id  │
        │ title           │                                │ FK property_id  │
        │ description     │                                └─────────────────┘
        │ property_type   │
        │ address         │
        │ location        │
        │ price           │
        │ capacity        │
        │ status          │
        └────────┬────────┘
                 │
        ┌────────┼─────────────────────┐
        │        │                     │
        ▼        ▼                     ▼
┌────────────┐ ┌──────────────┐ ┌──────────────────┐
│ PROPERTY   │ │ AVAILABILITY │ │ PROPERTY_IMAGE   │
│ AMENITY    │ │              │ │                  │
├────────────┤ ├──────────────┤ ├──────────────────┤
│ PK id      │ │ PK id        │ │ PK image_id      │
│ FK property│ │ FK property  │ │ FK property_id   │
│ FK amenity │ │ date         │ │ image_url        │
└────────────┘ │ status       │ │ is_primary       │
               └──────────────┘ └──────────────────┘
                 │
                 │
                 ▼
        ┌─────────────────┐
        │     BOOKING     │
        ├─────────────────┤
        │ PK booking_id   │
        │ FK guest_id     │
        │ FK property_id  │
        │ check_in        │
        │ check_out       │
        │ guests          │
        │ total_amount    │
        │ status          │
        └───────┬─────────┘
                │
          ┌─────┴──────────────
          │                     
          ▼                     
 HOST_PROFILE
     │
     └── 1:N ── HOST_REQUIREMENT
                       │
                       ▼
                   BOOKING
                       │
                       ├── 1:1 ── REQUIREMENT_CONFIRMATION
                       │
                       ├── 1:1 ── PAYMENT
                       │
                       ├── 1:1 ── REVIEW
                       │
                       └── 1:N ── ISSUE_REPORT
                                      │
                                      ▼
                                RISK_ASSESSMENT
│     PAYMENT     │    │     REVIEW      │
├─────────────────┤    ├─────────────────┤
│ PK payment_id   │    │ PK review_id    │
│ FK booking_id   │    │ FK booking_id   │
│ FK user_id      │    │ FK user_id      │
│ amount          │    │ FK property_id  │
│ status          │    │ rating          │
│ transaction_id  │    │ comment         │
│ paid_at         │    │ created_at      │
└─────────────────┘    └─────────────────┘


                 ╔══════════════════════════════════════╗
                 ║        VISTARA TRUST LAYER           ║
                 ╚══════════════════════════════════════╝

        ┌─────────────────┐
        │   VERIFICATION  │
        ├─────────────────┤
        │ PK verification │
        │ FK user_id      │
        │ FK property_id  │
        │ type            │
        │ status          │
        │ submitted_at    │
        │ verified_at     │
        └────────┬────────┘
                 │
        ┌────────┼──────────────────────┐
        │        │                      │
        ▼        ▼                      ▼
┌────────────┐ ┌──────────────┐ ┌──────────────────┐
│ IDENTITY   │ │  BUSINESS    │ │ CERTIFICATE /    │
│ CHECK      │ │  CHECK       │ │ DOCUMENT CHECK   │
├────────────┤ ├──────────────┤ ├──────────────────┤
│ FK verify  │ │ FK verify    │ │ FK verify        │
│ identity   │ │ company_name │ │ document_url     │
│ status     │ │ registration │ │ certificate_no   │
│ result     │ │ status       │ │ issuer           │
└────────────┘ └──────────────┘ │ expiry_date      │
                                │ status            │
                                └──────────────────┘
                                         │
                                         ▼
                                ┌─────────────────┐
                                │   RISK ASSESSMENT│
                                ├─────────────────┤
                                │ PK risk_id      │
                                │ FK user_id      │
                                │ FK property_id  │
                                │ risk_level      │
                                │ risk_score      │
                                │ reason          │
                                │ created_at      │
                                └────────┬────────┘
                                         │
                                         ▼
                                ┌─────────────────┐
                                │     REPORT      │
                                ├─────────────────┤
                                │ PK report_id    │
                                │ FK reporter_id  │
                                │ FK user_id      │
                                │ FK property_id  │
                                │ reason          │
                                │ status          │
                                │ created_at      │
                                └─────────────────┘


                    ╔══════════════════════════════╗
                    ║          AI LAYER            ║
                    ╚══════════════════════════════╝

        ┌─────────────────────┐
        │    AI_CONVERSATION   │
        ├─────────────────────┤
        │ PK conversation_id  │
        │ FK user_id          │
        │ type                │
        │ created_at          │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │    AI_MESSAGE       │
        ├─────────────────────┤
        │ PK message_id       │
        │ FK conversation_id  │
        │ role                │
        │ content             │
        │ created_at          │
        └─────────────────────┘


        ╔══════════════════════════════╗
        ║     REGULATORY LAYER         ║
        ╚══════════════════════════════╝

        ┌─────────────────────┐
        │     REGULATION      │
        ├─────────────────────┤
        │ PK regulation_id   │
        │ location            │
        │ requirement        │
        │ permit_required    │
        │ tax_requirement    │
        │ source             │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │ PROPERTY_COMPLIANCE │
        ├─────────────────────┤
        │ PK compliance_id   │
        │ FK property_id     │
        │ FK regulation_id   │
        │ status             │
        │ checked_at         │
        └─────────────────────┘