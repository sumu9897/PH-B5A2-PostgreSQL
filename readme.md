### ✅ ১. What is PostgreSQL?

**PostgreSQL** হলো একটি ওপেন-সোর্স এবং অবজেক্ট-রিলেশনাল ডেটাবেজ ম্যানেজমেন্ট সিস্টেম (ORDBMS)। এটি SQL ভাষার উপর ভিত্তি করে তৈরি, তবে এতে রয়েছে উন্নত ফিচার যেমন:

- ট্রানজ্যাকশন সাপোর্ট
- কাস্টম ডেটা টাইপ
- ইনডেক্সিং
- স্টোরড প্রসিডিউর
- ACID কমপ্লায়েন্স

PostgreSQL অনেক বেশি নিরাপদ এবং স্কেলেবল হওয়ায় বড় বড় এন্টারপ্রাইজ ও ডেভেলপাররা এটি ব্যবহার করে।

📌 **উদাহরণ:**

```sql
CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  age INT,
  gpa NUMERIC(3,2)
);
```

### ✅ ২. What is the purpose of a database schema in PostgreSQL?

**Schema** হলো একটি লজিকাল কাঠামো, যা PostgreSQL ডেটাবেজে বিভিন্ন অবজেক্ট যেমন টেবিল, ফাংশন, ভিউ ইত্যাদিকে গ্রুপ আকারে সংরক্ষণ করে।

#### 🟢 উপকারিতা:
- বড় ডেটাবেজকে ছোট অংশে ভাগ করা যায়
- আলাদা আলাদা অ্যাপ্লিকেশন একই ডেটাবেজে কাজ করতে পারে
- নিরাপত্তা ও ব্যবস্থাপনা সহজ হয়

📌 **উদাহরণ:**

```sql
CREATE SCHEMA hr;

CREATE TABLE hr.employees (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  salary NUMERIC
);
```

### ✅ ৩. Explain the Primary Key and Foreign Key concepts in PostgreSQL

PostgreSQL-এ ডেটাবেজ টেবিলগুলোর মধ্যে সম্পর্ক এবং ইউনিকনেস নিশ্চিত করার জন্য **Primary Key** এবং **Foreign Key** ব্যবহার করা হয়।

---

#### 🔹 Primary Key:
**Primary Key** এমন একটি কলাম বা কলামের সমষ্টি যা প্রতিটি রেকর্ডকে ইউনিকভাবে চিহ্নিত করে।  
এটি কখনো NULL হতে পারে না এবং প্রতিটি রেকর্ডের জন্য ইউনিক হতে হয়।

📌 **বৈশিষ্ট্যসমূহ**:
- প্রতিটি টেবিলে কেবল একটি Primary Key থাকতে পারে
- এটি স্বয়ংক্রিয়ভাবে `UNIQUE` এবং `NOT NULL` কনস্ট্রেইন্ট আরোপ করে

📌 **উদাহরণ**:

```sql
CREATE TABLE departments (
  dept_id SERIAL PRIMARY KEY,
  dept_name VARCHAR(100)
);
```

এখানে dept_id কলামটি Primary Key হিসেবে কাজ করছে এবং প্রতিটি ডিপার্টমেন্টের জন্য ইউনিক আইডি সরবরাহ করছে।

#### 🔹 Foreign Key:
**Foreign Key**  হলো এমন একটি কনস্ট্রেইন্ট যা এক টেবিলের কলামকে অন্য টেবিলের Primary Key-এর সাথে সংযুক্ত করে।

এটি টেবিলগুলোর মধ্যে সম্পর্ক তৈরি করে এবং রেফারেনশিয়াল ইন্টেগ্রিটি বজায় রাখে।

📌 **বৈশিষ্ট্যসমূহ**:
- এটি ডেটা ইন্টিগ্রিটি নিশ্চিত করে
- রিলেশন তৈরি করে Parent এবং Child টেবিলের মধ্যে



📌 **উদাহরণ**:

```sql
CREATE TABLE employees (
  emp_id SERIAL PRIMARY KEY,
  emp_name VARCHAR(100),
  dept_id INT REFERENCES departments(dept_id)
);
```
এখানে dept_id কলামটি departments টেবিলের dept_id কে রেফারেন্স করে। ফলে প্রতিটি কর্মচারী কোন ডিপার্টমেন্টে কাজ করে, তা নির্ধারণ করা যায়।