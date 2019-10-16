Intro
=====

Introduction to the eBox connector

The eBox connector supports the following processes:

* eBox Registration
* New eBox Document
* Consent Expiration (not available yet)
* Consent Renewal (not available yet)
* Deregistration (not available yet)

During these processes the eBox connector behaves a back-end service. There is no explicit interaction with the user. It will take care of the following tasks:

* Management of the user consent and Oauth tokens
* Storage of eBox document using Doccle
* Single point of interaction for all government api's like:

  * Document provider register
  * FAS login
  * Event API
  * Api's of all document providers

* Audit logging

The usage of the receiver plugin to visualise eBox documents is out of scope of this document.