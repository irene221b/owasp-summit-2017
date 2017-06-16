---
layout       : blocks/working-session
title        : Threat Modeling by Feature and Layer
type         : workshop
track        : Threat Model
technology   :
related-to   :
status       : draft
when-day     : Thu
when-time    : AM-1
location     : Room-6
organizers   :
participants :
---

...intro text...

## Why

...why text...

## What

...what text...

## Outcomes

### Synopsis/Takeaways

#### Address Lookup (external entity)

**Threats**

- (S) Fake address lookup service
    - possibly through DNS poisoning
    - goals might be either to siphon private data of JuiceShop customers or return bogus addresses
 - Mitigation: TLS with mutual authentication
    
- (S) Fake JuiceShop - someone else (possibly including the address lookup service itself) sending requests on behalf of the JuiceShop
- (R) Malicious data in these requests - can JuiceShop be liable if addressing service incures damage
    
- (D) If service is rate-limited, the threat above will lead to DoS.

- (S) Customer enters fake address, leading to "craiglist" attack

- Address lookup is malicious, leading to:

- (T) Trucks being sent to fake address
- (T) Bad data sent back, violating assumed response format, leading to range of problems with JuiceShop depending how vulnerable the JuiceShop parser is (from DoS to RCE)

- (D) Customers or maybe fake JuiceShop requests include bad addresses (bad as in associated with drug trade, terrorists etc), hoping to trigger alerts in some security analytics, leading to DoS by government.

- (I) Eavesdropping on communication will break privacy regulations, GDPR etc.
    Mitigation: TLS.

- (D) If the service is synchronous and unavailable or slow, would it result in DoS in JuiceShop?

- (I) If JuiceShop authenticates with keys, how secure is key storage.


**Assumptions**

- Address resolution service is paid (or at least rate-limited, with Juice shop having a specific quota)
- The API sends (name, address), gets back either:
  - address if it was correct
  - list of potential addresses if the resolution was a bit fuzzy
  - nothing if failed to resolve
- No outbound rate limit, so a fuzzy request can result in a large list of matches


#### Delivery Service (External)

**Threats**

- Fake delivery services
- Tampering of quantity
- Reproduction of confirmation response
- Reversal of data direction

**Assumptions**

- TLS is used
- Threat models exist for TLS
- Paid Service
- A Quote-flow is generated

#### Juice Shop User (External)

**Threats**

- Weak user authentication allows the user to be spoofed easily (spoofing, EoP)
- No Audit trail for user activity exists (repudiation)
- Weak account management security allows account takeover, e.g. lack of email confirmation (spoofing, EoP)
- Admin console available due to lack of authentication (EoP)
- Admin console security relies on obfuscation (information disclosure)
- POST-SESSION: User is able to input malicious data (EoP)

**Assumptions**

- TLS is used
- Threat models exist for TLS
- User is authenticated

#### Email Service (External)

**Threats**

- Service is misused
- Juice Shop sends malicious emails
- Connected to the correct service
- BCC abused
- HTML body injection
- Header injection
- Juice Shop sending spam
- Email message tampering
- Sent confirmation
- Sensitive data sent in emails
- Tracking mechanism (privacy)

**Assumptions**

- Rest API
- TLS is used
- Threat models exist for TLS
- Delivery confirmation
- Validated reputation



#### Invoice Tracking (Internal)

**Threats**

- Unauthorised access to the invoice service
- Page is obfuscated
- Discouragement of business sensitive data (Prices, Quantities)
- Discouragement of user sensitive data
- Audit trail of the invoice
- Manipulation of invoice data
- Logging of read access
- Screen scraping

**Assumptions**

- Page is within the application
- User is authenticated
- Used only for delivery services
- Not built for user invoicing

#### Takeaways

- Went through the user story handling the address lookup delivery service
- Threats were identified for the service that threat model templates need to be created for: TLS, e-mail etc.
- The discussion did not resolve the level of threat we should be looking at

![Whiteboard picture](https://raw.githubusercontent.com/OWASP/owasp-summit-2017/master/Working-Sessions/Threat-Model/whiteboard-photos/By-Feature-and-Layer.jpg)

## Who

... target audience ...

---

## Working materials

Here are the current 'work in progress' materials for this session

(please add as much information as possible before the sessions)

### Content

...add content...
