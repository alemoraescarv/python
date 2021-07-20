```python
import sys
import json
import pandas as pd
dfglobal=pd.read_csv("test.csv")
#print(dfglobal)
filtered_df2  = pd.DataFrame([])
# s=sys.argv[1]
# ci=s[s.find("City=")+5:s.find("&State")]
# cs=s[s.find('State')+6:s.find("&Country")]
# ci=ci.replace('+','')
# cs=cs.replace('+','-')
# co=s[s.find("Country")+8:s.find("&ZipCode")]
# givenpostal=s[s.find("ZipCode")+8:s.find("&Radius")]
# radius=float(s[s.find("Radius")+8:])
ci="Barcelona"
co="Spain"
cs=""
givenpostal="08001"
radius=4.0
print(ci,co,cs,givenpostal,radius)
#print("hello1")
filtered_df2=pd.concat([filtered_df2,dfglobal[(dfglobal['Country'] == co) & (dfglobal['City'] == ci) &  (dfglobal['PostalCode'] == givenpostal)]])
#print(filtered_df2)
#filtered_df2['PostalCode']=filtered_df2['PostalCode'].apply(str)
a_dict=filtered_df2['Distance']
#print(a_dict)
result  = pd.DataFrame([])
resp=[]
resr=[]
for index, row in filtered_df2.iterrows():
    #print(row['Distance'])
    dictp=row['Distance']
    for key in dictp: 
        print(dictp[key])


result['PostalCode']=resp
result['City']=ci
result['Country']=co
result['Radius']=resr
result=result.reindex(["City","Country","PostalCode","Radius"],axis=1)
result.to_csv("distance.csv")    
```

    Barcelona Spain  08001 4.0

