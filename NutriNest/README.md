# NutriNest

NutriNest is a planned full-stack web application for managing a nutrition-focused meal subscription business and its cloud kitchen operations.

## Development Status

**Current Stage:** Documentation-only (Phase 0)

**Implemented Today:**
- Project documentation

**Not Implemented Yet:**
- Frontend application
- Backend APIs
- Database models
- Authentication and authorization
- Subscription workflows
- Admin workflows
- Kitchen operations engine
- Payments
- Automated tests
- Deployment configuration

---

## Problem Statement

Many students, working professionals, and health-conscious individuals struggle to access convenient daily meals that are nutritious, reasonably priced, and operationally reliable. Existing options often fail in one or more of the following ways:
- Meals are either unhealthy or difficult to sustain long-term.
- Nutrition-focused options are expensive or too rigid.
- Subscription experiences are confusing.
- Businesses struggle to run predictable kitchen operations with rotating menus.

NutriNest aims to solve both customer convenience and backend food-service execution.

## Proposed Solution

NutriNest will provide:
- A customer-facing website to discover meals and subscribe by meal slot (breakfast/lunch/dinner), portion size, and duration.
- A backend system to manage recipes, recipe versions, portion variants, menu scheduling, subscriptions, and orders.
- Administrative operations for meal planning, kitchen preparation summaries, packing workflows, and dispatch tracking.

Nutrition data will be presented as **estimated values** unless laboratory validation is available.

## Target Users

- College students living in hostels
- Working professionals living away from family
- Gym-goers seeking balanced meals
- People focused on fat loss, muscle gain, or maintenance
- Users who want healthier food without cooking daily

## Core Product Features (Planned)

### Customer-facing
- Meal subscription by slot combinations:
  - Breakfast
  - Lunch
  - Dinner
  - Breakfast + Lunch
  - Breakfast + Dinner
  - Lunch + Dinner
  - Breakfast + Lunch + Dinner
- Goal selection:
  - Fat Loss
  - Muscle Gain
  - Maintenance
- Portion category selection:
  - S, M, L, XL
- Rotating menu browsing and recipe details
- Subscription management (renew, pause, cancel per policy)
- Order and payment history

### Administrative
- Recipe and ingredient management
- Recipe versioning and portion variants
- Nutrition, allergen, and storage metadata
- Menu scheduling and publishing
- Subscription and order management
- Kitchen prep planning and packing support
- Dispatch status tracking
- Basic reporting

## Customer Workflow (Planned)

1. Visitor explores public pages (home, meals, plans, FAQ, policies).
2. User registers and logs in.
3. User configures profile, address, preferences, goal, and portion.
4. User selects meal slots and subscription duration.
5. System computes pricing summary based on selected configuration.
6. User confirms subscription and payment (once payment integration exists).
7. User views upcoming scheduled meals and order history in dashboard.
8. User can pause/renew/cancel according to business rules.

## Administrative and Kitchen Workflows (Planned)

### Administration
1. Admin creates/updates ingredients and recipes.
2. Admin maintains recipe versions and portion variants.
3. Admin schedules recipes to meal slots and dates.
4. Admin publishes upcoming menu.
5. Admin monitors subscriptions, orders, and payment statuses.

### Kitchen operations
1. Identify active eligible subscriptions for a service date.
2. Map eligible meal slots to published menu recipes.
3. Aggregate required meal counts by recipe and portion category.
4. Derive ingredient quantity requirements from recipe definitions.
5. Generate preparation and packing sheets.
6. Generate labels with recipe, portion, allergens, nutrition estimate, and date.
7. Track prep -> packed -> dispatched statuses.

## Proposed Technology Stack

### Frontend
- React (JavaScript + JSX)
- React Router
- Tailwind CSS
- JavaScript form validation approach (to be decided)

### Backend
- Node.js (JavaScript)
- Express.js
- REST APIs
- MongoDB + Mongoose

### Supporting tools
- Git + GitHub
- VS Code + GitHub Copilot
- Postman
- Cloudinary or equivalent for media (when required)
- Indian payment gateway (to be decided, when payments are implemented)
- Transactional email provider (to be decided)

## High-Level Architecture Overview (Planned)

NutriNest is planned as a modular monolith:
- Frontend web client consumes backend REST APIs.
- Backend organizes logic into routes, controllers, services, models, and validation.
- MongoDB stores users, profiles, recipes, menus, subscriptions, orders, and operational records.
- Role-based access control protects admin capabilities.
- Historical order/price/nutrition snapshots preserve data accuracy over time.

## Planned Project Roadmap

### Phase 0: Product and technical documentation
- Product definition
- Scope and architecture planning
- Security and testing strategy

### Phase 1: Foundation
- Minimal project setup for frontend and backend
- Basic configuration and environment strategy

### Phase 2: First usable customer experience
- Initial public pages and first subscription flow slice

### Phase 3: Recipes and rotating menus
- Recipe catalogue, portion variants, menu scheduling/publishing

### Phase 4: Customer accounts and subscriptions
- Profiles, slot selection, subscriptions, order generation

### Phase 5: Payments
- Payment gateway integration with server-side verification

### Phase 6: Administrative operations
- Admin recipes/menus/subscriptions/orders and kitchen prep workflows

### Phase 7: Testing and deployment
- Workflow hardening, testing, deployment preparation

## Security and Privacy Considerations (Planned)

- Server-side authentication and role-based authorization
- Strict access control for customer data isolation
- Request payload validation and error handling consistency
- Secret management via environment variables only
- No credential or API key commits
- Payment verification via trusted server-side flow/webhooks
- Auditability for key business events where appropriate

## Planned Testing Strategy

- Unit tests for business logic (pricing, subscription eligibility, aggregation)
- Integration tests for API modules and critical workflows
- Security-focused tests for authorization boundaries
- Regression checks for menu/snapshot consistency
- Manual QA scripts for customer and admin critical paths

Status: Detailed test suite not implemented yet.

## Future Enhancements (Post-initial release)

- One-time orders in addition to subscriptions
- Enhanced analytics and business intelligence reports
- Smarter operations planning tools
- Richer customer communication and notification automation

The following are intentionally out of initial scope unless explicitly approved:
- Calorie/workout/wearables tracking
- AI meal recommendation engine
- Microservices migration

## Screenshots (To Be Added)

- Home page
- Meal browsing
- Subscription checkout
- Customer dashboard
- Admin recipe management
- Kitchen preparation sheet

## Setup Instructions (Pending Implementation)

Implementation repositories and runnable apps are not created yet. Setup instructions will be added once foundational code exists.

Planned future setup sections:
- Prerequisites
- Environment variables
- Frontend local run steps
- Backend local run steps
- Database setup
- Test execution

## License and Acknowledgements

- License: To be decided
- Acknowledgements: Not applicable at current stage
