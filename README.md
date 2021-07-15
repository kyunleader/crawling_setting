# crawling_setting

## 크롤링 셋팅 도구 정리

 크롤링을 시작할때 기본적으로 필요한 패키지 및 코드들을 정리해보자. 두고두고 쓸수 있을 것이다아아아.


### 기본 필요 패키지

 ```python
 
 from selenium import webdriver  # 셀레니움할때 필요한 패키지
 
 import requests  # 사이트에 정보를 요청하는 패키지
 
 from selenium.webdriver.chrome.options import Options  # 원격창을 띄울때 여러 옵션을 설정할 때 필요
 
 from bs4 import BeautifulSoup  # 사이트의 정보를 가져오는 패키지
 
 from selenium.webdriver.common.keys import Keys  # 셀레니움에서 어떤 키를 누르게 할때 필요
 
 from selenium.webdriver.support.ui import WebDriverWait  # 웹사이트 로딩 될때까지 기다리게할때 필요
 
 from webdriver_manager.chrome import ChromeDriverManager  # 크롬드라이버 설치에 필요
 
 from selenium.common.exceptions import *  # 셀레니움 예외발생을 볼때 필요
 
 
 ```

<h3>크롬드라이버 불러오기 </h3>

 
 - 방법 1 크롬드라이버 설치해서 가져오기
 
 https://chancoding.tistory.com/136     참조
 
 
 
 - 방법 2 ChromeDriverManager를 활용해서 가져오기
 
 ```python
 driver = webdriver.Chrime(ChromeDriverManager().install()) # 으로 설치
 ```
 
 
<h3>requsts 하기</h3>
 
 
 ```python
 # 예시 (크롬드라이버 및 셀레니움이 필요없는 간단한 크롤링)
 # 간단한 크롤링에 사용 됨.
 url = https://www.naver.com/
 req = requests.get(url)
 soup = BeautifulSoup(req.text, 'html.parser')  # html 정보 불러오기 완료
 
 # 원하는 정보 찾기
 
 # 방법 1.
 soup.find('div', class_ = 'class_name')
 
 # 방법 2.
 soup.select('.class_name > next_sub_name')  # 앞에 .을 붙이면 class라는 뜻
 
 # select 참고 
 soup.select('원하는 정보')  # select('원하는 정보') -->  단 하나만 있더라도, 복수 가능한 형태로 되어있음
 soup.select('태그명')
 soup.select('.클래스명')
 soup.select('상위태그명 > 하위태그명 > 하위태그명')
 soup.select('상위태그명.클래스명 > 하위태그명.클래스명')    # 바로 아래의(자식) 태그를 선택시에는 > 기호를 사용
 soup.select('상위태그명.클래스명 하~위태그명')              # 아래의(자손) 태그를 선택시에는   띄어쓰기 사용
 soup.select('상위태그명 > 바로아래태그명 하~위태그명')     
 soup.select('.클래스명')
 soup.select('#아이디명')                  # 태그는 여러개에 사용 가능하나 아이디는 한번만 사용 가능함! ==> 선택하기 좋음
 soup.select('태그명.클래스명')
 soup.select('#아이디명 > 태그명.클래스명')
 soup.select('태그명[속성1=값1]')
 ```
 
 
 ### 셀레니움 하기
 
 ```python
 
 # 셀레니움 옵션 설정 (필요한 것만 쓰기)
 options = webdriver.ChromeOptions()
 options.add_argument('headless')     # 창 안보이게 하기
 options.add_argument('--incognito')  # 시크릿모드 설정
 
 import os
 
 try:  # 크롬드라이버 설치했을경우
     path = os.getcwd()
     driver = webdriver.Chrome(path + '/chromedriver', options=options)
 except:  # 크롬드라이버 없을경우
     driver = webdriver.Chrome(ChromeDriverManager().install(), options=options)
     
 url = https://www.naver.com/
 driver.get(url)  # 해당 url 페이지로 이동
 ```
 
 https://ltlkodae.tistory.com/18   <- 셀레니움 정보 찾기 참조
 
 



 
