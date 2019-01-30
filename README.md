# LearnFromBest
A platform for you to make most of the github by following the right person regarding to your interest.

## Project Idea
Started from 2008, Github is now one of the most popular open source community in tech world. As of 2018, there are 28 million users and 57 million repositories, making it the largest host of source code in the world. 

Github is also one of the best sources for learning coding, we share code, publish new project, follow and learn from other users. But github do not have a system to help you find the right person and resources on specific area.

**Everyone wants to learn from the best, this project aims to creat a platform which can help you on finding the social influencer from the github network.**

## Data Source
* [Github archive](https://www.gharchive.org/) : GH Archive is a project to record the public GitHub timeline, which stores all the event based github. Weighing in over **3TB** total, this is the largest Bigquery dataset available on kaggle.
* Data size: 80~100G/month since 2011
* Update frenquency: Update every 1 hour

## Tech Stack 

![Tech Stack](https://raw.githubusercontent.com/catherinesdataanalytics/LearnFromBest/master/pics/tech_flow_V2.png)

* **Data Ingestion**
   - Raw data stored in Bigquery, it will be cleaned with bigquery and will be transferred to HDFS.
   - New coming data cleaning: use bigquery api and airflow scheduler to clean the updated new coming data and append to historical data in HDFS.
   - HDFS: All data will be stored to HDFS for data processing in spark.

* **Data Processing** 
   - use spark for batch processing data on HDFS
   - algorithms(PageRank) written in scala 
   - other network analysis algorithms in graphX (TBD)

* **Database** 
   - Mysql, with 9 table corresponding to 9 languages. May be used for join later.

* **User Interface** 
   - Flask, user can select the language and they will get recommended users ranking by the social influencer score.

## Engineering challenge
* Data modeling: work on mapping user with languages from event data
* Processing and cleaning 2.9TB github event data in json format, slice and find the right field. - lambda 
* 80~100 G per month, and update every 1 hour in bigquery. Use airflow auto the whole processing. - airflow
* mysql connect and read from S3 using spark session 
* scala and graphX

## Alogorithms
* Centrality Measures: Pagerank in Scala
* Community Detection: Strongly Connected Components
* GraphX and more analysis soon.
<img src="https://raw.githubusercontent.com/catherinesdataanalytics/LearnFromBest/master/pics/graphSpark.png " width="550">

## Business Value
1. If you want to learn "Golang" or other languages, this platform will recommend you the most valueble github user to follow and learn from based on network analysis results.
2. For example, Show the 10 or N people to learn from based on network analysis result.
Recommend community for colaboration.

## Temporal output
* show sample result of the github user. User list which has a high pagerank score.
* show the pagerank score which are defined by the user language.

4.glassesfactory,68.0407463652.
68,desandro,59.9803118883.
119,defunkt,59.4355582686.
53,mojombo,56.4538433468.
95,GillesHaverbeke,56.4495397138.
130,visionmedia,51.6731830982.
40,paulirish,50.9951976587.
114,zurmo,49.3660697581.
17,substack,43.313750552.
67,schacon,37.3535144986.
94,douglascrockford,36.7314431584.
60,Marak,34.9735266652.
51,lokesh,34.834088857.
6,ry,33.7864270164.
105,holman,33.5289454831.
11,jashkenas,32.6160846564.
49,marijnh,32.4338197749.
52,jeresig,31.9755856618.
30,zedshaw,31.7697354151.
19,trevorturk,30.8578839416.
9,kennethreitz,30.4337720903.

## Further Questions
* Is it a good way to make most of bigquery API and make input data small, will this reduce the depth of spark?
* The way to make the whole process real time
* make data clean for deleted user and delete no following users
* move to scala, test structure in scala 
