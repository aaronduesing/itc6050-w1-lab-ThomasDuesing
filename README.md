"# ITC 6050 - Week 1 Lab" 

: Why are we running Postgres in Docker instead of installing it directly? Write a
one-sentence answer in your README.md. (Hint: the answer is in the Week 1 deck.)


Concept check: What did dlt do for you that you would have had to write yourself if you were
using plain Python + SQLAlchemy? List three things in your README.

Concept check: Notice how nested fields (like user, labels) became columns in the table. How
did dlt handle the JSON arrays? Look at the column types and find the JSONB ones — that's
modern Postgres + dlt working together.


Stretch: Write a query that returns the top 5 issue authors by number of issues opened. (Hint:
user__login is your friend.)

 SELECT column_name, data_type
FROM information_schema.columns
WHERE table_schema = 'raw'
 AND table_name = 'github_issues'
ORDER BY ordinal_position
LIMIT 40;
lab=# SELECT user__login, COUNT(*) AS issue_count
FROM raw.github_issues
GROUP BY user__login
ORDER BY issue_count DESC
LIMIT 5;
  user__login  | issue_count
---------------+-------------
 zilto         |          27
 elviskahoro   |          13
 rudolfix      |           8
 lis365b       |           6
 AyushPatel101 |           5
(5 rows)

Concept check: Why did we build stg_github_issues as a separate model first, instead of
writing one giant SELECT in issues_summary? (Hint: think about what happens when six analysts
each want a slightly different summary.)
