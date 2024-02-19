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
1111
```
g_df2['AppRating'].mean()
```
2222
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
3333
```
from transformers import pipeline
sentiment_analysis = pipeline("sentiment-analysis",model="siebert/sentiment-roberta-large-english")
```
```
print(sentiment_analysis("I love this!"))
```
4444
```
g_df2.dtypes
```
5555
```
g_df2['Review']=g_df2['Review'].astype('str')
```
```
g_df2['result']=g_df2['Review'].apply(lambda x: sentiment_analysis(x))
```
```
g_df2.head()
```
666
```
g_df2['sentiment']=g_df2['result'].apply(lambda x: (x[0]['label']))
g_df2['score']=g_df2['result'].apply(lambda x: (x[0]['score']))
```
```
g_df2.head()
```
777
```
```
g_df2['score'].mean()
```
888
```
g_df2['sentiment'].value_counts()
```
999
```
```
g_df2['sentiment'].value_counts(normalize=True)
```
1010
```
import plotly.express as px
fig=px.histogram(g_df2,x='sentiment',color='sentiment', text_auto=True)
fig.show()
```
11 11
12 12
```
g_df2.to_csv("C:\\Users\\hp\\Desktop\\newfile.CSV")
g_df2=pd.read_csv("C:\\Users\\hp\\Desktop\\newfile.csv")
g_df2
```



