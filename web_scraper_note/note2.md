# 2. BUILDING A JOB SCRAPPER

## 2.0 What is Web Scrapping     
- What is Web Scrapping
: 웹상의 데이터를 추출하는 것을 이야기함

- Scrapping : 
url 에서 제목과 상단 이미지를 가져와서 화면에 보여줌 

* 활용 예시
내가 새 휴대폰을 구입하고 싶을 때, 
파이썬 스크립트를 통해서 웹사이트 내 휴대폰 정보를 불러올 수 있음,
할인 상품/할인률/최저가 정보 등등 정보 추출 가능
그외에도 리뷰를 비교, 제품 색인,영화를 리뷰하는 등등
사용 가능


## 2.1 What are We Building      
- 프로젝트 목표 : 이번 프로젝트에서 파이썬 개발 일자리에 대한 정보를 크롤링함. (Indeed/stackoverflow)

- 최종 결과물 : indeed/stackoverflow 에서 python 검색시, 나오는 검색 결과를 불러온 후, 가져온 모든 데이터를 엑셀 시트로 옮김

## 2.2 Navigating with Python      
- import urllib : 파이썬에서 제공하는 라이브러리
- python request : 파이썬에서 요청을 만드는 기능을 모아 놓은 것 (import requests)<br>
ex) indeed_result = request.get("https://www.indeed.com/jobs?q=python&limit=50")
requests 패키지 사용하여 파이썬을 통해서 페이지의 URL 을 가져옴 

- HTML 가져오기
ex) print(indeed_result.text)

- 페이지 숫자 가져오기
 : beautiful soup을 통해서 페이지 숫자 추출


## 2.3 Extracting Indeed Pages      
- beautiful soup 통해서 page 숫자 추출    
~~~
 from bs4 import BeautifulSoup;

 indeed_result = requests.get("https://indeed.com/jobs?q=python&limit=50");

 indeed_soup = BeautifulSoup(indeed_result.text,"html.parset")

 print(indeed_soup)

 pagination = indeed_soup.find("div",{"class":"pagination"})
 print(pagination)
~~~


## 2.4 Extracting Indeed Pages part Two      
~~~
from bs4 import BeautifulSoup

indeed_result = requests.get("https://indeed.com/jobs?q=python&limit=50")

indeed_soup = BeautifulSoup(indeed_result.text,"html.parset")

print(indeed_soup)

pagination = indeed_soup.find("div",{"class":"pagination"})
print(pagination)

links = pagination.find_all("a")
pages = []
print(links)

/*모든 anchor의 span을 찾기*/
for link in links : 
    print(link.find("span"))
    pages.append(link.find("span"))

max_page = pages[0:-1]

~~~

## 2.5 Requesting Each Page      
~~~
from bs4 import BeautifulSoup

/*재사용 가능하도록 정리*/
LIMIT = 50
indeed_URL = requests.get(f"https://indeed.com/jobs?q=python&limit={LIMIT}")

def extract_indeed_pages () : 
    result = requests.get(indeed_URL)

    soup = BeautifulSoup(result.text,"html.parser")

    print(soup)

    pagination = soup.find("div",{"class":"pagination"})
    print(pagination)

    links = pagination.find_all("a")
    pages = []
    print(links)

    /*  모든 anchor의 span을 찾기 */
    for link in links : 
        print(link.find("span"))
        pages.append(link.find("span"))

    max_page = pages[0:-1]
    return max_page

def extract_indeed_jobs (last_page) : 
    jobs = []
    for page in range(last_page)
        #print(f"&start={page*LIMIT}")#
        result = requests.get(f"{URL}&start={page*LIMIT}")
        print(result.status_code)
     return jobs

~~~


## 2.6 Extracting Titles      
~~~
from bs4 import BeautifulSoup


#재사용 가능하도록 정리#
LIMIT = 50
indeed_URL = requests.get(f"https://indeed.com/jobs?q=python&limit={LIMIT}")

def extract_indeed_pages () : 
    result = requests.get(indeed_URL)

    soup = BeautifulSoup(result.text,"html.parser")

    print(soup)

    pagination = soup.find("div",{"class":"pagination"})
    print(pagination)

    links = pagination.find_all("a")
    pages = []
    print(links)

    # 모든 anchor의 span을 찾기 #
    for link in links : 
        print(link.find("span"))
        pages.append(link.find("span"))

    max_page = pages[0:-1]
    return max_page

def extract_indeed_jobs (last_page) : 
    jobs = []
    for page in range(last_page)
        #print(f"&start={page*LIMIT}")#
        result = requests.get(f"{URL}&start={page*LIMIT}")
        """
        어떻게 데이터를 HTML에서 추출해야하는가?
        beautiful soup을 이용해서 데이터 추출이 가능

        """
        soup = BeautifulSoup(result.text,"html.parser")
        results = soup.find_all("div",{"class":"jobsearch-SerpJobCard"})
        print(results)
        for result in results : 
            title = result.find("div",{"class":"title"}).find("a")[["title"]]
    return jobs


~~~
## 2.7 Extracting Companies      
~~~

##company 정보 가져옴#

#재사용 가능하도록 정리#
LIMIT = 50
indeed_URL = requests.get(f"https://indeed.com/jobs?q=python&limit={LIMIT}")

def extract_indeed_pages () : 
    result = requests.get(indeed_URL)

    soup = BeautifulSoup(result.text,"html.parser")

    print(soup)

    pagination = soup.find("div",{"class":"pagination"})
    print(pagination)

    links = pagination.find_all("a")
    pages = []
    print(links)

    # 모든 anchor의 span을 찾기 #
    for link in links : 
        print(link.find("span"))
        pages.append(link.find("span"))

    max_page = pages[0:-1]
    return max_page

def extract_indeed_jobs (last_page) : 
    jobs = []
    for page in range(last_page)
        #print(f"&start={page*LIMIT}")#
        result = requests.get(f"{URL}&start={page*LIMIT}")
        """
        어떻게 데이터를 HTML에서 추출해야하는가?
        beautiful soup을 이용해서 데이터 추출이 가능

        """
        soup = BeautifulSoup(result.text,"html.parser")
        results = soup.find_all("div",{"class":"jobsearch-SerpJobCard"})
        print(results)
        for result in results : 
            title = result.find("div",{"class":"title"}).find("a")[["title"]]
            #링크가 있는 경우, span이 있는 경우가 있음.#
            company = result.find("span",{"class":"company"})
            company_anchor = company.find("a");
            if  company_anchor is not None: 
                company = str(company.find("a").string)
            else : 
                company = str(company.string)
            company = company.strip()#빈칸 제거를 위해 python strip 사용 곁가지에있는 whitespace제거 #
            print(title,company)
            """
            - find : 가져온 데이터의 첫번째만 가져옴
            - find_all : 리스트 결과 전부를 가져옴

            
            """
    return jobs

~~~
## 2.8 Extracting Locations and Finishing up   
- 리팩토링 및 장소 추출
~~~
from bs4 import BeautifulSoup

##company 정보 가져옴#

#재사용 가능하도록 정리#
LIMIT = 50
indeed_URL = requests.get(f"https://indeed.com/jobs?q=python&limit={LIMIT}")

def extract_indeed_pages () : 
    result = requests.get(indeed_URL)

    soup = BeautifulSoup(result.text,"html.parser")

    print(soup)

    pagination = soup.find("div",{"class":"pagination"})
    print(pagination)

    links = pagination.find_all("a")
    pages = []
    print(links)

    # 모든 anchor의 span을 찾기 #
    for link in links : 
        print(link.find("span"))
        pages.append(link.find("span"))

    max_page = pages[0:-1]
    return max_page


def extract_job(html):
    title = html.find("div",{"class":"title"}).find("a")[["title"]]
    #링크가 있는 경우, span이 있는 경우가 있음.#
    company = html.find("span",{"class":"company"})
    company_anchor = company.find("a")
    if  company_anchor is not None: 
        company = str(company.find("a").string)
    else : 
        company = str(company.string)
    company = company.strip()#빈칸 제거를 위해 python strip 사용 곁가지에있는 whitespace제거 #
    location = html.find("div",{"class":"recJobLoc"}).["data-rc-loc"]
    job_id = html["data-jk"]

    return {'title':title,'company':company,'location':location,"link":f"https://www.indeed.com/viewjob?jk={job_id}"}

    """
    - find : 가져온 데이터의 첫번째만 가져옴
    - find_all : 리스트 결과 전부를 가져옴
    """


def extract_indeed_jobs (last_page) : 
    jobs = []
    for page in range(last_page)
        print(f"Scrapping page {page}" )
        #print(f"&start={page*LIMIT}")#
        result = requests.get(f"{URL}&start={page*LIMIT}")
        """
        어떻게 데이터를 HTML에서 추출해야하는가?
        beautiful soup을 이용해서 데이터 추출이 가능

        """
        soup = BeautifulSoup(result.text,"html.parser")
        results = soup.find_all("div",{"class":"jobsearch-SerpJobCard"})
        print(results)
        for result in results : 
            job = extract_job(result)
            jobs.append(job)
    return jobs
~~~

- 타이틀, 회사명, 장소, 링크 정보 수집 완료
## 2.9 ~ 13 (StackOverflow Pages/ extract jobs / extract job / Finish)     
~~~
import requests
from bs4 import BeautifulSoup
"""
requests 요청은 내장 모듈이 아니며 (기본 파이썬 설치와 함께 제공되지 않음) 설치해야합니다.
pip install requests
pip install BeautifulSoup4
"""

##company 정보 가져옴#

#재사용 가능하도록 정리#
LIMIT = 10
URL = f"https://www.indeed.com/q-python-jobs"


def get_last_page () : 
    result = requests.get(URL +".html") #request 생성
    soup = BeautifulSoup(result.text,"html.parser")  #총 페이지 수 알기 위해서 soup 생성/ 어떤 데이터를 찾아주는 라이브러리. 데이터 탐색   
    pagination = soup.find("div",{"class":"pagination"})
    pages = []

    # 모든 anchor의 span을 찾기 #
    links = pagination.find("ul").find_all("li")
    for link in links : 
        links_anchor = link.find("a")        
        if links_anchor is not None: 
            link = str(link.find("span").string)
        else : 
            link = str(link.find("b").string)#get_text()와 string 의 차이? 
        
        pages.append(link)
        print(pages)
    max_page = pages[0:-1]

    return max_page


def extract_job(html):
    title = html.find("h2",{"class":"title"}).find("a")["title"]
    #링크가 있는 경우, span이 있는 경우가 있음.#
    if company : 
        company = html.find("span",{"class":"company"})

        company_anchor = company.find("a")
        if  company_anchor is not None: 
            company = str(company.find("a").string)
        else : 
            company = str(company.string)
            company = company.strip()#빈칸 제거를 위해 python strip 사용 곁가지에있는 whitespace제거 #
    else :
        company = None

    location = html.find("div",{"class":"location"})
    job_id = html["data-jk"]

    return {'title':title,'company':company,'location':location,"link":f"https://www.indeed.com/q-python-jobs.html?vjk={job_id}"}

    """
    - find : 가져온 데이터의 첫번째만 가져옴
    - find_all : 리스트 결과 전부를 가져옴
    """


def extract_jobs (last_page) : 
    jobs = []
    for page in range(last_page) :
        #print(f"Scrapping page {page}" )#
        #print(f"&start={page*LIMIT}")#
        result = requests.get(f"{URL}?q=python&start={page*LIMIT}")
        """
        어떻게 데이터를 HTML에서 추출해야하는가?
        beautiful soup을 이용해서 데이터 추출이 가능

        """
        soup = BeautifulSoup(result.text,"html.parser")
        results = soup.find_all("div",{"class":"jobsearch-SerpJobCard"})
        #print(results)#
        for result in results : 
            job = extract_job(result)
            jobs.append(job)
    return jobs


def get_jobs():
    last_page = get_last_page()
    #jobs = extract_jobs(last_page)
    #return jobs
    
~~~

## 2.14 What is CSV      
 - CSV : 추출한 데이터를 파일(excel)로 옮겨 저장함. 실제 액셀 파일은 아니고, 맥, 윈도우, 브라우저, 구글 드라이브 등등에서도 사용가능한 파일. 
 excel은 마이크로 소프트 제품이 꼭 있어야함. 
 - 확장자명 csv. comma seperated values . 각 컬럼을 ,(comma)로 분리해줌    
 - 각 row는 new line(새 줄) 로 구분    
 
## 2.15 Saving to CSV      
## 2.16 OMG THIS IS AWESOME     


