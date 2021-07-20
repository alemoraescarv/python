```python
import yaml
import re
import pandas as pd
import csv

#declaring the list which will contain all the user's emails from the policy biding yaml
final_list=[]

def yaml_as_python(val):
    """Convert YAML to dict"""
    try:
        return yaml.load_all(val,Loader=yaml.FullLoader)
    except yaml.YAMLError as exc:
        return exc

with open('users.yaml','r') as input_file, open('emails_to_remove_policies.csv', 'w') as emails_to_remove_policies:
    results = yaml.load_all(input_file,Loader=yaml.FullLoader)

    #print(results)
    for value in results:

        try:
            mydict=value['policy']['bindings'][0]['members']
            mydict=sorted(mydict)
            r=re.compile(r'.+\@(abc.com)')
            my_newlist=[email.lstrip("user:") for email in mydict if re.match(r,email)]
            
            final_list.extend(my_newlist)
            #final_list.writerow(email_list)

            
        except TypeError:
            #print("type erorr")
            continue
            
    #writting the csv with the list of emails which will be removed from the policies        
    wr = csv.writer(emails_to_remove_policies, quoting=csv.QUOTE_NONE, delimiter = '\n')
    wr.writerow(final_list)



#CSV file example from documentation
#Header: Group Email [Required],Member Email,Member Type,Member Role
#Entry: yourgroup@email.com, membername@email.com,USER,MEMBER 


df = pd.DataFrame(final_list)
df2 = pd.DataFrame(final_list, columns=['Member Email'])
df2 = df2.assign(GroupEmail='yourgroup@email.com').assign(MemberType='USER').assign(MemberRole= 'MEMBER')
df2 = df2.reindex(columns=['GroupEmail','Member Email','MemberType','MemberRole'])


df2 = df2.rename(columns={'GroupEmail': 'Group Email [Required]', 'MemberType': 'Member Email', 
                          'MemberRole': 'Member Role' })
print (df2)

#list of emails to add in the google group
df2.to_csv('emails_to_add.csv',index=False)




```

       Group Email [Required]               Member Email Member Email Member Role
    0     yourgroup@email.com       Sanaa.Keller@abc.com         USER      MEMBER
    1     yourgroup@email.com         adam.skill@abc.com         USER      MEMBER
    2     yourgroup@email.com    albert.withmore@abc.com         USER      MEMBER
    3     yourgroup@email.com    alison.mcknight@abc.com         USER      MEMBER
    4     yourgroup@email.com      andre.soretti@abc.com         USER      MEMBER
    5     yourgroup@email.com        andrew.born@abc.com         USER      MEMBER
    6     yourgroup@email.com        andrew.hill@abc.com         USER      MEMBER
    7     yourgroup@email.com        andrew.ives@abc.com         USER      MEMBER
    8     yourgroup@email.com   andrew.windridge@abc.com         USER      MEMBER
    9     yourgroup@email.com     angela.hammond@abc.com         USER      MEMBER
    10    yourgroup@email.com         anil.patel@abc.com         USER      MEMBER
    11    yourgroup@email.com         anna.lynch@abc.com         USER      MEMBER
    12    yourgroup@email.com        ben.carlson@abc.com         USER      MEMBER
    13    yourgroup@email.com  lisabeth.morrison@abc.com         USER      MEMBER
    14    yourgroup@email.com       Sanaa.Keller@abc.com         USER      MEMBER
    15    yourgroup@email.com         adam.skill@abc.com         USER      MEMBER
    16    yourgroup@email.com    albert.withmore@abc.com         USER      MEMBER
    17    yourgroup@email.com    alison.mcknight@abc.com         USER      MEMBER
    18    yourgroup@email.com      andre.soretti@abc.com         USER      MEMBER
    19    yourgroup@email.com        andrew.born@abc.com         USER      MEMBER
    20    yourgroup@email.com        andrew.hill@abc.com         USER      MEMBER
    21    yourgroup@email.com        andrew.ives@abc.com         USER      MEMBER
    22    yourgroup@email.com   andrew.windridge@abc.com         USER      MEMBER
    23    yourgroup@email.com     angela.hammond@abc.com         USER      MEMBER
    24    yourgroup@email.com         anil.patel@abc.com         USER      MEMBER
    25    yourgroup@email.com         anna.lynch@abc.com         USER      MEMBER
    26    yourgroup@email.com        ben.carlson@abc.com         USER      MEMBER
    27    yourgroup@email.com  lisabeth.morrison@abc.com         USER      MEMBER
    28    yourgroup@email.com       Sanaa.Keller@abc.com         USER      MEMBER
    29    yourgroup@email.com         adam.skill@abc.com         USER      MEMBER
    30    yourgroup@email.com    albert.withmore@abc.com         USER      MEMBER
    31    yourgroup@email.com    alison.mcknight@abc.com         USER      MEMBER
    32    yourgroup@email.com      andre.soretti@abc.com         USER      MEMBER
    33    yourgroup@email.com        andrew.born@abc.com         USER      MEMBER
    34    yourgroup@email.com        andrew.hill@abc.com         USER      MEMBER
    35    yourgroup@email.com        andrew.ives@abc.com         USER      MEMBER
    36    yourgroup@email.com   andrew.windridge@abc.com         USER      MEMBER
    37    yourgroup@email.com     angela.hammond@abc.com         USER      MEMBER
    38    yourgroup@email.com         anil.patel@abc.com         USER      MEMBER
    39    yourgroup@email.com         anna.lynch@abc.com         USER      MEMBER
    40    yourgroup@email.com        ben.carlson@abc.com         USER      MEMBER
    41    yourgroup@email.com  lisabeth.morrison@abc.com         USER      MEMBER
    42    yourgroup@email.com         brian.king@abc.com         USER      MEMBER



```python
import yaml
import re
import pandas as pd

#declaring the list which will contain all the user's emails from the policy biding yaml
final_list=['Sanaa.Keller@abc.com', 'adam.skill@abc.com', 'albert.withmore@abc.com', 'alison.mcknight@abc.com']

def yaml_as_python(val):
    """Convert YAML to dict"""
    try:
        return yaml.load_all(val,Loader=yaml.FullLoader)
    except yaml.YAMLError as exc:
        return exc

    
with open('users.yaml','r') as input_file, open('new_users12.yaml', 'w') as newfile:
    results = yaml.load_all(input_file,Loader=yaml.FullLoader)
    print(results)
    newfile.write('---\n')
    for value in results:
        try:
            print('here')
            yaml.dump(value, newfile, default_flow_style=False)
            #newfile.write(value)
            mydict=value['policy']['bindings'][0]['members']
            mydict=sorted(mydict)
            #r=re.compile(r'.+\@(abc.com)')
            print('here2')
            for email in mydict:
                if email not in final_list:
                    #yaml.dump(value,newfile)
                    #yaml.dump(value, newfile, default_flow_style=False)
                    print('email')
        except TypeError:
            print("type erorr")
            continue

```

    <generator object load_all at 0x7f3cd83237d0>
    here
    here2
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    here
    here2
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    here
    here2
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    email
    here
    here2
    email
    here
    type erorr



```python
import subprocess
subprocess.Popen("gcloud projects get-iam-policy test-proj-261014 --format yaml > policy_bash.yaml ")
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-88-706b419956e3> in <module>
          1 import subprocess
    ----> 2 subprocess.Popen("ls ")
    

    /opt/conda/lib/python3.7/subprocess.py in __init__(self, args, bufsize, executable, stdin, stdout, stderr, preexec_fn, close_fds, shell, cwd, env, universal_newlines, startupinfo, creationflags, restore_signals, start_new_session, pass_fds, encoding, errors, text)
        798                                 c2pread, c2pwrite,
        799                                 errread, errwrite,
    --> 800                                 restore_signals, start_new_session)
        801         except:
        802             # Cleanup if the child failed starting.


    /opt/conda/lib/python3.7/subprocess.py in _execute_child(self, args, executable, preexec_fn, close_fds, pass_fds, cwd, env, startupinfo, creationflags, shell, p2cread, p2cwrite, c2pread, c2pwrite, errread, errwrite, restore_signals, start_new_session)
       1549                         if errno_num == errno.ENOENT:
       1550                             err_msg += ': ' + repr(err_filename)
    -> 1551                     raise child_exception_type(errno_num, err_msg, err_filename)
       1552                 raise child_exception_type(err_msg)
       1553 


    FileNotFoundError: [Errno 2] No such file or directory: 'ls ': 'ls '

