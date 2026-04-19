# Product Requirements Document (PRD)

# Revotek Solar Planner

## 1. Overview

Revotek Solar Planner is a lead-generation and pre-sales web application for Revotek, a solar installation company operating in Castilla y León, with initial focus on Salamanca, Ávila, Zamora, and Valladolid.

The product allows homeowners to upload one or more electricity bills, provide details about their home and energy usage profile, and receive a personalized pre-assessment including:

- annualized electricity cost estimate
- annualized electricity consumption estimate
- recommended solar installation sizing
- recommended inverter and optional battery
- expected annual production based on location, orientation, slope, and climate
- estimated savings
- break-even estimate
- tax deduction guidance
- financing comparison
- next-step conversion actions (call, email, WhatsApp, online reservation / contracting)

The same platform must include an admin panel where Revotek can manage the product catalog, pricing, labor cost, commercial rules, and lead workflow.

---

## 2. Product Goal

Build a conversion-oriented solar estimation platform that transforms cold inbound traffic into qualified sales opportunities and, where possible, enables direct online progression to reservation or contracting.

---

## 3. Business Goals

1. Generate qualified leads from organic and paid traffic.
2. Increase conversion rate versus static contact forms.
3. Reduce time spent by Revotek sales staff on low-quality inbound requests.
4. Standardize preliminary proposals and make them consistent.
5. Allow Revotek to update products, pricing, and installation logic without developer intervention.
6. Support local SEO expansion in target provinces.

---

## 4. Primary Users

### 4.1 End Customers
Homeowners or property owners who want to assess whether solar panels make sense for their home.

Typical characteristics:
- residential single-family homes first
- interested in savings, self-consumption, financing, and tax deductions
- limited technical knowledge
- want fast and credible answers

### 4.2 Revotek Internal Users
- sales staff
- technical pre-sales staff
- operations / admin users
- marketing / content managers

They need to:
- manage product catalog
- update prices and labor assumptions
- review leads
- decide follow-up actions
- configure conversion logic

---

## 5. Product Scope

## 5.1 Public Experience

The public-facing app must include:
- SEO landing pages by location and intent
- a solar savings calculator flow
- bill upload
- guided property and usage questionnaire
- personalized results page
- conversion actions

## 5.2 Admin Experience

The admin portal must include:
- product catalog management
- pricing rule management
- installation rule configuration
- financing option management
- tax guidance content management
- lead management and action tracking
- scheduling / calendar configuration

---

## 6. Key User Stories

### 6.1 Bill Analysis
As a homeowner, I want to upload my electricity bill so that the platform can estimate my current consumption and annual electricity cost.

### 6.2 Solar Recommendation
As a homeowner, I want the platform to recommend how many panels, what inverter, and whether I should consider a battery so that I understand what setup is appropriate for my home.

### 6.3 Savings Projection
As a homeowner, I want to see my expected annual production, annual savings, and payback so that I can decide whether the investment makes sense.

### 6.4 Tax and Financing
As a homeowner, I want to understand possible tax deduction ranges and financing options so that I can assess affordability.

### 6.5 Lead Activation
As a homeowner, I want to take the next step immediately by booking a call, receiving a proposal by email, contacting Revotek via WhatsApp, or contracting directly online if eligible.

### 6.6 Admin Control
As a Revotek admin, I want to control products, prices, and proposal logic so that the estimator reflects the real catalog and margin structure.

---

## 7. Functional Requirements

## 7.1 Landing & SEO
The platform must support:
- generic home page
- province/city pages
- intent pages (price, tax deduction, battery, aerotermia, pool, etc.)
- structured metadata for SEO
- clear CTA to the calculator

Examples:
- `/placas-solares-salamanca`
- `/placas-solares-avila`
- `/placas-solares-zamora`
- `/placas-solares-valladolid`
- `/financiacion-placas-solares-salamanca`
- `/deduccion-renta-placas-solares`

## 7.2 Calculator Intake
The calculator flow must collect:
- lead contact info (name, email, phone)
- property location
- property type
- approximate roof orientation
- approximate roof slope
- whether there are significant shadows
- approximate home size / usable area
- major loads (aerothermal, pool, AC, EV, etc.)
- whether the user wants battery guidance
- electricity bill file upload

## 7.3 Bill Upload and Parsing
The system must support:
- PDF upload
- image upload optional later
- extraction of bill date / billing period
- extraction of contracted power
- extraction of energy price per kWh when available
- extraction of fixed power term when available
- extraction of total consumption in the period
- extraction of invoice total if available

The system must support confidence tagging:
- high confidence
- medium confidence
- low confidence

If parsing confidence is low, the system must allow fallback to manual confirmation.

## 7.4 Annualization Logic
The system must estimate annual consumption and cost based on:
- one or more uploaded bills
- bill dates / seasonality
- declared energy profile (aerothermal, pool, AC, etc.)
- confidence score

The system should distinguish:
- full-year data
- partial-year estimate
- low-confidence estimate

## 7.5 Solar Sizing
The system must recommend:
- PV system size (kWp)
- number of panels
- inverter model
- battery recommendation (yes/no + proposed model)

The recommendation must consider:
- annual estimated demand
- roof usability / rough space
- orientation and slope
- expected production per kWp
- major loads
- day/night usage assumptions
- catalog constraints

## 7.6 Production Estimate
The system must estimate annual production based on:
- property location
- orientation
- slope / tilt
- selected panel count / kWp
- climatic dataset

The system should support 3 scenarios:
- conservative
- expected
- optimistic

## 7.7 Savings Engine
The system must calculate:
- direct self-consumption estimate
- optional battery contribution estimate
- grid residual consumption estimate
- export / excess estimate
- estimated annual savings
- average monthly savings
- break-even estimate

Savings logic must respect simplified compensation assumptions and avoid overstating export value.

## 7.8 Tax Guidance
The system must display tax deduction guidance in a non-advisory format.

It must support:
- 20% scenario content
- 40% scenario content
- 60% scenario content
- rules managed from admin or content configuration
- disclaimers about certificates and tax eligibility

## 7.9 Financing Comparison
The system must support multiple financing options:
- cash payment
- partner financing option A
- partner financing option B
- optional early repayment scenario using tax refund

Each financing option must show:
- monthly payment
- total financed cost
- total estimated savings impact
- illustrative break-even effect

## 7.10 Proposal Output
The system must generate a proposal summary with:
- current energy situation
- recommended system
- estimated production
- savings projection
- financing options
- tax guidance summary
- disclaimer section

The result must be viewable on screen and exportable as PDF.

## 7.11 Lead Action / Conversion
After results are shown, the platform must allow the user to:
- book a call
- request proposal by email
- open WhatsApp with prefilled context
- proceed to online reservation / contracting when eligible

The available CTA set must be configurable based on:
- lead type
- geography
- technical complexity
- confidence level
- product / bundle eligibility

## 7.12 Admin Panel
The admin panel must support:
- product CRUD
- price CRUD
- labor cost configuration
- province-specific configuration
- financing option configuration
- tax content management
- lead management
- scheduling settings
- conversion rule settings

---

## 8. Non-Functional Requirements

- Mobile-first public experience
- Fast first paint and SEO-friendly rendering
- GDPR-compliant consent handling
- Secure storage of uploaded bills
- Auditable calculation outputs
- Clear disclaimer strategy
- Low-friction admin UX
- Extensible rules engine

---

## 9. MVP Definition

The MVP must include:
- SEO landing pages
- calculator flow
- PDF bill upload
- bill parser v1
- annualization engine v1
- solar sizing engine v1
- production estimate engine v1
- savings engine v1
- tax guidance content
- financing comparison v1
- results page
- lead capture and action CTAs
- admin panel for catalog / pricing / leads
- proposal PDF generation

The MVP does not need to include:
- perfect bill parsing for every provider
- industrial / commercial flows
- advanced engineering validation
- fully automated online contracting for all cases
- deep CRM / ERP integrations

---

## 10. Online Contracting Strategy

### V1
Support:
- call booking
- email proposal delivery
- WhatsApp contact
- optional reservation / deposit flow

### Later phase
Support direct online contracting only for eligible cases.

Eligibility examples:
- residential detached home
- standard roof case
- acceptable data confidence
- compatible predefined bundle
- province supported by Revotek

---

## 11. Success Metrics

### Acquisition
- organic sessions by target province
- calculator start rate
- bill upload rate

### Funnel
- completion rate
- lead submission rate
- booked call rate
- WhatsApp initiation rate
- proposal delivery rate
- online reservation rate

### Sales
- lead to visit rate
- visit to proposal rate
- proposal to sale rate
- average deal value
- average time to close

### Accuracy / Ops
- parser confidence distribution
- estimate vs final project deviation
- admin usage of pricing / catalog tools

---

## 12. Risks

1. Overpromising savings.
2. Poor bill parsing accuracy.
3. Weak trust if estimates feel generic.
4. Legal / compliance issues if fiscal claims are too assertive.
5. Admin complexity if rules become too bespoke too early.

Mitigation:
- use scenarios and confidence labels
- keep disclaimers visible
- implement fallback manual validation
- separate deterministic logic from explanatory text

---

## 13. Suggested Rollout Plan

### Phase 1
- core estimator
- lead capture
- admin catalog
- PDF proposal
- local SEO pages

### Phase 2
- better bill parser coverage
- better battery logic
- scheduling
- WhatsApp deepening
- reservation flow

### Phase 3
- selective online contracting
- CRM integration
- advanced analytics
- expansion to more provinces

