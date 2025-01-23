
import numpy as np
import pandas as pd
import requests
from bs4 import BeautifulSoup
URL='https://timely-sunshine-e821b3.netlify.app/'
page=requests.get(URL)
page.status_code
htmlcode=page.text
soup=BeautifulSoup(htmlcode)
htmlcode
content=soup.find('div',attrs={'class':'name'})
text=content.text.strip()
print(text)
content=soup.find('div',attrs={'class':'price'})
text=content.text.strip()
print(text)
content = soup.find('div', attrs={'class' : 'main'})
text=content.text
r1 = text.split("\n")
#print(r1)
r2 = []
for i in r1:
  if i != '' and i != '\r':
    r2.append(i)
#print(r2)
r3 = []
for i in r2:
  k = i.strip()
  r3.append(k)
#print(r3)
r4 = []
for i in r3:
  if i != '':
    r4.append(i)
#print(r4)
names = []
prices = []
for i in range(0,len(r4),2):
  names.append(r4[i])
  prices.append(r4[i+1])
print(names)
print(prices)
df = pd.DataFrame({"product_name":names,"product_price":prices})
df.to_csv("sample.csv",header=True,index=False)
from google.colab import files
files.download('sample.csv')
