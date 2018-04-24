---
layout: post
title: SQL in Python
date: 2018-04-19 00:00:00 +0300
description: 
img: peaks.jpg
tags: [Meetup's, Python, SQL]
---

On Thursday 19th Feb I attended my first meetup event from the [Python North West User group][PyNW group]. The material of this session was focussed on SQL and featured a presentation and live demo of how SQL can be used with Python, delivered by [Dave Jones][DJ GitHub]. This was particularly good as you got hands on with the code, with Dave leading the way to ensure everything works. Here I have written a brief sum up of the main points from the meetup.

#### So what is SQL?

[SQL][SQL wiki], which stands for Structured Query Language, has been around a long time and has been an ISO standard since the 1980’s. It is a language which is used for managing data in relational databases and is very widely used - such as to run everyones bank accounts. Practically speaking, as it is old the standard is not followed universally and there are a number of different ways of running SQL. Furthermore, there have been a number of attempts to replace it, however it is still the de-facto standard. 

#### Using SQL with Python

In Python there are many different libraries for interfacing with SQL, but they can be badly designed and too variable/low-level to be useful. Dave recommended the libraries SQLAlchemy and Pandas to do the bulk of the work. Once you have them installed you can load up a terminal window and enter the following to create a new SQL engine using SQLAlchemy.

```python
import sqlalchemy as sa
import pandas as pd
engine = sa.create_engine('sqlite:///flight.db')
```

Then you can connect to it with

```python
c = engine.connect()
```

and now you are ready to start creating the powerful relational databases which are possible with SQL. This makes use of the engine [SQLite][SQLite link], which comes bundled in Python. To speak to the engine you then write your SQL commands into a string and pass them into the engine for execution.

```python
sql = """ SQL commands here """
c.execute(sql)
```

#### So what can you do with SQL?



[PyNW group]: https://www.meetup.com/Python-North-West-Meetup/
[DJ GitHub]: https://github.com/waveform80/
[SQL wiki]: https://en.wikipedia.org/wiki/SQL
[SQLite link]: https://www.sqlite.org/index.html