---
title: DNS Setup Notes
---

## What I learned about Subdomain Setup

You should not have 2 Route53 public zones with intermediary paths that would classify one as a sub-child of the other.

Given the root domain [subdomain.dominicklee.net](http://subdomain.dominicklee.net/) and two AWS accounts that have created the public zones:

* [service.subdomain.dominicklee.net](http://service.subdomain.dominicklee.net/) (Account 1)
* [us-east-1.prod.service.subdomain.dominicklee.net](http://us-east-1.prod.service.subdomain.dominicklee.net/) (Account 2)

^ This will cause an outage if you delegate nameservers from the parent. In this case, Account 2 should have its NS delegated from Account 1 instead of the Root domain.

Another example:

* [us-east-1.beta.service.subdomain.dominicklee.net](http://us-east-1.beta.service.subdomain.dominicklee.net/) (Account 1)
* [us-east-1.prod.service.subdomain.dominicklee.net](http://us-east-1.prod.service.subdomain.dominicklee.net/) (Account 2)

^ In this case, there is no issue, because there is no intermediary zone in the path that breaks the DNS delegation, and both records can be delegated from the Root domain.
