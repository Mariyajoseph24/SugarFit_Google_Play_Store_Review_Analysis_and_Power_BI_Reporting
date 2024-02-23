<h1>Sugarfit Google Play Store Review Analysis and Power BI Reporting</h1>
<img width="400" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit_Google_Play_Store_Review_Analysis_and_Power_BI_Reporting/assets/91487663/b0201363-15f4-40ec-9ed0-9c1f3a2fe9c9">
<h1>Contents📖</h1>
<ul>
  <li><a href="#introduction">Introduction</a></li>
  <li><a href="#datascrapingandsentimentanalysis">Data Scraping and Sentiment Analysis</a></li>
  <li><a href="#datacleaningandexploration">Data Cleaning and Exploration</a></li>
  <li><a href="#dataanalysis">Data Analysis</a></li>
  <li><a href="#datavisualization">Data Visualization</a></li>
  <li><a href="#findings">Findings</a></li>
</ul>

<h1><a name="introduction">Introduction</a></h1>
<p>Mobile applications heavily rely on user feedback to refine their offerings and ensure customer satisfaction. The Sugar.fit Android app, aimed at addressing diabetes-related concerns, stands to benefit greatly from an in-depth analysis of user reviews sourced from the Google Play Store. This project endeavors to leverage advanced analytics techniques to dissect these reviews, extracting valuable insights that can inform strategic decisions and drive improvements in app functionality and user experience.</p>

<p>Feel free to reach out for any questions or suggestions about this project. I'm open to discussions and eager to assist.
 <a href="https://www.linkedin.com/in/mariya-jos/">
  <img src=" Linkedln | Mariya Joseph" alt=""> Linkedln | Mariya Joseph</a><br>
  
  Don't forget to follow and star ⭐ the repository if you find it valuable.</p>

<ul>Tools Used🛠️:<br>
<li>Database:PostgreSQL</li>
<li>Programming Language: Python<br></li>
<li>Libraries: Pandas, Numpy, tensorflow<br></li>
<li>IDE: Microsoft Azure Data Studio<br></li></ul>

---------------------------------------------------------------------------------------------------------------------------------
<h1><a name="datascrapingandsentimentanalysis">Data Scraping & Sentiment Analysis📊</a></h1>

<ul>Tools Used🛠️:<br>
<li>Programming Language: Python<br></li>
<li>Libraries: Pandas, Numpy, Tensorflow<br></li>
<li>IDE: Microsoft Azure Data Studio<br></li></ul>
<ul>
 <li>Import Required Libraries</li>
  
```python
from google_play_scraper import app, Sort ,reviews_all
from app_store_scraper import AppStore
import pandas as pd 
import numpy as np 
import json,os,uuid
```
<li>Fetching Google Play Store Reviews for Sugarfit Android app</li>

```
g_reviews=reviews_all(
    'fit.sugar.android',
    sleep_milliseconds=0,
    lang='en',
    country='us',
    sort=Sort.NEWEST,
)
```
<li>Transforming and Cleaning Google Play Store Reviews Data for Analysis</li>

```
g_df=pd.DataFrame(np.array(g_reviews),columns=['review'])
g_df2=g_df.join(pd.DataFrame(g_df.pop('review').tolist()))

g_df2.drop(columns={'userImage','reviewCreatedVersion'},inplace=True)
g_df2.rename(columns={'reviewId':'ID','userName':'Username','content':'Review','score':'AppRating','thumbsUpCount':'ThumbsUpCount','at':'ReviewTime','replyContent':'CompanyReply','repliedAt':'ReplyTime','appVersion':'AppVersion'},inplace=True)
g_df2

```

<img width="900" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c365a80e-fde3-4b43-b696-35afd74aaec7"><br>
<li>Calculating the Mean App Rating of Sugar.fit Android App Reviews</li>

```
g_df2['AppRating'].mean()
```
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/43118838-5866-459e-a3ad-9726c8d5fe61"><br>
<li>Installing TensorFlow</li>

```
!pip install tensorflow
```
```
import tensorflow as tf
```
```
!pip install ipykernel
```
```
import tensorflow as tf
print(tf.__version__)
```
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/90616aa9-0728-4b14-bb29-e4f28bb5c66f"><br>
<li>Importing and Configuring Sentiment Analysis Pipeline</li>

```
from transformers import pipeline
sentiment_analysis = pipeline("sentiment-analysis",model="siebert/sentiment-roberta-large-english")
```
```
print(sentiment_analysis("I love this!"))
```
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/751b4f05-f66e-4a96-9868-0c9606c9ee27"><br>
<li>Checking Data Types of DataFrame Columns</li>

```
g_df2.dtypes
```
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c05d4887-dc3d-4bb0-881f-1df4b6c3acbe"><br>
<li>Converting Review Column to String Data Type</li>

```
g_df2['Review']=g_df2['Review'].astype('str')
```
<li>Applying Sentiment Analysis on Review Column</li>

```
g_df2['result']=g_df2['Review'].apply(lambda x: sentiment_analysis(x))
```
```
g_df2.head()
```
<img width="900" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c85ed335-994a-47d5-8d52-16d0a4815b78"><br>
<li>Extracting Sentiment Label and Score from Result Column</li>

```
g_df2['sentiment']=g_df2['result'].apply(lambda x: (x[0]['label']))
g_df2['score']=g_df2['result'].apply(lambda x: (x[0]['score']))
```
```
g_df2.head()
```
<img width="900" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/e533f34d-73a7-457b-a05a-86a817f0fe1a"><br>
<li>Calculating the Mean Sentiment Score</li>

```
g_df2['score'].mean()
```
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/d663220d-ae21-4631-9b67-604eca0739f5"><br>
```
g_df2['sentiment'].value_counts()
```
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c8c49707-abaf-4f72-ab1a-d15f09b3239f"><br>
<li>Calculating Normalized Sentiment Distribution</li>

```
g_df2['sentiment'].value_counts(normalize=True)
```
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c2d1cbc6-d9ca-4745-a76e-69b1e4ebc7a3"><br>
<li>Visualizing Sentiment Distribution with Plotly Express</li>

```
import plotly.express as px
fig=px.histogram(g_df2,x='sentiment',color='sentiment', text_auto=True)
fig.show()
```
<img width="900" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/6ba3152f-3d64-42c2-899b-ff31c419c5cc"><br>
<img width="900" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/d5764a16-2a05-425a-9083-22a354483f01"><br>
<li>Exporting DataFrame to CSV File and Reading it Back</li>

```
g_df2.to_csv("C:\\Users\\hp\\Desktop\\newfile.CSV")
g_df2=pd.read_csv("C:\\Users\\hp\\Desktop\\newfile.csv")
g_df2
```
------------------------------------------------------------------------------------------------------------

<h1><a name="datacleaningandexploration">Data Cleaning and Exploration🧹</a></h1>

<ul><li>Tools Used🛠️:Microsoft Excel</li></ul>
<ul>
<li>Deleted unwanted columns that is not required for this analysis</li>
<li>Checked and formatted the cells with proper datatypes</li>
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/984f4495-5552-4e3b-bfb4-674fde38bc45">
  
<li>Missing Values in each column</li></ul>
<ol>
<li>used filter function in excel to identify missing/null values</li>
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/9c97b9ed-40ba-4fa2-b7b1-a963d60afcf5">

<li>conditional foramtting to identify and highlight the missing values</li></ol>
<img width="300" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/bac7f686-a690-414e-b0d5-9b99b2d819c7">

<ul><li>Removing the duplicates</li>
<img width="100" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/bab31516-23dc-4433-a9e9-6ebdff1b5f71">

<li>Handling the missing values by using find & select inbuilt function in excel</li></ul>
<ol>
<li>Replaced the blank space with NULL for the column that is TEXT Datatype</li>
<li>Replaced the blank space with a default date value for the column that is DATE Datatype</li></ol>
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c669aeed-ea8b-4a4f-a00e-e63faee38639">
<img width="200" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/ebc37967-7369-40fa-8fb1-51438bd9b5a6">
------------------------------------------------------------------------------------------------

<h1><a name="dataanalysis">Data Analysis📈</a></h1>
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
------------------------------------------------------------------------------------------------------
<h1><a name="datavisualization">Data Visualization</a></h1>
<ul><li>Tools Used⚙️:Microsoft Power BI</li></ul>
<img width="900" alt="Coding" src=https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/784658f5-f0df-439a-abe6-b616168c8390>

---------------------------------------------------------------------------------------------------------
<h1><a name="findings">Findings</a></h1>
<p>Based on the analysis conducted in the project, the following findings and suggestions can be derived:</p>
<ol>
<li><b>Understanding User Issues:</b> By analyzing the negative reviews, we gained insights into user concerns and issues. This enables us to address them more effectively, leading to improved user satisfaction.</li>

<li><b>Identifying Review Trends:</b> The project helped in identifying trends in user reviews, such as common topics mentioned in negative feedback or frequently praised aspects in positive reviews. This information can guide product development and marketing strategies.</li>

<li><b>Enhancing Customer Trust:</b> Responding promptly to customer reviews demonstrates attentiveness and care towards users' experiences. It fosters trust and loyalty among customers, showing them that their feedback is valued and acted upon.</li>

<li><b>Improving Customer Engagement:</b> Engaging with customers through timely replies to reviews creates a positive interaction and strengthens the relationship between the company and its users. It encourages ongoing dialogue and fosters a sense of community around the product.</li>

<li><b>Leveraging Feedback for Improvement:</b> Analyzing user feedback provides valuable insights for product improvement and feature development. By addressing user concerns and implementing suggestions, the company can enhance the overall user experience and stay competitive in the market.</li>

<li><b>Understanding Pain Points:</b> Negative reviews often highlight areas where users are facing challenges or experiencing dissatisfaction with the product or service. By analyzing these reviews, we can pinpoint specific pain points and areas for improvement.</li>

<li><b>Proactive Issue Resolution:</b> Identifying and addressing negative feedback promptly demonstrates a proactive approach to problem-solving. By acknowledging user concerns and taking steps to resolve issues, the company can prevent further escalation and mitigate potential damage to its reputation.</li>

<li><b>Opportunity for Improvement:</b> Negative reviews present valuable opportunities for improvement. By listening to user feedback and incorporating suggestions for enhancement, the company can iteratively improve its products or services, ultimately leading to a better user experience and increased customer satisfaction.</li>

<li><b>Building Trust and Credibility:</b> Transparently addressing negative feedback shows users that their concerns are taken seriously and that the company is committed to delivering a high-quality product or service. This builds trust and credibility with users, fostering stronger relationships and brand loyalty over time.</li>

<li><b>Continuous Feedback Loop:</b> By monitoring and analyzing negative reviews on an ongoing basis, the company can establish a continuous feedback loop for product improvement. This allows for agile and responsive development, ensuring that user needs and preferences are always top of mind.</li></ol>





