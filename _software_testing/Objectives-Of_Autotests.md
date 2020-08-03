---
title: Objectives of Autotests
category: [Software_Testing]
---

# Objectives of Autotests

I was watching very interesting presentation [DevTernity 2017: Ian Cooper - TDD, Where Did It All Go Wrong](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwigrvCQ4_fqAhVCqaQKHe0eB2MQwqsBMAB6BAgLEAQ&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DEZ05e7EMOLM&usg=AOvVaw3BD1zy591v6KxTYxlJ_LRq) on youtube.


One statement just caught my attention:

> **Test the Behaviour and not the Implementation!**

We struggle with autotest failures and wonder is this the failure in the autotest's objective itself?
Is the autotest trying to catch something which is not going to impact end user at-all? 
Then why is it trying to catch that?

Can we use following criteria:

> **If this test fails, then as an end user, I will see this particulat change in behaviour.**

There is some test which validates some internal state and it starts failing. Can I make any sense as what behaviour impact this failure has as an end user?

If as an end user, there is no impact on behaviour (including UI, display value), data integrity, am I really supposed to get test failure?
Or does it just expose issue in my testing methodology, test itself, test framework (comparison, wrong assertion)?
