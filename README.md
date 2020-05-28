# FDP-LogParsing-Project
This is the submission for LogParsing project as required for FDP program on Big Data with SPARK conducted by CloudxLab and EICT IIT Roorkee.

My Name :Aaditya Dubey
CloudXLab ID: aadityasomu1234382

The Solution Script uses Scala and Spark SQL to answer the 5 question asked in log parsing project.

Question 1 :

Write spark code to find out top 10 requested URLs along with a count of the number of times they have been requested (This information will help the company to find out most popular pages and how frequently they are accessed)

Answer 1 :

spark.sql("select url,count(*) as req_cnt from nasa_log where upper(url) like '%HTML%' group by url order by req_cnt desc LIMIT 10").show()

+--------------------+-------+
|                 url|req_cnt|
+--------------------+-------+
|           /ksc.html|  43687|
|/shuttle/missions...|  24606|
|/shuttle/missions...|  22453|
|/software/winvn/w...|  10345|
|/history/history....|  10134|
|/history/apollo/a...|   8985|
|/shuttle/countdow...|   7865|
|/history/apollo/a...|   7177|
|/shuttle/technolo...|   6517|
|/shuttle/missions...|   5264|
+--------------------+-------+


Question 2 :

Write spark code to find out the top five-time frame for high traffic (which day of the week or hour of the day receives peak traffic, this information will help the company to manage resources for handling peak traffic load)

Answer 2 :

spark.sql("select host,count(*) as req_cnt from nasa_log group by host order by req_cnt desc LIMIT 5").show()

+--------------------+-------+
|                host|req_cnt|
+--------------------+-------+
|  edams.ksc.nasa.gov|   6530|
|piweba4y.prodigy.com|   4846|
|        163.206.89.4|   4791|
|piweba5y.prodigy.com|   4607|
|piweba3y.prodigy.com|   4416|
+--------------------+-------+


Question 3 :

Write spark code to find out top 5 time frames of least traffic (which day of the week or hour of the day receives least traffic, this information will help the company to do production deployment in that time frame so that less number of users will be affected if something goes wrong during deployment)

Answer 3 :

spark.sql("select substr(timeStamp,1,14) as timeFrame,count(*) as req_cnt from nasa_log group by substr(timeStamp,1,14) order by req_cnt desc LIMIT 5").show()

+--------------+-------+
|     timeFrame|req_cnt|
+--------------+-------+
|31/Aug/1995:11|   6319|
|31/Aug/1995:10|   6283|
|31/Aug/1995:13|   5948|
|30/Aug/1995:15|   5919|
|31/Aug/1995:09|   5627|
+--------------+-------+


Question 4 :

Write Spark code to find out unique HTTP codes returned by the server along with count (this information is helpful for DevOps team to find out how many requests are failing so that appropriate action can be taken to fix the issue)

Answer 4 :

spark.sql("select httpCode,count(*) as req_cnt from nasa_log group by httpCode ").show()

+--------+-------+
|httpCode|req_cnt|
+--------+-------+
|     304| 134146|
|     404|  10056|
|     500|      3|
|     501|     27|
|     403|    171|
|     200|1398988|
|     302|  26444|
+--------+-------+


