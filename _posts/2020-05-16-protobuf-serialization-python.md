---
layout: post
title: Python Protobuf Serialization Library
categories: Backend
excerpt: Introducing protobuf-serialization-py, helpers for Python gRPC protobuf serialization/deserialization.
---

While the Python protobuf library already has a class-based infrastructure, it can be very awkward to use, and there are a lot of operations you are restricted from doing. This library uses a familiar class-based "serializer" interface to make it easy to define how you'd like to map a Python object (such as a Django or SQLAlchemy model instance) or a source dictionary to an output, which in this case is a Python protobuf instance (rather than a dictionary object).

Another problem this solves is that protobuf3 doesn't support nullable values for primitives like strings, integers, bool. In real-life applications involving databases, it is very common to have data to sometimes be NULL/None. APIs often also have this need as well - NULL may have an actual meaning that isn't conveyed by the default primitive value (empty string, 0, false). When transitioning from something like a REST API to gRPC, I felt that this was something that is missing.

A solution for this is to use Google's wrapper values (like IntValue), which basically wrap a primitive inside a message (which CAN be nullable). However they can be cumbersome to work with. This library automates that away in both serializtion and deserialization directions so you don't have to think about it - values are encoded to a wrapped value, and unwrapped again in the deserialization step.

I've created a library to help with serializing and deserialization of Protobuf3 in Python for your gRPC application. It's inspired by serialization libraries like marshmallow, Django rest Framework and serpy, but for protobuf3 instead of JSON, and optimized with serialization performance in mind.

Check it out at [https://github.com/alvinchow86/protobuf-serialization-py](https://github.com/alvinchow86/protobuf-serialization-py) and on [PyPi](https://pypi.org/project/protobuf-serialization).

More documentation to come!
