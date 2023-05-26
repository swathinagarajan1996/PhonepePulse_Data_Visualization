![image](https://github.com/swathinagarajan1996/PhonepePulse_Data_Visualization/assets/127007232/fab1700a-8e35-4334-9bb3-aea43080bc1e)

***Data Visualization and Exploration
A User-Friendly Tool Using Streamlit and Plotly***

The Phonepe pulse Github repository contains a large amount of data related to
various metrics and statistics. The goal is to extract this data and process it to obtain
insights and information that can be visualized in a user-friendly manner.

**Libraries/Modules needed required**
1. Plotly - (To plot and visualize the data)
2. Pandas - (To Create a DataFrame with the scraped data)
3. sqlite3 server- (To store and retrieve the data)
4. Streamlit - (To Create Graphical user Interface)
5. json - (To load the json files)
6. git.repo.base - (To clone the GitHub repository
7. PIL - The Python Imaging Library, used for opening, manipulating, and saving many different image file formats.


**Approach**

**Step 1: Cloning Github Repository**

Clone the Github using scripting to fetch the data from the Phonepe pulse Github repository and store it in a suitable format such as JSON. Use the below link to clone the phonepe github repository into your local drive.
  
  "!git clone https://github.com/PhonePe/pulse.git  "
  
**Step 2: Importing the Libraries:**
    import pandas as pd
    import sqlite3 as sql
    import streamlit as st
    import plotly.express as px
    import os
    import json
    from PIL import Image

**Step 3:Data transformation:**
After cloning, in this step the JSON files that are available in the folders are converted into the readeable and understandable DataFrame format by using the for loop and iterating file by file and then finally the DataFrame is created. In order to perform this step used os, json and pandas packages. And finally converted the dataframe into CSV file and storing in the local drive.

path1='Path of the JSON files'

Agg_Trans_list=os.listdir(path1)
Agg_Trans_list


columns1 = {'State': [], 'Year': [], 'Quarter': [], 'Transaction_Type': [], 'Transaction_Count': [],
            'Transaction_Amount': []}

for state in Agg_Trans_list:
    cur_state=path1+state+'/'
    #print(cur_state)
    Agg_yr_list=os.listdir(cur_state)
    
    for year in Agg_yr_list:
        cur_year= cur_state+year+'/' 
        Agg_file_list=os.listdir(cur_year)
        #print(cur_year)
        
        for file in Agg_file_list:
            cur_file=cur_year+file
            Data=open(cur_file,'r')
            toload_Data=json.load(Data)
            #print(toload_Data)
            
            for z in toload_Data['data']['transactionData']:
                Name=z['name']
                count=z['paymentInstruments'][0]['count']
                amount=z['paymentInstruments'][0]['amount']
                
                columns1['Transaction_Type'].append(Name)
                columns1['Transaction_Count'].append(count)
                columns1['Transaction_Amount'].append(amount)
                columns1['State'].append(state)
                columns1['Year'].append(year)
                columns1['Quarter'].append(int(file.strip('.json')))
                
Agg_Trans_Table1=pd.DataFrame(columns1)
Agg_Trans_Table1

Converting the dataframe into csv file:
df.to_csv('filename.csv',index=False)


**Step 4: Database insertion**
To insert the dataframe into sqlite3, created a new database and tables using "sqlite3" library in Python  and inserted the transformed data using SQL commands.

Creating the connection between python and sqlite3
conn=sql.connect('Pulse.db')
mycursor=conn.cursor()

**Creating tables **

create_Table6='''CREATE TABLE Top_User( State varchar(100), 
                 Year int,
                 Quarter int, 
                 Pincode int, 
                 No_of_Regusers int); '''
mycursor.execute(create_Table6)

**Inserting values into tables **

for i,row in top_users_Label6.iterrows():
    mysql='INSERT INTO Top_User (State,Year,Quarter,Pincode,No_of_Regusers)VALUES (?,?,?,?,?)
    val=(row['State'],row['Year'],row['Quarter'],row['Pincode'],row['No_of_Regusers'])
    mycursor.execute(mysql,val)
conn.commit()


**Step 5:Dashboard creation**
To create colourful and insightful dashboard I've used Plotly libraries in Python to create an interactive and visually appealing dashboard. Plotly's built-in Pie, Bar, Geo map functions are used to display the data on a charts and map and Streamlit is used to create a user-friendly interface with multiple dropdown options for users to select different facts and figures to display.

**Step 6: Deployment**
Once created the dashboard, we can test it thoroughly and deploy it, making it accessible to users.
