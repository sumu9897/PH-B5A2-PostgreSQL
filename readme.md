##  ১. What is PostgreSQL?

**PostgreSQL** হলো একটি ওপেন-সোর্স অবজেক্ট-রিলেশনাল ডেটাবেজ ম্যানেজমেন্ট সিস্টেম (ORDBMS)। এটি SQL-এর উপর ভিত্তি করে তৈরি, তবে এতে রয়েছে অনেক উন্নত ফিচার যেমন:

- ট্রানজ্যাকশন সাপোর্ট
- কাস্টম ডেটা টাইপ
- ইনডেক্সিং
- স্টোরড প্রসিডিউর
- ACID কমপ্লায়েন্স

PostgreSQL নিরাপদ, স্থিতিশীল এবং স্কেলযোগ্য হওয়ায় এটি এন্টারপ্রাইজ লেভেল প্রজেক্টে ব্যবহৃত হয়।

###  উদাহরণ:
```sql
CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  age INT,
  gpa NUMERIC(3,2)
);
```

---

##  ২. What is the purpose of a database schema in PostgreSQL?

**Schema** হচ্ছে একটি লজিক্যাল কাঠামো যা ডেটাবেজের টেবিল, ফাংশন, ভিউ প্রভৃতি অবজেক্টকে গ্রুপ আকারে সাজায়। 

###  উপকারিতা:
- ডেটাবেজ ম্যানেজমেন্ট সহজ হয়
- একাধিক অ্যাপ একই ডেটাবেজ ব্যবহার করতে পারে
- ডেটা নিরাপত্তা ও পারফরম্যান্স বাড়ে

###  উদাহরণ:
```sql
CREATE SCHEMA hr;

CREATE TABLE hr.employees (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  salary NUMERIC
);
```

---

##  ৩. Explain the Primary Key and Foreign Key concepts in PostgreSQL

###  Primary Key:
Primary Key এমন একটি কলাম বা কলামের সমষ্টি যা প্রতিটি রেকর্ডকে ইউনিকভাবে চিহ্নিত করে। এটি কখনো NULL হতে পারে না।

####  উদাহরণ:
```sql
CREATE TABLE departments (
  dept_id SERIAL PRIMARY KEY,
  dept_name VARCHAR(100)
);
```

###  Foreign Key:
Foreign Key এক টেবিলের কলামকে অন্য টেবিলের Primary Key-এর সাথে সংযুক্ত করে, এবং সম্পর্ক তৈরি করে।

####  উদাহরণ:
```sql
CREATE TABLE employees (
  emp_id SERIAL PRIMARY KEY,
  emp_name VARCHAR(100),
  dept_id INT REFERENCES departments(dept_id)
);
```

---

##  ৪. Explain the purpose of the WHERE clause in a SELECT statement.

`WHERE` ক্লজ ব্যবহার করে আপনি নির্দিষ্ট শর্ত অনুযায়ী টেবিল থেকে ডেটা ফিল্টার করতে পারেন। এটি SELECT, UPDATE, এবং DELETE কোয়ারিতে ব্যবহার হয়।

###  উদ্দেশ্য:
- নির্দিষ্ট রেকর্ড নির্বাচন করা
- ডেটা বিশ্লেষণ ও যাচাই করা
- অপ্রয়োজনীয় ডেটা বাদ দেওয়া

###  উদাহরণ:
```sql
SELECT * FROM students WHERE age > 20;
```

---

##  ৫. What are the LIMIT and OFFSET clauses used for?

`LIMIT` ও `OFFSET` PostgreSQL-এ ডেটা প্রদর্শনের পরিমাণ এবং শুরু করার পজিশন নিয়ন্ত্রণ করে। এটি সাধারণত Pagination বা পাতায় পাতায় ডেটা দেখানোর জন্য ব্যবহৃত হয়।

###  LIMIT:
`LIMIT` দ্বারা নির্ধারণ করা হয় কোয়ারি থেকে সর্বোচ্চ কতটি রেকর্ড রিটার্ন করবে।

```sql
SELECT * FROM employees LIMIT 5;
```

###  OFFSET:
`OFFSET` দ্বারা বলা হয় কতটি রেকর্ড স্কিপ করতে হবে, অর্থাৎ কত নম্বর রেকর্ড থেকে শুরু করা হবে।

```sql
SELECT * FROM employees OFFSET 10;
```

###  Pagination উদাহরণ:
```sql
-- Page 1: রেকর্ড 1 - 20
SELECT * FROM products LIMIT 20 OFFSET 0;

-- Page 2: রেকর্ড 21 - 40
SELECT * FROM products LIMIT 20 OFFSET 20;

-- Page 3: রেকর্ড 41 - 60
SELECT * FROM products LIMIT 20 OFFSET 40;
```

---