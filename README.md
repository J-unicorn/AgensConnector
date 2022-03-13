# AgensConnector

### function info
---------------------------------------------
##### Program        : AgensConnector.py
##### Main function  : Connect AgensGraph and Pandas Dataframe
##### Creator        : Doohee Jung (Bitnine Graph Science)
##### Created date   : 2022.03.13

### Example
---------------------------------------------
### Connect Agensgraph Database

''' python

from AgensConnector import *

connect_info = {
   'host' : 'your_ip',
   'port' : 'your_port',
   'database' : 'database_name',
   'user' : 'user_name',
   'password' : 'password'
   }

agconn = AgensConnector(**connect_info)

''' 

OR

''' python
agconn = AgensConnector(your_ip, your_port, database , user , password)
'''

----------------------------------------------------
### Load graph

Split your dataframe into vertex & edge 

''' python 
v1,e1,v2=df.iloc[:,0:3],df.iloc[:,3:8],df.iloc[:,8:]
'''


Fill out your graph & label info


''' python 

param_dict = {}
param_dict['dfv1']=v1
param_dict['dfv2']=v2
param_dict['dfe1']=e1
param_dict['graph']='vio_test'
param_dict['vlabel1']='vt_vio'
param_dict['vlabel2']='vt_vio'
param_dict['elabel']='edg_viocng'
param_dict['key1']='vio_nm'
param_dict['key2']='vio_nm'


agconn.load_graph(**param_dict)

''' 
