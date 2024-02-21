<h1>Data Analysis📈</h1>
<ul><li>Tools Used⚙️:PostgreSQL</li></ul>
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
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/186def57-7b77-47b8-a46a-ceb0dd7c8aeb">

<li>Selecting and viewing the dataset</li>

```sql
SELECT * FROM SF1
```
<img width="400" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/029a3b78-0d6d-4d30-bf8f-24f1b2bcd055">

<li>Total Number of reviews</li>

```sql
SELECT COUNT(*) AS total_reviews
FROM sf1;

```
<img width="150" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/3b5e059d-6d0b-493a-9175-2ffeb137d9e2">

<li>Total number of positive reviews</li>

```
SELECT COUNT(*)
FROM SF1
WHERE sentiment='POSITIVE';
```
<img width="150" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/9ca14fbb-ccd9-4be0-a958-7d7f4585627a">

<li>Total number of negative reviews</li>

```
SELECT COUNT(*)
FROM SF1
WHERE sentiment='NEGATIVE';
```

<img width="150" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/0484a158-68ea-49bb-bd72-f63cb677ba73">

<li>Average App Rating</li>

```sql
SELECT AVG(AppRating) AS average_rating
FROM sf1


```
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/b570d3b8-5056-477a-b29b-75ef9efc65ca">
<li>Review with highest thump count</li>

```sql
SELECT Review, ThumbsUpCount
FROM sf1
ORDER BY ThumbsUpCount DESC
LIMIT 1;


```
<img width="400" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/db6b7f20-7f41-407e-920f-a80ccf954915">
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/7ba91e7f-2682-4c41-805a-4d456da0dce8">
<li>Users with high number of reviews</li>

```sql
SELECT Username, COUNT(*) AS review_count
FROM sf1
GROUP BY Username
ORDER BY review_count DESC
LIMIT 5;


```
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/262fd4ad-5f8d-48d2-95a5-b4b6e2d48168">
<li>Average Sentiment Score</li>

```sql
SELECT AVG(score) AS average_sentiment_score
FROM sf1;


```
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/e70b7572-b098-4d1d-92b4-b56adfaacd46">
<li>Count of User Reviews that are not replied by company</li>

```sql
SELECT COUNT(*)AS not_replied
FROM SF1
WHERE companyreply='NULL';


```
<img width="150" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/1a92f383-e483-4408-9c27-4fc5dba235d3">
<img width="150" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/cdb3c61d-6d20-4cb4-acc2-a8af1c7ad92c">
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
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/14f98363-d600-438b-b278-a63f61377765">

<li>Reviews with sentiment negative to analyze the issues</li>

```sql
SELECT review
FROM sf1
WHERE sentiment = 'NEGATIVE';


```
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/bbdda107-a70f-4a5e-ab1a-584bfaabbb39">
<li>Distribution of ratngs and it's total count</li>

```sql
SELECT AppRating, COUNT(*) AS rating_count
FROM sf1
GROUP BY AppRating
ORDER BY rating_count DESC;

```
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/ea80d384-acc3-4eb2-b6c4-cdf8c0229610">
<li>Reviews with the text like 'Challenges'</li>

```sql
SELECT id,review
FROM sf1
WHERE Review LIKE '%challenges%';

```
<img width="400" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/6249e3b8-58dc-4bf7-a868-3d691c1ef634">
<li>Total number of reviews per year</li>

```sql
SELECT EXTRACT(YEAR FROM ReviewTime) AS review_year, COUNT(*) AS review_count
FROM sf1
GROUP BY review_year
ORDER BY review_year;


```
<img width="250" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/ab4c57bc-d55b-40a3-b5bc-720d1dc86b33">
<li>Reviews with the text like 'Personalized diet'</li>

```sql
SELECT id,review
FROM sf1
WHERE Review LIKE '%personalized diet%';


```
<img width="400" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/3af290dd-1ba7-47a1-991a-fa2e79cafd74">
<li>Latest 5 reviews and date</li>

```sql
SELECT review,reviewtime
FROM sf1
ORDER BY ReviewTime DESC
LIMIT 5;


```
<img width="400" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/3f99e894-82d7-45a0-9562-f1d44e6628a7">
<img width="100" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/be4e0878-d3df-41c3-9af2-aa2505b75244">






</ul>
