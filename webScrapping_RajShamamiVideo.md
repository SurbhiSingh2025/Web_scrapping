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
driver.get("https://www.youtube.com/@rajshamani/videos")

```


```python
from bs4 import BeautifulSoup
```


```python
soup = BeautifulSoup(driver.page_source, 'html.parser')
```


```python
sp = soup.find_all('ytd-rich-grid-renderer')
```

#Scrapping the title


```python
sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').text
```




    'How to Use ChatGPT for Investment & Wealth Building – Wint Wealth | FO404 Raj Shamani'




```python
title = sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').text
video_link = sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').get('href') 
views = sp[0].find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[0].text
date_time= sp[0].find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[1].text
```


```python
sp[0].find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').get('href')
```




    '/watch?v=8OgwKBiDu5w'




```python
sp[0].find_all('span')
```




    [<span class="ytIconWrapperHost" style="width: 24px; height: 24px;"><span class="yt-icon-shape"></span></span>,
     <span class="yt-icon-shape"></span>,
     <span class="ytIconWrapperHost" style="width: 24px; height: 24px;"><span class="yt-icon-shape"></span></span>,
     <span class="yt-icon-shape"></span>,
     <span aria-label="1 hour, 13 minutes, 35 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:13:35
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span aria-label="1 hour, 13 minutes, 35 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:13:35
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">123K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">16 hours ago</span>,
     <span aria-label="1 hour, 45 minutes, 10 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:45:10
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span aria-label="1 hour, 45 minutes, 10 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:45:10
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">967K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2 days ago</span>,
     <span aria-label="55 minutes, 38 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         55:38
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span aria-label="55 minutes, 38 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         55:38
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">299K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">4 days ago</span>,
     <span aria-label="1 hour, 17 minutes, 57 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:17:57
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span aria-label="1 hour, 17 minutes, 57 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:17:57
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.6M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">6 days ago</span>,
     <span aria-label="1 hour, 19 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:00:19
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">165K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">8 days ago</span>,
     <span aria-label="1 hour, 25 minutes, 37 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:25:37
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">96K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">10 days ago</span>,
     <span aria-label="1 hour, 17 minutes, 24 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:17:24
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">3.1M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">12 days ago</span>,
     <span aria-label="1 hour, 27 minutes, 19 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:27:19
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2 weeks ago</span>,
     <span aria-label="1 hour, 21 minutes, 38 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:21:38
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">4.5M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2 weeks ago</span>,
     <span aria-label="1 hour, 35 minutes, 8 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:35:08
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">406K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2 weeks ago</span>,
     <span aria-label="1 hour, 3 minutes, 31 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:03:31
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">632K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">3 weeks ago</span>,
     <span aria-label="51 minutes, 2 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         51:02
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">182K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">3 weeks ago</span>,
     <span aria-label="1 hour, 5 minutes, 18 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:05:18
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">880K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">3 weeks ago</span>,
     <span aria-label="1 hour, 35 minutes, 38 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:35:38
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.4M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">4 weeks ago</span>,
     <span aria-label="1 hour, 4 minutes, 59 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:04:59
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">4 weeks ago</span>,
     <span aria-label="3 hours, 32 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         3:00:32
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.4M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="2 hours, 16 minutes, 30 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         2:16:30
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">4.1M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 19 minutes, 31 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:19:31
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">967K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 16 minutes, 54 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:16:54
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">610K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 43 minutes, 25 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:43:25
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2.1M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 20 minutes, 52 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:20:52
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.5M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="58 minutes, 51 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         58:51
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">493K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 41 minutes, 42 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:41:42
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.5M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 10 minutes, 46 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:10:46
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">348K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 32 minutes, 29 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:32:29
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">312K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 16 minutes, 14 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:16:14
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.9M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 39 minutes, 7 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:39:07
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1.2M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="58 minutes, 26 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         58:26
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">155K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">1 month ago</span>,
     <span aria-label="1 hour, 22 minutes, 55 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:22:55
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2.2M views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2 months ago</span>,
     <span aria-label="1 hour, 16 minutes, 43 seconds" class="style-scope ytd-thumbnail-overlay-time-status-renderer" id="text">
         1:16:43
       </span>,
     <span class="style-scope ytd-thumbnail-overlay-now-playing-renderer" id="overlay-text">Now playing</span>,
     <span class="yt-icon-shape style-scope yt-icon"></span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">544K views</span>,
     <span class="inline-metadata-item style-scope ytd-video-meta-block">2 months ago</span>]




```python
views = sp[0].find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[0].text
```


```python
date_time= sp[0].find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[1].text
```


```python
data = []

for sp in soup.find_all('ytd-rich-grid-renderer'):
    title = sp.find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').text
    video_link = sp.find('a',class_='yt-simple-endpoint focus-on-expand style-scope ytd-rich-grid-media').get('href')
    try:
        views = sp.find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[0].text
    except:
        views = None 
    try:
        date_time= sp.find_all('span', class_ ='inline-metadata-item style-scope ytd-video-meta-block')[1].text
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
      <td>How to Use ChatGPT for Investment &amp; Wealth Bui...</td>
      <td>123K views</td>
      <td>16 hours ago</td>
      <td>/watch?v=8OgwKBiDu5w</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
