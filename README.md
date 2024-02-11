# web-scraping-mini-project

CODE


from bs4 import BeautifulSoup
import requests


url= 'https://en.wikipedia.org/wiki/List_of_Indian_states_and_union_territories_by_GDP_per_capita'

page =requests.get(url)

soup= BeautifulSoup(page.text,'html')

table= soup.find_all('table')[1]

print(table)

titles= table.find_all('th')

table_titles= [title.text.strip() for title in titles]

print(table_titles)

import pandas as pd

df = pd.DataFrame(columns = table_titles)

col_data =table.find_all('tr')

for row in col_data[1:]:

    row_data= row.find_all('td')
    
    individual_row_data = [data.text for data in row_data]
    
    length =len(df)
    
    df.loc[length]= individual_row_data
    
df

df.to_csv("states and gdp.csv")

