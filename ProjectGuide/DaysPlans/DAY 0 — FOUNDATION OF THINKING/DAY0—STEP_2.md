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
-----------------------------

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


## Today’s New Small Assignment

We’ll go VERY slowly.

# Task 1

Think about the:

“Booking Workflow”
--------------------------------
from customer perspective.

Write step-by-step:

What happens from:

opening app
to
service completion.

Don’t think technically yet.

Think practically.

# Task 2

Now think:

What can fail at EACH step?

Example:

Step:
“Payment Processing”

Possible failures:

card declined
timeout
duplicate payment
payment success but booking failed

Do this for multiple steps.

# My Answers

Task 1 — Booking Workflow (Customer Perspective)

Let’s think practically.

No code.
No database.
No APIs.

Just real-world flow.

Complete Booking Journey
Step 1 — Customer opens app

Customer wants:

plumber
tutor
cleaner
freelancer
astrologer
etc.

Possible actions:

login/signup
browse homepage
search service
Step 2 — Customer searches for service

Example:

“AC repair”
“Math tutor”
“Logo designer”

Customer expects:

relevant providers
ratings
pricing
availability
location support
Step 3 — Customer views provider profile

Customer checks:

reviews
portfolio
pricing
experience
completed jobs
availability calendar

Now customer decides:
“Can I trust this provider?”

Step 4 — Customer selects service/package

Example:

basic cleaning
premium package
hourly consultation

May include:

add-ons
duration
quantity
Step 5 — Customer selects date & time slot

Example:

tomorrow
7 PM–8 PM

System shows:

available slots only
Step 6 — Customer enters address/details

Example:

home address
issue description
uploaded images
special instructions
Step 7 — Price calculation shown

May include:

base fee
taxes
platform fee
discount coupon
surge pricing

Customer reviews final amount.

Step 8 — Payment step

Customer:

selects payment method
pays online
OR
chooses cash after service
Step 9 — Booking confirmation

Customer expects:

booking ID
provider assigned
confirmation notification
estimated arrival time
Step 10 — Provider accepts/rejects booking

Some platforms:

auto assign
manual accept

Customer waits for final confirmation.

Step 11 — Service in progress

Possible things:

provider traveling
provider started work
live tracking
in-app chat/call
Step 12 — Service completed

Provider marks:

completed

Customer may:

verify completion
share OTP
confirm manually
Step 13 — Final payment settlement

If partial payment:

remaining amount charged

Invoice generated.

Step 14 — Review & rating

Customer leaves:

star rating
feedback
complaint if needed
Task 2 — What Can Fail at Each Step?

THIS is where systems become production-grade.

Step 1 — Opening App

Possible failures:

app/server down
slow loading
login session expired
CDN issue
Step 2 — Searching Services

Possible failures:

no providers shown
wrong search results
search timeout
stale provider data
nearby providers missing
Step 3 — Viewing Provider Profile

Possible failures:

fake reviews
outdated pricing
missing portfolio images
incorrect availability
Step 4 — Selecting Package

Possible failures:

package no longer available
price mismatch
invalid add-on combinations
Step 5 — Selecting Time Slot

MOST CRITICAL AREA.

Possible failures:

slot already booked
stale availability cache
timezone mismatch
provider manually unavailable
double booking
Step 6 — Entering Address/Details

Possible failures:

invalid address
unsupported service area
image upload failure
incomplete details
Step 7 — Price Calculation

Possible failures:

coupon invalid
tax mismatch
surge pricing changed suddenly
different final amount at payment
Step 8 — Payment Processing

Critical failures:

payment timeout
duplicate payment
card declined
UPI failure
payment succeeded but booking failed
webhook delay
refund failed

This is where many startups suffer.

Step 9 — Booking Confirmation

Possible failures:

booking created twice
notification not sent
provider not assigned
booking ID mismatch
Step 10 — Provider Acceptance

Possible failures:

provider ignores request
provider rejects late
multiple providers accept simultaneously
provider app offline
Step 11 — Service In Progress

Possible failures:

provider late
GPS tracking broken
chat system down
provider unreachable
customer unavailable
Step 12 — Service Completion

Possible failures:

provider falsely marks completed
customer disputes work
OTP mismatch
incomplete work
Step 13 — Final Settlement

Possible failures:

payout delayed
wrong commission calculation
duplicate charge
invoice generation failed
Step 14 — Reviews & Ratings

Possible failures:

fake reviews
abusive reviews
review spam
revenge ratings


# Task 3

Think about booking states.
What states should a booking have?

Example:

pending
confirmed

Try designing your own list.

This exercise will train:

backend thinking
workflow design
state modeling

Which is MUCH more important than jumping into Django immediately.

Answer: 

Booking State:

REQUESTED
CONFIRMED
REJECTED
CANCELLED
IN_PROGRESS
COMPLETED

Payment State:

PENDING
SUCCESS
FAILED
REFUNDED

Notice how we separated concerns.


## Tiny Homework Before Day 0 - Step 3

Think about only ONE question:

What exactly is a Booking?

Not technically.

Business-wise.

For example:

Is booking:

just a reservation?
a contract?
a transaction?
an agreement between customer and provider?
something else?

Write your answer in 5–10 lines.


<!-- Answer -->

My answer:

A booking is not just a reservation. It is a mutual agreement between a customer and a provider where both parties commit to a specific service, time, and cost. A booking creates expectations and responsibilities for both sides. The customer agrees to pay for the service, and the provider agrees to deliver the service as promised. It also acts as a transaction record that the platform can use for tracking, payments, cancellations, disputes, and reviews. From a business perspective, a booking is the core contract of trust that connects the customer, provider, and platform. Without a valid booking, there is no clear commitment, accountability, or service relationship between the parties.

This answer shows the thinking I want you to develop:

Booking = Trust + Commitment + Agreement + Transaction Record

Not merely:

"a row in the database"

efore booking:
------------------
Customer and provider are strangers.

After booking:

Customer expects:

service delivery
provider availability
correct pricing

Provider expects:

payment
customer presence
platform protection

Platform expects:

rules followed
commission collected
disputes manageable

A booking creates these obligations.\

Hidden Insight

You accidentally discovered something very important.

A booking is actually:

A Business Contract

Not necessarily a legal contract.

But a business contract.

When booking is created:

The platform now has to enforce rules.

Examples:

Cancellation Policy

Can customer cancel?

If yes:

when?
how much refund?
Provider No-show

What happens if provider doesn't arrive?

Platform must decide:

refund?
compensation?
penalty?
Customer No-show

What happens now?

Provider spent time.

Who absorbs the loss?

Notice:

All these questions originate from:

Booking = Agreement
Why This Matters for Backend Design

Many engineers create tables first.

Great engineers identify:

Invariants

An invariant is a rule that must always remain true.

For example:

Invariant 1

A booking belongs to exactly one customer.

Invariant 2

A booking belongs to exactly one provider.

Invariant 3

A booking must reference a service.

Invariant 4

A booking must have a valid state.

Invariant 5

Two confirmed bookings cannot occupy the same provider slot.

This one becomes very interesting later.

The Core Domain Discovery

Today we discovered something important.

In our platform:

Customer is not the core entity.
Provider is not the core entity.
Payment is not the core entity.

The heart of the system is:

Booking

Everything revolves around it.

Think:

Customer
    ↓
Booking
    ↑
Provider

Then:

Booking
   ↓
Payment

Booking
   ↓
Review

Booking
   ↓
Notification

Booking
   ↓
Dispute

Almost everything connects back to booking.

This is why marketplaces are often called:

Transaction-Centric Systems