# AgensConnector
---------------------------------------------
### function info

##### Program        : AgensConnector.py
##### Main function  : Connect AgensGraph and Pandas Dataframe
##### Creator        : Doohee Jung (Bitnine Graph Science)
##### Created date   : 2022.03.13
---------------------------------------------
### Connect Agensgraph Database

``` python

from AgensConnector import *

connect_info = {
   'host' : 'your_ip',
   'port' : 'your_port',
   'database' : 'database_name',
   'user' : 'user_name',
   'password' : 'password'
   }

agconn = AgensConnector(**connect_info)

```

OR

``` python
agconn = AgensConnector(your_ip, your_port, database , user , password)
```

----------------------------------------------------
### Load graph

Split your dataframe into vertex & edge 

``` python 
v1,e1,v2=df.iloc[:,0:3],df.iloc[:,3:8],df.iloc[:,8:]
```


Set your graph & label info 


``` python 

param_dict = {}
param_dict['dfv1']=v1
param_dict['dfv2']=v2
param_dict['dfe1']=e1
param_dict['graph']='your_graph'
param_dict['vlabel1']='vertex label1'
param_dict['vlabel2']='vertex label2'
param_dict['elabel']='edge label'
param_dict['key1']='vertex key1'
param_dict['key2']='vertex key2'
``` 

Execute load graph

``` python
agconn.load_graph(**param_dict)
``` 


----------------------------------------------------
### Create/Insert dataframe into Table

Create table 

``` python
agconn.pandas_exe(df,'test_table',exists='replace')
```
Insert table

``` python
agconn.pandas_exe(df,'test_table',exists='append')
```

----------------------------------------------------
### Query Graph/Table Data

Query table data

``` python
sql = 'select * from test_table'
sql_tbl = 'test_table'

df_sql = agconn.query_pandas(sql)
df_tbl = agconn.query_pandas(sql_tbl, table=True)

``` 
Compare df_sql with df_tbl

Query Graph data

``` python
cypher = 'match(a)-[r]->(b) return a,r,b'
cypher_val = 'match(a)-[r]->(b) return a.property1,a.property2,r.property1,r.property2,b.property1,b.property2'

# Property is labels subdata

df_cypher = agconn.query_pandas(cypher, graph='your graph')
df_cypher_val = agconn.query_pandas(cypher_val, graph='your graph')

``` 
Compare df_cypher with df_cypher_val

----------------------------------------------------
### Execute query into Database 

Execute query

``` python


drop_sql = 'drop graph 'your_graph' cascade;'

# drop your graph schema

agconn.query_exe(drop_sql)

agconn.set_graph('your_graph')

# get error: graph "your graph" does not exist.
``` 


