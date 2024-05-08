---
tags: [Getting Started, Underwriting, Risk, Application]
---

# Using our APIs

Exchange uses RESTful APIs to allow requests to be sent to our services, allowing onboarding, reporting, funding and more. These are constructed using a Header and request Body.

---

### Unlocking an Application

After an application is submit, it will move to underwriting. If there are every cases where a Credit Risk Error or AML error is recieved due to invalid data, an application can be unlocked in order to be updated and resubmit using the unlock application endpoint

```json
{
  "operation": {
    "operation_type": "APPLICATION_UNLOCK"
  },
  "application": {
    "application_external_id": "APL01-75CDF-663EB-79CBA-DF321-BEUIP-KL123"
  }
}
```


