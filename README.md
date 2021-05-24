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
