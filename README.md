# SugarFit_Sentiment_Insights_Google_Play_Store_Review_Analysis_and_Power_BI_Reporting
 <h1><a name="importrequiredlibraries">Import Required Libraries</a></h1>
  
```python
from google_play_scraper import app, Sort ,reviews_all
from app_store_scraper import AppStore
import pandas as pd 
import numpy as np 
import json,os,uuid
```
```
g_reviews=reviews_all(
    'fit.sugar.android',
    sleep_milliseconds=0,
    lang='en',
    country='us',
    sort=Sort.NEWEST,
)
```
```
g_df=pd.DataFrame(np.array(g_reviews),columns=['review'])
g_df2=g_df.join(pd.DataFrame(g_df.pop('review').tolist()))

g_df2.drop(columns={'userImage','reviewCreatedVersion'},inplace=True)
g_df2.rename(columns={'reviewId':'ID','userName':'Username','content':'Review','score':'AppRating','thumbsUpCount':'ThumbsUpCount','at':'ReviewTime','replyContent':'CompanyReply','repliedAt':'ReplyTime','appVersion':'AppVersion'},inplace=True)
g_df2

```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c365a80e-fde3-4b43-b696-35afd74aaec7"><br>
```
g_df2['AppRating'].mean()
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/43118838-5866-459e-a3ad-9726c8d5fe61"><br>
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
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/90616aa9-0728-4b14-bb29-e4f28bb5c66f">
```
from transformers import pipeline
sentiment_analysis = pipeline("sentiment-analysis",model="siebert/sentiment-roberta-large-english")
```
```
print(sentiment_analysis("I love this!"))
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/751b4f05-f66e-4a96-9868-0c9606c9ee27">
```
g_df2.dtypes
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c05d4887-dc3d-4bb0-881f-1df4b6c3acbe">
```
g_df2['Review']=g_df2['Review'].astype('str')
```
```
g_df2['result']=g_df2['Review'].apply(lambda x: sentiment_analysis(x))
```
```
g_df2.head()
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c85ed335-994a-47d5-8d52-16d0a4815b78">
```
g_df2['sentiment']=g_df2['result'].apply(lambda x: (x[0]['label']))
g_df2['score']=g_df2['result'].apply(lambda x: (x[0]['score']))
```
```
g_df2.head()
```
<img width="500" alt="Coding" src="ttps://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/e533f34d-73a7-457b-a05a-86a817f0fe1a">
```
g_df2['score'].mean()
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/d663220d-ae21-4631-9b67-604eca0739f5">
```
g_df2['sentiment'].value_counts()
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c8c49707-abaf-4f72-ab1a-d15f09b3239f">
```
g_df2['sentiment'].value_counts(normalize=True)
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/c2d1cbc6-d9ca-4745-a76e-69b1e4ebc7a3">
```
import plotly.express as px
fig=px.histogram(g_df2,x='sentiment',color='sentiment', text_auto=True)
fig.show()
```
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/6ba3152f-3d64-42c2-899b-ff31c419c5cc">
<img width="500" alt="Coding" src="https://github.com/Mariyajoseph24/SugarFit-Sentiment-Insights-Google-Play-Store-Review-Analysis-and-Power-BI-Reporting/assets/91487663/d5764a16-2a05-425a-9083-22a354483f01">
```
g_df2.to_csv("C:\\Users\\hp\\Desktop\\newfile.CSV")
g_df2=pd.read_csv("C:\\Users\\hp\\Desktop\\newfile.csv")
g_df2
```



