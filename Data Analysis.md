<ul>
  <li>Creating and importing dataset to postgreSQL</li>
 
</ul>

```
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
<li>Select and viewing the dataset</li>

```
SELECT * FROM SF1
```
222
</ul>
