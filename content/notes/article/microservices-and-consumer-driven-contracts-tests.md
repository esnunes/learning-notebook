---
title: Microservices and Consumer-Driven Contracts Tests
date: 2016-03-07T20:48:00-03:00
is: Article
categories:
  - Software Testing
  - Microservices
  - Consumer-Driven Contracts
---

Due to its distributed nature, integration / end-to-end tests in microservices
are hard to do, either by the number of microservices required to cover the test
case or by the time it takes to run them. A good alternative to solve the
problem are the consumer-driven contracts tests.

Consumer-Driven Contracts tests focus on the contract established between two
services but from the point of view of the consumer. Consider the following
scenario: 

The **Profile Service** is responsible to store and provide information about
users of the application like their contact information, addresses, metadata,
avatar, etc and the **E-Mail Service** is responsible to send e-mails based on a
`profile id`. In order to send the e-mail the **E-Mail Service** needs to load
the current data of the profile but not all data, the only information it needs
is the profile name and e-mail address.

In the scenario above the E-Mail Service is a consumer of the Profile Service.
The E-Mail Service expects that the Profile Service is going to send the name
and the e-mail address of the profile in a specific format, there is a contract
established between them. The Profile Service has its unit and service tests to
ensure all profile data is returned based on its internal business logic,
whenever the Profile Service changes the returned data its unit and service
tests will break, e.g. the birth date was a required information and from now on
it is not available anymore on the Profile Service. Even when a change in the
Profile Service breaks its tests doesn't mean that the contracts between the
Profile Service and others are broken, in the scenario above the birth date
wasn't an expected value by the E-Mail Service.

A Consumer-Driven Contract test would check if the Profile Service returns only
the information that the E-Mail Service needs. Back to the example above, if the
Profile Service from now on doesn't return the e-mail address then the
Consumer-Driven Contract test will fail. The failure of the Consumer-Driven
Contract test doesn't mean that the Profile Service implementation is not
correct, it means there is a breaking change between Profile Service and E-Mail
Service.  Based on the failure of the test the E-Mail Service team must be
notified in order to adapt E-Mail Service to the new contract. 

The Consumer-Driven Contract tests should be part of the continuos integration /
deployment pipeline of the producer service. Ideally the tests must be developed
by the team that owns the producer with the help of the team that own the
consumer.

