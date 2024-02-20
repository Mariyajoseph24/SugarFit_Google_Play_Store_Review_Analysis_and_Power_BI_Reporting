<ul>
  <li>Creating and importing dataset to postgreSQL</li>
 
</ul>

```sql
CREATE TABLE SF1 (
  ID VARCHAR(50),
  Username VARCHAR(50),
  Review VARCHAR(5000),
  AppRating INT,
  ThumbsUpCount INT,
  ReviewTime DATE,
  CompanyReply VARCHAR(5000),
  ReplyTime DATE,
  sentiment VARCHAR(10),
  score NUMERIC );

```
111

<li>Selecting and viewing the dataset</li>

```sql
SELECT * FROM SF1
```
222

<li>Total Number of reviews</li>

```sql
SELECT COUNT(*) AS total_reviews
FROM sf1;

```
333
<li>Average App Rating</li>

```sql
SELECT AVG(AppRating) AS average_rating
FROM sf1


```
444
<li>Review with highest thump count</li>

```sql
SELECT Review, ThumbsUpCount
FROM sf1
ORDER BY ThumbsUpCount DESC
LIMIT 1;


```
555
<li>Users with high number of reviews</li>

```sql
SELECT Username, COUNT(*) AS review_count
FROM sf1
GROUP BY Username
ORDER BY review_count DESC
LIMIT 5;


```
666
<li>Average Sentiment Score</li>

```sql
SELECT AVG(score) AS average_sentiment_score
FROM sf1;


```
777
<li>Count of User Reviews that are not replied by company</li>

```sql
SELECT COUNT(*)AS not_replied
FROM SF1
WHERE companyreply='NULL';


```
888
<li>Total number of reviews that are replied by company</li>

```sql
SELECT id,review
FROM SF1
WHERE companyreply='NULL';
```

<li>Reviews that are not replied by company</li>

```sql
SELECT COUNT(*)AS replied
FROM sf1
WHERE id NOT IN
(SELECT id
FROM SF1
WHERE companyreply='NULL');


```
9

<li>Reviews with sentiment negative to analyze the issues</li>

```sql
SELECT review
FROM sf1
WHERE sentiment = 'NEGATIVE';


```
10
<li>Distribution of ratngs and it's total count</li>

```sql
SELECT AppRating, COUNT(*) AS rating_count
FROM sf1
GROUP BY AppRating
ORDER BY rating_count DESC;

```
11
<li>Reviews with the text like 'Challenges'</li>

```sql
SELECT id,review
FROM sf1
WHERE Review LIKE '%challenges%';

```
12
<li>Total number of reviews per year</li>

```sql
SELECT EXTRACT(YEAR FROM ReviewTime) AS review_year, COUNT(*) AS review_count
FROM sf1
GROUP BY review_year
ORDER BY review_year;


```
13
<li>Reviews with the text like 'Personalized diet'</li>

```sql
SELECT id,review
FROM sf1
WHERE Review LIKE '%personalized diet%';


```
14
<li>Latest 5 reviews and date</li>

```sql
SELECT review,reviewtime
FROM sf1
ORDER BY ReviewTime DESC
LIMIT 5;


```
15






</ul>
