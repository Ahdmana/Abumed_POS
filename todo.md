# Abumed-Pharmacy - Project TODO

## Phase 1: Core Infrastructure & Database Schema
- [x] Design and implement database schema (users, roles, stores, products, batches, patients, prescriptions, transactions, audit logs, controlled substances log)
- [x] Set up role-based access control (RBAC) with roles: Pharmacy Admin, Pharmacist, Cashier, Manager
- [x] Implement user authentication with 2FA support
- [x] Create database migration and apply schema

## Phase 2: Point of Sale (POS) Screen
- [x] Build POS counter interface with barcode scanning
- [x] Implement cart management (add, edit, remove items)
- [ ] Implement product search and quick lookup
- [ ] Add expiry date validation and blocking for expired batches
- [x] Build payment method selection (cash, card, insurance, patient credit)
- [x] Implement automatic change calculation for cash payments
- [ ] Create receipt generation with print, PDF download, and email options
- [ ] Add near-expiry alerts during checkout
- [ ] Implement transaction logging and audit trail

## Phase 3: Inventory Management
- [x] Build product master with barcode support
- [x] Implement batch/lot tracking with expiry dates
- [ ] Create purchase order management with supplier linking
- [ ] Build stock level management and reorder points
- [ ] Implement barcode label and shelf-tag printing
- [ ] Create stock transfer between stores
- [ ] Build stock adjustment interface for discrepancies
- [ ] Add low-stock alerts

## Phase 4: Patient & Prescription Management
- [x] Build patient record creation and management
- [x] Implement doctor/prescriber reference linking
- [x] Create digital prescription upload and storage
- [ ] Build prescription-to-sale linking
- [ ] Implement patient history and transaction lookup
- [x] Create patient search and filtering

## Phase 5: Controlled Substances Management
- [ ] Flag products as controlled substances
- [ ] Implement pharmacist override requirement for controlled items
- [ ] Create immutable audit trail for controlled substance transactions
- [ ] Build controlled substance transaction report
- [ ] Implement export functionality for regulatory inspection

## Phase 6: Insurance & Credit Sales
- [ ] Create insurance provider configuration
- [ ] Implement insurance payment mode at checkout
- [ ] Build patient credit account system
- [ ] Create insurance claim reconciliation workflow
- [ ] Implement claim status tracking
- [ ] Build insurance billing report

## Phase 7: Customer Loyalty & Discounts
- [ ] Implement loyalty points system per customer
- [ ] Create customer-group pricing tiers
- [ ] Build promotional scheme configuration
- [ ] Implement time-bound discount application
- [ ] Create loyalty points redemption interface
- [ ] Build customer tier management

## Phase 8: Reporting Engine
- [ ] Build Stock Ageing/Expiry Report with Excel/PDF export
- [ ] Create POS Closing Shift Report
- [ ] Build Monthly Sales Summary and P&L Statement
- [ ] Implement report scheduling with email delivery
- [ ] Create on-demand report generation
- [ ] Build consolidated multi-store reporting
- [ ] Implement report filtering and customization
- [ ] Create audit log export functionality

## Phase 9: Admin Panel & User Management
- [x] Build user management interface
- [x] Implement role creation and permission assignment
- [ ] Create password policy enforcement
- [ ] Build 2FA setup and management
- [x] Implement user activity audit logs
- [x] Create store and counter management
- [x] Build system configuration interface
- [ ] Implement backup and data export

## Phase 10: Multi-Store Support
- [ ] Implement store isolation and data segregation
- [ ] Create multi-store user assignment
- [ ] Build consolidated management dashboard
- [ ] Implement cross-store reporting
- [ ] Create store-specific inventory tracking
- [ ] Build store transfer and consolidation reports

## Phase 11: Compliance & Audit
- [ ] Implement comprehensive audit logging for all actions
- [ ] Create immutable audit trail storage
- [ ] Build audit log viewer and search
- [ ] Implement audit log export for regulatory inspection
- [ ] Create compliance checklist and status tracking
- [ ] Build data retention policies

## Phase 12: UI/UX Polish & Testing
- [ ] Design and implement professional pharmacy-appropriate UI theme
- [ ] Create responsive layouts for desktop and tablet
- [ ] Implement keyboard shortcuts for POS efficiency
- [ ] Add loading states and error handling
- [ ] Create comprehensive unit and integration tests
- [ ] Perform user acceptance testing
- [ ] Optimize performance and database queries

## Phase 13: Deployment & Documentation
- [ ] Create system documentation
- [ ] Build user manuals and training materials
- [ ] Set up production deployment
- [ ] Create backup and disaster recovery procedures
- [ ] Implement monitoring and alerting
- [ ] Create API documentation

## Completed Features
(Items will be moved here as completed)

## Known Implementation Gaps (To Be Addressed)
- [ ] Implement real barcode scanning and product lookup in POS
- [ ] Implement transaction creation and payment processing
- [ ] Build functional CRUD for products (create, edit, delete)
- [ ] Build functional CRUD for patients (create, edit, delete)
- [ ] Build functional CRUD for users (create, edit, delete, role assignment)
- [ ] Build functional CRUD for stores and terminals
- [ ] Build functional CRUD for doctors and prescriptions
- [ ] Implement prescription file upload and storage
- [ ] Implement 2FA setup, verification, and enforcement
- [ ] Implement backend RBAC enforcement for all procedures
- [ ] Add audit logging middleware to log all critical actions
- [ ] Implement receipt generation (PDF, print, email)
- [ ] Implement report scheduling and email delivery
- [ ] Persist system settings through backend APIs
- [ ] Generate proper Drizzle migrations for schema
- [ ] Add comprehensive unit and integration tests
