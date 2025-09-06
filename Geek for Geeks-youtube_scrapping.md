```python
!pip install webdriver-manager
```

    Requirement already satisfied: webdriver-manager in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (4.0.2)
    Requirement already satisfied: requests in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from webdriver-manager) (2.32.4)
    Requirement already satisfied: python-dotenv in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from webdriver-manager) (1.1.1)
    Requirement already satisfied: packaging in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from webdriver-manager) (25.0)
    Requirement already satisfied: charset_normalizer<4,>=2 in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from requests->webdriver-manager) (3.4.2)
    Requirement already satisfied: idna<4,>=2.5 in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from requests->webdriver-manager) (3.10)
    Requirement already satisfied: urllib3<3,>=1.21.1 in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from requests->webdriver-manager) (2.5.0)
    Requirement already satisfied: certifi>=2017.4.17 in c:\users\dell.desktop-695k4nf\appdata\local\programs\python\python313\lib\site-packages (from requests->webdriver-manager) (2025.7.14)
    

    
    [notice] A new release of pip is available: 25.1.1 -> 25.2
    [notice] To update, run: python.exe -m pip install --upgrade pip
    


```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

# Wrap the path with Service
service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)

```


```python
import pandas as pd
```


```python
driver.get('https://www.youtube.com/@GeeksforGeeksVideos/videos')
```


```python
from bs4 import BeautifulSoup
```


```python
soup=BeautifulSoup(driver.page_source, 'html.parser')
```


```python
sp = soup.find_all('ytd-rich-item-renderer')
```


```python
sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').text
```




    'What is Generative AI? | Generative AI Roadmap For Absolute Beginners 🔥'




```python
title         = sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').text
video_link    = sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').get('href')
views         = sp[0].find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[0].text
date_time     = sp[0].find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[1].text
```


```python
title
```




    'What is Generative AI? | Generative AI Roadmap For Absolute Beginners 🔥'




```python
video_link 
```




    '/watch?v=hbRgHyHNVag'




```python
views
```




    '753 views'




```python
date_time
```




    '21 hours ago'




```python
data = []

for sp in soup.find_all('ytd-rich-item-renderer'):
    title         = sp.find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').text
    video_link    = sp.find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').get('href')

    try:
        views         = sp.find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[0].text
    except:
        views = None 
    try:
        date_time     = sp.find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[1].text
    except:
        date_time =None 

    data.append([title, views,date_time,video_link])
```


```python
df= pd.DataFrame(data, columns = ['title', 'views', 'date_time', 'video_link'])
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>views</th>
      <th>date_time</th>
      <th>video_link</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>What is Generative AI? | Generative AI Roadmap...</td>
      <td>753 views</td>
      <td>21 hours ago</td>
      <td>/watch?v=hbRgHyHNVag</td>
    </tr>
    <tr>
      <th>1</th>
      <td>I reviewed 100+ resumes so that you can avoid ...</td>
      <td>2.6K views</td>
      <td>4 days ago</td>
      <td>/watch?v=tnqPUh0YuBE</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DSA In Java | Recursion Part 1 | Java in One S...</td>
      <td>4K views</td>
      <td>5 days ago</td>
      <td>/watch?v=UTutbbpOLgE</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Communication and Interpersonal Skills Explain...</td>
      <td>1.5K views</td>
      <td>6 days ago</td>
      <td>/watch?v=dn60Buj8tbA&amp;pp=0gcJCcYJAYcqIYzv</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Why you should Learn ML in 2025? | The Complet...</td>
      <td>2.3K views</td>
      <td>6 days ago</td>
      <td>/watch?v=gmxUueRo97U</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Top MCA Colleges in India with Highest Placeme...</td>
      <td>6.8K views</td>
      <td>8 days ago</td>
      <td>/watch?v=bvGvRoAeLbg</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Top 5 ways to get rejected in Interviews! ❌</td>
      <td>4K views</td>
      <td>9 days ago</td>
      <td>/watch?v=LmjCc5ynAL0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Why are you even learning coding when AI does ...</td>
      <td>60K views</td>
      <td>10 days ago</td>
      <td>/watch?v=WNPS6wVAKDw&amp;pp=0gcJCcYJAYcqIYzv</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Learn Data Science by Doing: 21 Projects in 21...</td>
      <td>3.6K views</td>
      <td>11 days ago</td>
      <td>/watch?v=YBMv3CtzHbg</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NIMCET Preparation | NIMCET Logarithm PYQ | Lo...</td>
      <td>1.3K views</td>
      <td>11 days ago</td>
      <td>/watch?v=ATq9HSG2OXQ</td>
    </tr>
    <tr>
      <th>10</th>
      <td>DSA In Java | 2D Arrays | Java in One Shot | 2...</td>
      <td>5.3K views</td>
      <td>12 days ago</td>
      <td>/watch?v=ohIucTEqkVk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>5 Levels to Master Data Science | How to Maste...</td>
      <td>1.4K views</td>
      <td>13 days ago</td>
      <td>/watch?v=CKhNCF623eQ</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Top 15 VS Code Extensions to Boost your Prepar...</td>
      <td>4.6K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=DPy0-aylwRA</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Nation SkillUp Free Courses | Big Updates Rele...</td>
      <td>13K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=T2_ivhrauzk</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NIMCET Preparation | NIMCET PYQ | Quadratic Eq...</td>
      <td>2.6K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=0PJipN9EhA0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Beginner’s Guide to Soft Skills: Boost Your Ca...</td>
      <td>3.1K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=aRUvhkkcLAQ</td>
    </tr>
    <tr>
      <th>16</th>
      <td>DSA In Java | Strings | Java in One Shot | Str...</td>
      <td>7.3K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=bIyit0VaJp8</td>
    </tr>
    <tr>
      <th>17</th>
      <td>NIMCET 2026 Preparation | NIMCET PYQ | NIMCET ...</td>
      <td>1.9K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=_lUDvHwi7l0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>DSA In Java | Binary Search | Java in One Shot...</td>
      <td>7.1K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=GeO3HQNnpoE</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0 to AI Engineer Roadmap! 🚀</td>
      <td>45K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=YWV_ly5qSKs</td>
    </tr>
    <tr>
      <th>20</th>
      <td>DSA Roadmap | DSA Preparation Strategy | Big N...</td>
      <td>11K views</td>
      <td>2 weeks ago</td>
      <td>/watch?v=VwCG3slCNc4&amp;pp=0gcJCcYJAYcqIYzv</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Big New For Gen AI &amp; Data Science | Big Surpri...</td>
      <td>1.3K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=QC9JlMqiW84</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Big Surprise For NIMCET 2026 Exam | NIMCET 202...</td>
      <td>2.9K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=sZZr4ZIogWg</td>
    </tr>
    <tr>
      <th>23</th>
      <td>DSA In Java | Bubble, Selection &amp; Insertion So...</td>
      <td>5.5K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=Aa5gV3o7Rno</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Why GPT-5 Might Be a Game-Changer for Coders 🚀...</td>
      <td>1.7K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=YP6LdlkAtrI&amp;pp=0gcJCcYJAYcqIYzv</td>
    </tr>
    <tr>
      <th>25</th>
      <td>DSA In Java | Time &amp; Space Complexity | Java i...</td>
      <td>7K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=s1OHQ1kNHsM</td>
    </tr>
    <tr>
      <th>26</th>
      <td>DSA In Java | Arrays | Java in One Shot | Arra...</td>
      <td>24K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=_MwptrixhCs</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Zero to Job Ready | 2025 Front-End Development...</td>
      <td>13K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=YOqXO2oHU0k</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Job -a -Thon | How To apply ? | What is Job -a...</td>
      <td>4.4K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=5Z3hXxIGn-0&amp;pp=0gcJCcYJAYcqIYzv</td>
    </tr>
    <tr>
      <th>29</th>
      <td>DSA In Java | Methods | Java in One Shot | Met...</td>
      <td>6.4K views</td>
      <td>3 weeks ago</td>
      <td>/watch?v=NDO_hnHrsTk</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.isnull().sum()
```




    title         0
    views         0
    date_time     0
    video_link    0
    dtype: int64




```python

```
