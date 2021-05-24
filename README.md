# pyspark_learn

## getting_started
https://spark.apache.org/docs/latest/api/python/getting_started/quickstart.html#Working-with-SQL

## java version

https://www.oracle.com/in/java/technologies/javase/javase-jdk8-downloads.html#license-lightbox
## environment settings
```python

os.environ['SPARK_HOME'] = r'D:\spark\spark-3.1.1-bin-hadoop2.7'
os.environ['HADOOP_HOME'] = r'D:\spark\spark-3.1.1-bin-hadoop2.7'
os.environ['PYSPARK_DRIVER_PYTHON'] = 'jupyter'
os.environ['PYSPARK_DRIVER_PYTHON_OPTS'] = 'notebook'
os.environ['JAVA_HOME'] ='C:\Java\jdk1.8.0_291'  # no spaces allowd 

Path = 'D:\spark\spark-3.1.1-bin-hadoop2.7\bin'
```
## in anaonda promt
```cmd
pip install findspark

pin install pyspark

```

## in note book
```
import findspark
findspark.init()

import pyspark # only run after findspark.init()
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

df = spark.sql('''select 'spark' as hello ''')
df.show()
```

## connect mysql using jdbc
```python
from pyspark.sqlimportSQLContext

sqlContext = SQLContext(sc)
dataframe_mysql = sqlContext.read.format("jdbc").options(url="jdbc:mysql://127.0.0.1:3306/spark_db", driver="com.mysql.jdbc.Driver", dbtable="spark_table", user="root", password="root").load()
dataframe_mysql.show()
```

## use pyspark to deal data
```
import time
import pyspark # only run after findspark.init()
from pyspark.sql import SparkSession
from datetime import datetime, date
import pandas as pd
from pyspark.sql import Row
import findspark
findspark.init()
spark = SparkSession.builder.getOrCreate()

pandas_df = pd.DataFrame({
    'a': [1, 2, 3],
    'b': [2., 3., 4.],
    'c': ['string1', 'string2', 'string3'],
    'd': [date(2000, 1, 1), date(2000, 2, 1), date(2000, 3, 1)],
    'e': [datetime(2000, 1, 1, 12, 0), datetime(2000, 1, 2, 12, 0), datetime(2000, 1, 3, 12, 0)]
})

df = spark.createDataFrame(pandas_df)
#df.show()


spark_sql = """
SELECT 
* ,
ROW_NUMBER() OVER (ORDER BY a) as rn,
sum(b) over (order by a) as culmu_sum  
from tableA"""

df.createOrReplaceTempView("tableA")

df2 = spark.sql(spark_sql)

# df2.show()
pandas_df2 = df2.toPandas()
# pandas_df2.head(5)
print(pandas_df2.head())
```
