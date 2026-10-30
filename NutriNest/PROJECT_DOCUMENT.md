# NutriNest Project Document

## 1) Executive Summary

NutriNest is a planned nutrition-focused meal subscription and cloud kitchen management platform. The product combines a customer-facing subscription experience with operational tooling for recipe management, rotating menus, order generation, and kitchen execution.

This document defines the initial product and technical plan for incremental implementation. It intentionally separates confirmed decisions from proposed or pending decisions.

## 2) Background and Problem Statement

Customers who want practical daily nutrition often face a trade-off between convenience, affordability, and food quality. At the same time, meal providers face operational complexity in maintaining rotating menus, predictable pricing, and reliable kitchen execution.

NutriNest addresses these dual challenges by:
- Simplifying meal subscription selection for customers.
- Structuring backend operations around recipes, portions, schedules, and daily preparation needs.

## 3) Goals and Measurable Objectives

### Product goals
- Provide a simple subscription experience by meal slot and duration.
- Offer menu variety through controlled recipe rotation.
- Maintain operational consistency for preparation and dispatch.

### Measurable objectives (Proposed)
- Subscription flow completion rate target: To be decided
- Menu publishing lead time target: To be decided
- Order preparation accuracy target: To be decided
- Customer support response SLA: To be decided
- Refund/failed-payment incident threshold: To be decided

## 4) Target Users and User Needs

### A) College students in hostels
- Need affordable, reliable meals.
- Need low-friction subscription choices.

### B) Working professionals away from families
- Need consistent daily meal availability.
- Need ability to manage pauses and renewals.

### C) Gym-goers and health-conscious users
- Need nutrition-aware meal options.
- Need clear estimated nutrition and portion choices.

### D) Operations/admin staff
- Need clear recipe/menu management tools.
- Need practical daily prep and packing summaries.

## 5) Product Principles

1. Prioritize food-service operations and subscriptions.
2. Keep UX simple and practical.
3. Focus on everyday nutritious meals, not extreme diet plans.
4. Maintain rotating menus.
5. Keep pricing understandable and predictable.
6. Build minimal usable scope first.
7. Avoid unsupported micronutrient guarantees.
8. Treat nutrition as estimated unless validated.
9. Favor extensible design without overengineering.
10. Exclude fitness trackers, wearables, and AI meal recommendations in initial release.

## 6) Scope of the Initial Release

### In scope (Initial usable release)
- Customer account creation and login (basic secured auth)
- Profile and address management
- Subscription selection by meal slots, portion category, and duration
- Basic pricing summary based on configuration
- Recipe catalogue and recipe details with estimated nutrition
- Rotating menu publication and upcoming meal visibility
- Admin recipe and menu scheduling essentials
- Initial order creation from active subscriptions
- Basic kitchen prep aggregation (meal counts)

### Out of scope for initial release
- One-time non-subscription ordering
- Advanced reporting and forecasting
- Loyalty/referral systems
- AI-based personalization
- Fitness/workout/calorie-tracking modules

## 7) Explicitly Excluded Features

- Workout tracking
- Wearable integration
- Automatic bodyweight-only portion assignment
- Unverified medical or nutrition claims
- Frontend-only payment success trust model
- Microservices/Kubernetes/event queue infrastructure in v1

## 8) Functional Requirements

### 8.1 Public website
- Home, How It Works, Browse Meals, Recipe Details, Plans/Pricing, About, FAQ, Contact, policy pages.

### 8.2 Customer account
- Registration/login/logout
- Profile updates
- Multiple addresses (Proposed: capped count to be decided)
- Preferences (veg/non-veg, allergens where supported)
- Goal selection: fat loss, muscle gain, maintenance
- Portion selection: S/M/L/XL

### 8.3 Subscription management
- Meal slot combinations (7 combinations)
- Duration selection (exact durations to be decided)
- Pricing summary before confirmation
- Renewal/pause/cancellation according to policy

### 8.4 Recipes and menus
- Recipe creation and update
- Recipe versioning for historical consistency
- Portion variants per recipe version
- Nutrition estimate and allergen metadata
- Date-slot scheduling and menu publishing

### 8.5 Orders and operations
- Generate orders from eligible subscriptions
- Prevent duplicate meal counts from overlapping records
- Basic prep and packing summaries
- Dispatch status tracking (basic)

### 8.6 Payments (later phase)
- Initiate payment transaction
- Verify payment server-side
- Persist payment status transitions
- Handle failure and reconciliation paths

## 9) Non-Functional Requirements

- Security: authenticated endpoints, RBAC, data isolation
- Reliability: deterministic order generation from subscription + schedule inputs
- Maintainability: modular monolith structure
- Scalability: support incremental growth without major rewrite
- Performance: acceptable page/API response times (targets TBD)
- Accessibility: responsive and usable on mobile/desktop
- Auditability: preserve historically relevant order/price/nutrition references

## 10) User Roles and Permissions

### Customer
- Manage own profile, addresses, subscriptions
- View own upcoming meals, orders, and payments
- Submit feedback/support requests

### Administrator
- Manage recipes, ingredients, portion variants, menu schedules
- Manage subscription plans and customer subscriptions (policy constrained)
- Access operational summaries and order statuses

### Super Admin (Proposed)
- Role assignment and sensitive configuration changes
- Advanced operational overrides with audit logging

## 11) Customer User Journeys

### Journey A: New subscription
1. User registers/logs in.
2. Completes profile and address.
3. Selects food preference and goal.
4. Selects meal slots, portion, duration.
5. Reviews pricing summary.
6. Confirms subscription and payment (when enabled).
7. Views upcoming meals in dashboard.

### Journey B: Pause/resume
1. User opens active subscription.
2. Selects pause dates per policy/cutoff rules.
3. System validates eligibility.
4. User confirms.
5. Future eligible orders are adjusted.

### Journey C: Cancellation
1. User requests cancellation.
2. System applies cutoff/refund policy.
3. Subscription status updated.
4. User sees final state and policy outcome.

## 12) Administrator User Journeys

### Journey A: Recipe lifecycle
1. Admin creates ingredient and recipe metadata.
2. Admin defines recipe version and portion variants.
3. Admin sets nutrition estimates and allergens.
4. Admin marks version active for scheduling.

### Journey B: Menu publication
1. Admin selects service dates and meal slots.
2. Assigns recipes to each slot/date.
3. Reviews conflicts/cost constraints.
4. Publishes menu.

### Journey C: Operational oversight
1. Admin views generated meal counts.
2. Reviews prep and packing summaries.
3. Tracks dispatch statuses and exceptions.

## 13) Kitchen Preparation and Dispatch Workflows

### Core daily flow
1. Determine eligible subscriptions for service date and slot.
2. Resolve scheduled recipe by slot/date.
3. Aggregate counts by recipe + portion category.
4. Compute ingredient totals from recipe definitions.
5. Generate prep list and packing sheet.
6. Generate labels with key fields.
7. Mark order states through prep, packed, dispatched.

### Key safeguards
- Avoid duplicate counting caused by overlapping subscriptions/orders.
- Freeze historical references used for produced orders.
- Apply cutoff rules consistently.

## 14) Recipe and Portion Data Requirements

Each recipe should support:
- Basic metadata (name, description, slot suitability, food category)
- Ingredient list references
- Versioned definitions
- Portion variants (S/M/L/XL) with quantity multipliers or explicit quantities
- Estimated nutrition by portion
- Cost estimates by portion
- Allergen and storage notes where applicable

## 15) Nutrition and Allergen Data Considerations

- Nutrition values are estimates unless validated.
- Micronutrients shown only when reliable data source exists.
- Allergen handling is informational and must include disclaimers (wording TBD).
- Versioned nutrition references required for historical order accuracy.

## 16) Subscription and Pricing Business Rules

### Confirmed rules
- Subscription is primary model in initial release.
- Pricing should be predictable.
- Goal and portion are separate selections.

### Proposed/TBD rules
- Available durations (e.g., 1/2/4 weeks) - To be decided
- Pause policy constraints - To be decided
- Cancellation cutoff and refund logic - To be decided
- Tax/fee handling model - To be decided
- Delivery charge policy - To be decided

## 17) High-Level System Architecture

Planned architecture: modular monolith (MERN stack, JavaScript only).

- Frontend React app consumes REST APIs.
- Backend Express API handles auth, validation, business logic.
- MongoDB stores domain entities via Mongoose.
- Shared conventions for error handling and response formatting.

## 18) Proposed Frontend and Backend Responsibilities

### Frontend responsibilities
- Render pages and forms
- Local form validation for UX
- Auth token/session handling strategy (TBD)
- Calling backend APIs and presenting results/errors

### Backend responsibilities
- Source of truth for business logic and authorization
- Input validation and sanitization
- Subscription/order generation rules
- Menu and recipe management logic
- Payment verification and webhook handling

## 19) Candidate Database Entities and Relationships

Candidate entities (initial set, not all required immediately):
- User
- CustomerProfile
- Address
- Ingredient
- Recipe
- RecipeVersion
- PortionVariant
- MenuSchedule
- SubscriptionPlan
- Subscription
- Order
- OrderItem
- Payment
- KitchenPreparationRecord
- Feedback

Proposed relationship highlights:
- User 1..1 CustomerProfile
- User 1..N Address
- Recipe 1..N RecipeVersion
- RecipeVersion 1..N PortionVariant
- MenuSchedule references RecipeVersion by slot/date
- Subscription belongs to User and references plan/selection
- Order derives from Subscription eligibility + MenuSchedule
- OrderItem captures snapshot references for historical integrity

## 20) Proposed API Module Boundaries

- Auth module
- User/Profile/Address module
- Recipe/Ingredient module
- Menu scheduling module
- Subscription module
- Order module
- Payment module
- Kitchen operations module
- Feedback/support module

Each module should expose REST routes with separated controller/service/model concerns where needed.

## 21) Authentication and Authorization Strategy

### Proposed
- JWT-based auth with refresh strategy (exact design TBD)
- Password hashing with modern algorithm
- Role-based access checks enforced server-side
- Ownership checks for customer resources

### Security controls
- Rate limiting for sensitive endpoints (TBD phase)
- Input validation for all write endpoints
- Consistent unauthorized/forbidden responses

## 22) Payment Security Considerations

- Never trust frontend-only success callback
- Verify payment state using gateway server-to-server method/webhook
- Validate signature where gateway provides it
- Store transaction status transitions and reconciliation metadata
- Keep keys/secrets in environment variables only

Gateway provider selection: To be decided.

## 23) Error Handling and Validation Approach

- Centralized error middleware pattern (backend)
- Structured error response format (Proposed standard)
- Request schema validation at API boundary
- User-safe errors for clients; detailed logs for server diagnostics
- Business-rule validation separated from transport validation where practical

## 24) Testing Strategy

### Planned test layers
- Unit tests for pricing, eligibility, aggregation, snapshot selection
- Integration tests for API modules and auth boundaries
- Security tests for authorization and data isolation
- Regression tests for menu and order generation consistency

### Manual QA (initial phases)
- Critical customer flow scripts
- Admin scheduling and kitchen summary checks

Tooling specifics (framework choice) are To be decided in implementation phase.

## 25) Development Phases and Feature Dependencies

### Phase 0 (Current)
- Product and technical documentation

### Phase 1
- Minimal MERN project foundation
- Basic auth shell and environment configuration

### Phase 2
- First customer-facing usable flow
- Depends on Phase 1

### Phase 3
- Recipe catalogue and rotating menus
- Depends on Phase 1, partially on Phase 2 for UI integration

### Phase 4
- Subscription and account workflows
- Depends on Phase 2 and Phase 3 data availability

### Phase 5
- Payment integration
- Depends on stable subscription/order flow

### Phase 6
- Administrative operations expansion
- Depends on recipe/menu/subscription/order base

### Phase 7
- Reliability hardening, testing, deployment prep
- Depends on end-to-end flow completeness

## 26) Deployment Approach

Status: Proposed only.

### Proposed direction
- Separate frontend and backend deployments
- Managed MongoDB deployment
- Environment-based configuration
- Basic CI checks before deployment (TBD)

### To be decided
- Hosting providers
- CI/CD tooling details
- Monitoring and alerting stack

## 27) Known Risks and Unresolved Business Decisions

### Risks
- Incomplete policy definitions may block subscription edge-case behavior.
- Poor historical snapshot strategy may cause reporting inconsistencies.
- Pricing complexity may increase if cost constraints are not formalized early.

### Unresolved decisions
- Exact subscription durations
- Pause/cancellation/refund policy details
- Pricing formula and tax/delivery handling
- Payment gateway selection
- Initial geography/service area constraints
- SLA definitions and support workflow depth

## 28) Acceptance Criteria for Initial Usable Release

Initial usable release is considered acceptable when:
1. A customer can register/login and manage basic profile/address.
2. A customer can choose meal slots, goal, portion, and duration.
3. A customer can view a clear pricing summary before confirmation.
4. Admin can manage recipes/versions/portion variants.
5. Admin can publish a rotating menu by date and slot.
6. System can generate upcoming customer meals from active subscriptions.
7. Basic kitchen aggregation by recipe and portion is available.
8. Authorization prevents cross-customer data access.
9. Critical input validation and error handling are in place.
10. Documentation is updated for setup and workflows at each implemented phase.

---

## Mandatory Language Constraint (Confirmed)

NutriNest implementation must use JavaScript end-to-end for initial development:
- Frontend: React with JavaScript and JSX
- Backend: Node.js + Express.js with JavaScript
- Database access: Mongoose with JavaScript

TypeScript is excluded unless explicitly approved in a future decision.
