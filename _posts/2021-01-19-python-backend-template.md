---
layout: post
title: Building a Framework-Independent Python Backend
categories: Backend
excerpt: My template for building a modern Python backend service that's not tied to a specific framework.
---
I've been working on Python backends for a number of companies and projects now, along with a number of libraries and frameworks. Lately I've started to feel that it is better to not be overly dependent on a framework in the first place, especially as I"ve started building gRPC-serving microservices. This sentiment is driven by two trends in backend development: the move toward API-driven single-page-apps, and microservice architectures.

Django has been a popular and convenient framework on the Python side, but in my experience it itself is bloated and monolithic and contains a lot of things that are outdated for modern API-centric backends (e.g. forms). It bundles a lot of things like an ORM and templating language, but none of these are even the best available libraries at what they do. More importantly, relying too much on Django patterns, features and plug-ins actually impede long term scaling and makes it harder to eventually refactor a monolith into microservices.

Flask is a much smaller "micro framework" which, comparatively speaking, is better designed and probably better suited for backend development and microservices. However given that modern microservices are likely to use something like gRPC and HTTP/2 instead of serving REST APIs, even Flask isn't really strictly necessary.

I think that it is better not to think of a Python-based backend app as a "Django" or "Flask" or some-other-framework app, but instead structure it as a framework agnostic Python application that uses appropriate libraries as needed (which could include things like SQLALchemy, Flask, Graphene, gRPC, etc). This permits maximum flexibility, and makes it more straightforward to say, start with a monolithic codebase and then later break it up into smaller pieces without unnecessarily expensive rewrites.

For my last few startups I've been developing a simple backend application structure puts this idea to practice, which I've open-sourced as a template. It is a little bit inspired by Flask applications and other microframeworks, but taking the "micro" to the next level. It should be noted that this template could be re-used for either a monolith or a microservice; the intention is that the code structure shouldn't fundamentally change too much for either, so that it is easy to migrate from one to the other.

Here were some of the key design objectives:

1. **Not be overly tied to a specific library or framework**
  - Any library or technology should be possible to swap out (e.g. Flask could be swapped for another web framework, SQLAlchemy could be switched to another ORM, etc)
  - I avoid helper libraries like Flask-SQLAlchemy, because this would create too much of a Flask dependence
2. **Encourage good coding practices, like separation of concerns**.
  - Explicit coding style and separation of concerns (e.g. separate API, database and application logic layers) is good for testing, and also greatly simplifies refactoring and breaking apart a growing codebase
3. **Be prepared for future microservice refactors**.
  - Make it straightforward to start with a monolith or larger service, and refactor into smaller ones (or move functionality to another service). A microservice migration should look more like copy-pasting rather than a costly rewrite.
  - Common code and utilities live in a separate library
4. **Easy and fast development experience**.
  - Docker-compose based local development (one or two "clicks" to spin up the entire service)
  - Fast running unit test suite

I've also tried to retain some of the minimal things that web frameworks tend to do that are useful for an API-serving backend service. For example:
- A way to application configuration for different environments (local, staging, prod) with environment variables
- Have somewhere to do one-time application initialization stuff (like setting up database connections)
- Do cleanup between API requests or worker tasks (e.g. cleanup the database session, clear any in-memory cache)
- Developer conveniences (Python shell, CLI commands, database migration flow)

Check it out at [https://github.com/alvinchow86/python-backend-template](https://github.com/alvinchow86/python-backend-template), and feel free to try using it for your next Python backend project! Additional documentation is in the README.
