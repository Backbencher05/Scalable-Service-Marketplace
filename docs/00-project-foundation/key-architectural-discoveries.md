# Key Architectural Discoveries

## Marketplace Nature

Marketplace = Trust + Coordination System

The platform exists to coordinate service transactions between customers and providers while establishing trust.

---

## Core Business Entity

Booking is the Core Business Entity.

Without bookings:

* No revenue
* No payments
* No reviews
* No disputes
* No marketplace

---

## Marketplace Invariants

### Time Integrity

One provider cannot be double-booked for the same time slot.

### Financial Integrity

Money cannot be lost, duplicated, or refunded incorrectly.

### Historical Integrity

Past events must remain auditable and immutable.

---

## Domain Classification

### Foundational Domain

Identity & Account Domain

### Core Domain

Booking & Scheduling Domain

### Supporting Domains

* Service Marketplace
* Payments & Financial
* Trust & Reputation
* Communication

### Generic Domains

* Support & Resolution
* Platform Operations

---

## Architectural Mindset Shift

From:

API → Serializer → Model → Database

To:

Business Goal
↓
Domain
↓
Commands
↓
Events
↓
Policies
↓
State Changes
↓
Implementation

---

## Booking Architecture Decision

Selected Approach:

Temporary Booking
↓
Reserve Slot
↓
Payment Window
↓
Payment Success
↓
Booking Confirmed

OR

Payment Timeout
↓
Booking Expired
↓
Release Slot

Reason:

* Prevents double booking
* Improves customer experience
* Reduces refund complexity
* Protects providers
