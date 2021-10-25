---
title: Objectives of Autotests
category: [Software_Testing]
---

# Objectives of Autotests

I was watching very interesting presentation [DevTernity 2017: Ian Cooper - TDD, Where Did It All Go Wrong (YouTube)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwigrvCQ4_fqAhVCqaQKHe0eB2MQwqsBMAB6BAgLEAQ&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DEZ05e7EMOLM&usg=AOvVaw3BD1zy591v6KxTYxlJ_LRq).


One statement just caught my attention:

> **Test the Behaviour and not the Implementation!**

Use cases of autotest failures where behaviour for end-user is not changed, but some internal state has changed and validation needs to be modified accordingly point to above statement.

We normally try to capture internal state as developers as we tend to validate all the internal states coded for. Now due to some coding/ setup changes, these internal states may change and we need to modify validations.

Can we use following criteria:

> **If this test fails, then as an end user, I will see this particular change in behaviour.**

There is some test which validates some internal state and it starts failing. Can I make any sense as what behaviour impact this failure has as an end user?

If as an end user, there is no impact on behaviour (including UI, display value), data integrity, am I really supposed to get test failure?
Or does it just expose issue in my testing methodology, test itself, test framework (comparison, wrong assertion)?
