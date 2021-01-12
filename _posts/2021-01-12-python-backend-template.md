---
layout: post
title: Building a Framework-Independent Python Backend
categories: Backend
excerpt: My template for building a modern Python backend service that's not tied to a specific framework.
---
Django has been a popular and convenient framework on the Python side, but in my experience it itself is bloated and monolithic and contains a lot of things that are outdated for modern API-centric backends (e.g. forms). It bundles a lot of things like an ORM and templating language, but none of these are even the best available libraries at what they do. More importantly, relying too much on Django patterns, features and plug-ins actually makes it harder to eventually refactor a monolith into microservices.

Flask is a much smaller "micro framework" which, comparatively speaking, is better designed and probably better suited for backend development and microservices. However given that modern microservices are likely to use something like gRPC and HTTP/2 instead of serving REST APIs, even Flask isn't really strictly necessary.


Check it out at [https://github.com/alvinchow86/python-backend-template](https://github.com/alvinchow86/python-backend-template)
