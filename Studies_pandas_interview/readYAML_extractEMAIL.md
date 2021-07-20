```python
import yaml
import re
import pandas as pd
import csv
#a_yaml_file = open("pol.yaml")
#docs_yaml = yaml.load_all(a_yaml_file, Loader=yaml.FullLoader)

#for doc in docs_yaml:
#    print(doc.get("members"))
       # print(user)
#    print("\n")

#print(parsed_yaml_file.get("users"))

final_list=[]

def yaml_as_python(val):
    """Convert YAML to dict"""
    try:
        return yaml.load_all(val,Loader=yaml.FullLoader)
    except yaml.YAMLError as exc:
        return exc

with open('users.yaml','r') as input_file:
    results = yaml.load_all(input_file,Loader=yaml.FullLoader)
    #= yaml_as_python(input_file)
    print(results)
    for value in results:
        #for policy in value[policy]:
        #print(value['policy']['bindings'][0]['members'])
        print("inicio\n\n")
        try:
            mydict=value['policy']['bindings'][0]['members']
            mydict=sorted(mydict)
            r=re.compile(r'.+\@(abc.com)')
            my_newlist=['yourgroup@email.com,'+email.lstrip("user:")+',USER,MEMBER' for email in mydict if re.match(r,email)]
            final_list.extend(my_newlist)
            
                #print(final_list)
                #for policy, bindings in value.items():
                #    for member in bindings['members']:
                #        print(member)
        except TypeError:
            print("tupe erorr")


print("\n\n\n\n\nFINAL LIST\n")
print(final_list)

df = pd.DataFrame(final_list)
#print (df)

header=['Group Email [Required]','Member Email','Member Type','Member Role']

with open('list.csv','w') as out:
    csv_out = csv.writer(out)
    csv_out.writerow(header)
    for row in final_list:
        csv_out.writerow(row)


```

    <generator object load_all at 0x7f986f35aed0>
    inicio
    
    
    inicio
    
    
    inicio
    
    
    inicio
    
    
    inicio
    
    
    tupe erorr
    
    
    
    
    
    FINAL LIST
    
    ['yourgroup@email.com,Sanaa.Keller@abc.com,USER,MEMBER', 'yourgroup@email.com,adam.skill@abc.com,USER,MEMBER', 'yourgroup@email.com,albert.withmore@abc.com,USER,MEMBER', 'yourgroup@email.com,alison.mcknight@abc.com,USER,MEMBER', 'yourgroup@email.com,andre.soretti@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.born@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.hill@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.ives@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.windridge@abc.com,USER,MEMBER', 'yourgroup@email.com,angela.hammond@abc.com,USER,MEMBER', 'yourgroup@email.com,anil.patel@abc.com,USER,MEMBER', 'yourgroup@email.com,anna.lynch@abc.com,USER,MEMBER', 'yourgroup@email.com,ben.carlson@abc.com,USER,MEMBER', 'yourgroup@email.com,lisabeth.morrison@abc.com,USER,MEMBER', 'yourgroup@email.com,Sanaa.Keller@abc.com,USER,MEMBER', 'yourgroup@email.com,adam.skill@abc.com,USER,MEMBER', 'yourgroup@email.com,albert.withmore@abc.com,USER,MEMBER', 'yourgroup@email.com,alison.mcknight@abc.com,USER,MEMBER', 'yourgroup@email.com,andre.soretti@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.born@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.hill@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.ives@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.windridge@abc.com,USER,MEMBER', 'yourgroup@email.com,angela.hammond@abc.com,USER,MEMBER', 'yourgroup@email.com,anil.patel@abc.com,USER,MEMBER', 'yourgroup@email.com,anna.lynch@abc.com,USER,MEMBER', 'yourgroup@email.com,ben.carlson@abc.com,USER,MEMBER', 'yourgroup@email.com,lisabeth.morrison@abc.com,USER,MEMBER', 'yourgroup@email.com,Sanaa.Keller@abc.com,USER,MEMBER', 'yourgroup@email.com,adam.skill@abc.com,USER,MEMBER', 'yourgroup@email.com,albert.withmore@abc.com,USER,MEMBER', 'yourgroup@email.com,alison.mcknight@abc.com,USER,MEMBER', 'yourgroup@email.com,andre.soretti@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.born@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.hill@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.ives@abc.com,USER,MEMBER', 'yourgroup@email.com,andrew.windridge@abc.com,USER,MEMBER', 'yourgroup@email.com,angela.hammond@abc.com,USER,MEMBER', 'yourgroup@email.com,anil.patel@abc.com,USER,MEMBER', 'yourgroup@email.com,anna.lynch@abc.com,USER,MEMBER', 'yourgroup@email.com,ben.carlson@abc.com,USER,MEMBER', 'yourgroup@email.com,lisabeth.morrison@abc.com,USER,MEMBER', 'yourgroup@email.com,brian.king@abc.com,USER,MEMBER']



    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-14-8aeb2c5ba215> in <module>
         51 #print (df)
         52 
    ---> 53 df.to_csv(header=['Group Email [Required]','Member Email','Member Type','Member Role'], index=True)
         54 


    /opt/conda/lib/python3.7/site-packages/pandas/core/generic.py in to_csv(self, path_or_buf, sep, na_rep, float_format, columns, header, index, index_label, mode, encoding, compression, quoting, quotechar, line_terminator, chunksize, date_format, doublequote, escapechar, decimal)
       3202             decimal=decimal,
       3203         )
    -> 3204         formatter.save()
       3205 
       3206         if path_or_buf is None:


    /opt/conda/lib/python3.7/site-packages/pandas/io/formats/csvs.py in save(self)
        202             )
        203 
    --> 204             self._save()
        205 
        206         finally:


    /opt/conda/lib/python3.7/site-packages/pandas/io/formats/csvs.py in _save(self)
        307 
        308     def _save(self) -> None:
    --> 309         self._save_header()
        310 
        311         nrows = len(self.data_index)


    /opt/conda/lib/python3.7/site-packages/pandas/io/formats/csvs.py in _save_header(self)
        241             if len(header) != len(cols):
        242                 raise ValueError(
    --> 243                     f"Writing {len(cols)} cols but got {len(header)} aliases"
        244                 )
        245             else:


    ValueError: Writing 1 cols but got 4 aliases

