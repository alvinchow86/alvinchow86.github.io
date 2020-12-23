---
layout: post
title: SQLAlchemy PostgreSQL 64-bit ID generation
categories: Backend
excerpt: Introducing SQLAlchemy-Postgres-BigInt-ID, a library to automate 64-bit IDs in SQLAlchemy and PostgreSQL.
---

In my last couple of companies I have started using 64-bit "Instagram/Snowflake" style as the primary keys for tables in Postgres and SQLAlchemy.

The IDs are generated in the database via Postgres functions. Basically the idea is to encode the current timestamp in most of the bits, while reserving some bits for shard ID and some for an autoincrementing sequence (to guarantee no duplicates even if a ID is generated in the same millisecond.)

Compared to 32-bit IDs, you will not have to run out of IDs for many years, and you do not leak information about the size of your tables even if used in APIs.

UUID is an "easy" option but I find they feel a bit overkill in terms of space. Not only are your primary keys larger, but indices, foreign keys, Redis keys, URLS, get bigger as well. Also they are a slightly annoying to work with due to their length and dashes.

64-bit BIGINT for IDs are nice in that they are just twice as larger as 32-bit INT but are still more than enough for any realistic table.

In practice, I just use these 64-bit IDs for everything and forget about it. In theory if you really want to optimize for space, you could use normal 32-bit IDs for tables you know will remain small, but in practice I think it's easier to just be consistent and have one rule, versus having to decide on a table by table basis.

If you are using SQLAlchemy and Postgres, I've made a helper library that automates everything for you.

Check it out at [https://github.com/alvinchow86/sqlalchemy-postgres-bigint-id](https://github.com/alvinchow86/sqlalchemy-postgres-bigint-id). It's released on [PyPi](https://pypi.org/project/sqlalchemy-postgres-bigint-id) so you can easily install it. Instructions are in the README.
