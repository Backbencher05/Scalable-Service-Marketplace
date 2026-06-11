DAY 0 — STEP 2

Now we move deeper.

## Understanding Workflows
--------------------------------------------
This is one of the most important backend skills.

Before coding,
engineers must understand:

## “How does the business flow?”
-----------------------------------------


# What is a Workflow?
-----------------------
A workflow is:

sequence of state transitions.

Example:

Customer searches
    ↓
Selects provider
    ↓
Chooses slot
    ↓
Makes payment
    ↓
Booking created
    ↓
Provider notified
    ↓
Provider accepts
    ↓
Service completed
    ↓
Review submitted

This looks simple.

But every arrow contains:

- APIs
- validations
- business rules
- failure cases
- async jobs
- DB transactions

Important Engineering Principle

Senior backend engineers think in:

STATES

not screens.

Example booking states:

- PENDING
- CONFIRMED
- REJECTED
- CANCELLED
- COMPLETED
- REFUNDED

This is called:

State Machine Thinking

VERY IMPORTANT.

-> Why State Machines Matter

Because invalid transitions must NEVER happen.

Example:

Can a booking go:

COMPLETED → PENDING

No.

Can:

CANCELLED → CONFIRMED

Usually no.

Backend must enforce this.

This is business integrity.