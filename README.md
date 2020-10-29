mkdir scraping
cd scraping
python -m venv env
env\Scripts\Activate.ps1
(env) > pip install requests
(env) > pip install beautifulsoup4



import requests


def main():
    params = {
        'keyword': 'python',
        'ym': '201812',
    }
    url = 'https://connpass.com/api/v1/event/'
    r = requests.get(url, params=params)
    event_info = r.json()  # レスポンスのJSONを変換

    print('件数:', event_info['results_returned'])  # 件数を表示
    for event in event_info['events']:
        print(event['title'])
        print(event['started_at'])

if __name__ == '__main__':
    main()

import requests

def main():
    params = {
        'keyword': 'python',
        'ym': '201812',
    }

url = 'https://connpass.com/api/v1/event/'
r = requests.get(url, params=params)
event_info = r.json()


print('件数:', event_info['results_returned'])
for event in event_info['events']:
    print(event['title'])
    print(event['started_at'])


if __name__ == '__main__':
    main()

import requests
from bs4 import BeautifulSoup


def main():
    url = 'https://pycon.jp/2017/ja/sponsors/'
    res = requests.get(url)
    content = res.content
    soup = BeautifulSoup(content, 'html.parser')
    sponsors = soup.find_all('div', class_='sponsor-content')
    for sponsor in sponsors:
        url = sponsor.h3.a['href']
        name = sponsor.h4.text
        print(name, url)


if __name__ == '__main__':
    main()

import requests
from bs4 import BeautifulSoup

def main():

url = 'https://pycon.jp/2017/ja/sponsors/'
res = requests.get(url)
content = res.content


soup = BeautifulSoup(content, 'html.parser')
sponsors = soup.find_all('div', class_='sponsor-content')
for sponsor in sponsors:
url = sponsor.h3.a['href']
name = sponsor.h4.text
print(name, url)


if __name__ == '__main__':
    main()

soup = BeautifulSoup(content, 'html.parser')
sponsors = soup.find_all('div', class_='sponsor-content')
for sponsor in sponsors:
url = sponsor.h3.a['href']
name = sponsor.h4.text
print(name, url)

import requests
r = requests.get('https://api.github.com/user', auth=('user', 'pass'))
r.status_code


payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.post('http://httpbin.org/post', data=payload)
print(r.text)

payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('http://httpbin.org/get', params=payload)
print(r.url)
http://httpbin.org/get?key2=value2&key1=value1
payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
r = requests.get('http://httpbin.org/get', params=payload)
print(r.url)
http://httpbin.org/get?key1=value1&key2=value2&key2=value3



import requests
from bs4 import BeautifulSoup
r = requests.get('https://www.python.org/blogs/')
soup = BeautifulSoup(r.content, 'html.parser')
soup.title
<title>Our Blogs | Python.org</title>
soup.title.name

soup.title.string

soup.a
<a href="#content" title="Skip to content">Skip to content</a>
len(soup.find_all('a'))

url = 'https://www.python.org/news/'
res = requests.get(url)
soup = BeautifulSoup(res.content, 'html.parser')


len(soup.find_all('h1'))
3
len(soup.find_all(['h1', 'h2', 'h3']))
24
len(soup.find_all('h3', {'class': 'event-title'}))
