---
layout: post
title: Python and SQL
date: 2018-04-23 00:00:00 +0300
description: How to get started using SQL with Python.
img: flight.jpg
tags: [Meetup's, Python, SQL]
caption: Taken on Air New Zealand flight NZ001 over Washington, USA.
---

On Thursday 19th Feb I attended my first meetup event from the [Python North West User group][PyNW group]. The material of this session was focussed on SQL and featured a presentation and live demo of how SQL can be used with Python, delivered by [Dave Jones][DJ GitHub]. This was particularly good as you got hands-on with the code, with Dave leading the way to ensure everything worked. Here I have written a brief write up of the main points from the meetup and some of the SQL that we went through.

#### So what is SQL?

[SQL][SQL wiki], which stands for Structured Query Language, has been around a long time and has been an ISO standard since the 1980’s. It is a language which is used for managing data in relational databases and is very widely used - such as to run everyone's bank accounts. Practically speaking, as it is old the standard is not followed universally and there are a number of different ways of running SQL. Furthermore, there have been a number of attempts to replace it, however it is still the de-facto standard. 

#### Using SQL with Python

In Python, there are many different libraries for interfacing with SQL, but they can be badly designed and too variable/low-level to be useful. Dave recommended the libraries SQLAlchemy and Pandas to do the bulk of the work. Once you have them installed you can load up a terminal window and enter the following to create a new SQL engine using SQLAlchemy.

{% highlight python %}
import sqlalchemy as sa
import pandas as pd
engine = sa.create_engine('sqlite:///newdatabase.db')
{% endhighlight %}

Then you can connect to it with

{% highlight python %}
c = engine.connect()
{% endhighlight %}

Now you are ready to start creating the powerful relational databases which are possible with SQL. This makes use of the engine [SQLite][SQLite link], which comes bundled in Python. To speak to the engine you then write your SQL commands into a string and pass them into the engine for execution.

{% highlight python %}
sql = """ SQL commands here """
c.execute(sql)
{% endhighlight %}

#### Creating a table

In the session, Dave used the example of a flight data recording system. First things first you will want to create a table to store the data. The SQL command that you would pass is as follows.

{% highlight sql %}
CREATE TABLE readings (
    flight    VARCHAR(10) NOT NULL,
    ts        TIMESTAMP NOT NULL,
    temp      NUMERIC(3,1) NOT NULL,
    pressure  NUMERIC(4,0) NOT NULL,
    humidity  NUMERIC(3,0) NOT NULL,
    accel_x   REAL DEFAULT 0 NOT NULL,
    accel_y   REAL DEFAULT 0 NOT NULL,
    accel_z   REAL DEFAULT 0 NOT NULL,
    CONSTRAINT readings_pk PRIMARY KEY (flight, ts),
    CONSTRAINT temp_ck CHECK (temp BETWEEN -70 AND 70),
    CONSTRAINT pres_ck CHECK (pressure BETWEEN 0 AND 2000),
    CONSTRAINT hum_ck CHECK (humidity BETWEEN 0 AND 100)
{% endhighlight %}

Here we have created a table called "readings", with multiple columns titled "fight", "ts", "temp", etc. For each column we specify a data-type, e.g. TIMESTAMP must be a time/date, and NUMERIC, is a number. You can read more about data types [here][SQL data types]. We also specify that each column cannot contain a NULL value, this is good practice and ensures that data must be entered into each column to create a new row. Finally, and perhaps most importantly, we can apply constraints to the data. 

Firstly, we must specify a PRIMARY KEY, which is a unique identifier for each row in the table. This is very important as the order of rows in the table is not fixed and SQL can move them around a bit, therefore a key for each row is necessary. In our case, the key for each row is a combination of the flight and ts columns - i.e. each row must have a unique combination of timestamp and flight number. So a single flight cannot record twice on the same timestamp, which makes sense.

Next, we constrain some of the data, specifically the temperature, pressure and humidity measurements to ensure they are physical.

So to actually run this command in the terminal we simply paste the SQL into a string and then pass that to SQLAlchemy.

{% highlight python %}
sql = """ 
CREATE TABLE readings (
    flight    VARCHAR(10) NOT NULL,
    ts        TIMESTAMP NOT NULL,
    temp      NUMERIC(3,1) NOT NULL,
    pressure  NUMERIC(4,0) NOT NULL,
    humidity  NUMERIC(3,0) NOT NULL,
    accel_x   REAL DEFAULT 0 NOT NULL,
    accel_y   REAL DEFAULT 0 NOT NULL,
    accel_z   REAL DEFAULT 0 NOT NULL,
    CONSTRAINT readings_pk PRIMARY KEY (flight, ts),
    CONSTRAINT temp_ck CHECK (temp BETWEEN -70 AND 70),
    CONSTRAINT pres_ck CHECK (pressure BETWEEN 0 AND 2000),
    CONSTRAINT hum_ck CHECK (humidity BETWEEN 0 AND 100)
"""
c.execute(sql)
{% endhighlight %}

#### Inserting data

We can insert data into this table using the following SQL commands.

{% highlight sql %}
INSERT INTO readings(flight, ts, temp, pressure, humidity)
VALUES ('hab1', '2015-01-01 09:00:00', 25.5, 1020, 40);

-- Inserting multiple rows in a single statement
INSERT INTO readings(flight, ts, temp, pressure, humidity)
VALUES
  ('hab1', '2015-01-01 09:01:00', 25.5, 1019, 40),
  ('hab1', '2015-01-01 09:02:00', 25.5, 1019, 41);

-- Inserting the results of a query
INSERT INTO readings
SELECT flight, DATETIME(ts, '+3 minutes') AS ts, temp,
       pressure, humidity, accel_x, accel_y, accel_z
FROM readings;
{% endhighlight %}

In the final line, we query the table and then insert new lines which are shifted along in time by 3 minutes.

#### Viewing the data

To view the data we can use Pandas (we change the display options so that it fits on the page better). 

{% highlight python %}
pd.set_option('display.width', 120)
pd.read_sql('readings', c)
{% endhighlight %}

If you have inserted all the lines into the table by running the SQL commands detailed above then you should see a six-line table as the result.

{% highlight bash %}
      flight                  ts  temp  pressure  humidity  accel_x  accel_y  accel_z
0   hab1 2015-01-01 09:00:00  25.5      1020        40        0        0        0
1   hab1 2015-01-01 09:01:00  25.5      1019        40        0        0        0
2   hab1 2015-01-01 09:02:00  25.5      1019        41        0        0        0
3   hab1 2015-01-01 09:03:00  25.5      1020        40        0        0        0
4   hab1 2015-01-01 09:04:00  25.5      1019        40        0        0        0
5   hab1 2015-01-01 09:05:00  25.5      1019        41        0        0        0
{% endhighlight %}

#### Working with a lot of data

Every time we run the execute command we make a transaction with the database and all the changes are immediately written to the database file. This makes transactions computationally expensive and therefore when working with a lot of data it is best to group data together and perform them in one transaction. If you have a dataset that is in a .csv file then a quick way to import it all into the table is as follows.

{% highlight python %}
def load_data(filename):
    insert = """
        INSERT INTO readings
            (flight, ts, temp, pressure, humidity,
            accel_x, accel_y, accel_z)
        VALUES
            ('hab1', ?, ?, ?, ?, ?, ?, ?)
    """
    data = pd.read_csv(filename)
    data = [
        (row.timestamp, row.temp_h, row.pressure,
         min(100, max(0, row.humidity)),
         row.accel_x, row.accel_y, row.accel_z)
        for row in data.itertuples()
    ]
    with c.begin():
        c.execute("DELETE FROM readings")
        c.execute(insert, data)
{% endhighlight %}

You can also see the [to_sql()][Pandas to_sql] method in Pandas. You have to be careful when inserting large amounts of data to ensure you do not leave yourself vulnerable to [SQL injection][SQL inject].

#### Saving the data

One query I had during the meetup was how to save the data. Well, as I mentioned before, each transaction with the database saves everything to hard disk. Therefore, you should see a 'newdatabase.db' file in the directory you have been working in. Dave reassured us that these files are hard to corrupt or damage, which is handy given all the important data companies store in them.

I hope that this post has helped some of you appreciate how easily you can get a database set up in SQL. I am looking to getting some more hands-on experience of it in the future. If you have any comments or corrections to this post then please [let me know][my email].

[PyNW group]: https://www.meetup.com/Python-North-West-Meetup/
[DJ GitHub]: https://github.com/waveform80/
[SQL wiki]: https://en.wikipedia.org/wiki/SQL
[SQLite link]: https://www.sqlite.org/index.html
[SQL data types]: https://www.w3schools.com/sql/sql_datatypes.asp
[Pandas to_sql]: https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_sql.html
[SQL inject]: https://www.w3schools.com/sql/sql_injection.asp
[my email]: mailto:henryfcox@live.com