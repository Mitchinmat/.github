# <img src="./resources/img/logo.png" width="20px"/> 믿친맛(믿을 수 있는 친구들의 맛집 공유 서비스)


<br/>
<img src="./resources/img/main.png" />
<br/><br/>

> '믿친맛'은 믿을 수 있는 친구들과 맛집을 공유하는 서비스입니다.  

<br/>

|믿친맛|
| :------: |
|[랜딩 페이지(mitchinmat.com)](https://mitchinmat.com/)|
|[서비스 페이지(mitchinmat.com)](https://app.mitchinmat.com/)|
|[믿친맛 앱(google play)](https://play.google.com/store/apps/details?id=com.mitchinmat&hl=ko)|
|[믿친맛 Notion](https://www.notion.so/jmxx219/0be8aa563b104eedaf97cd76eaeb604b)|

 
<br><br>

## 목차
1. [개요](#개요)
2. [서비스 소개](#서비스-소개)
3. [프로젝트 설계](#프로젝트-설계)
4. [개발 환경 및 기술 스택](#개발-환경-및-기술-스택)
5. [팀원 소개](#팀원-소개)

<br/>

## [개요](#목차)

> **개발 기간** : `2024-07-02 ~ 2024-08-15`

<br>

검색 알고리즘을 역이용한 바이럴, 생성형 AI를 활용한 가짜 정보들이 주요 검색 채널을 장악하면서 사용자가 신뢰할만한 정보가 인터넷에서 줄어들고 `죽은 인터넷`이라는 사회적 문제로 대두되고있다. 이에 따라 신뢰성 높은 정보 제공에 대한 정보 검색 사용자들의 수요가 증가하고 있다.

<br>
 
**믿친맛이란?**

믿친맛은 '믿을 수 있는 친구의 맛집 공유 서비스'의 약어로 사용자로 하여금 친구의 친구라는 범위 안에서 음식점을 추천하고 공유할 수 있는 소셜 네트워크 서비스로, 맛집 추천이라는 주제 안에서 사용자들에게 신뢰할 수 있는 검색 채널을 제공한다.

<br>

### 주요 기능


1. 친구의 친구들의 맛집 공유
    -  카카오톡 소셜로그인으로 친구 목록 동기화 
    -  친구관계를 기반으로 친구의 친구들의 맛집 지도를 공유 
    -  친구 공개 비공개 기능을 통해서 원하는 목록만 지도에 남길수 있음

2. 맛집과 맛집지도 공유 링크 제공
    -  맛집과 맛집 지도를 스냅샷으로 공유할 수 있는 기능 제공 
    -  서비스 내부에 내장된 메세지 기능으로 친구에게 바로 전송 가능 
    -  공유시 남들에게 보이고싶지 않은 맛집을 숨김처리 가능

3. 맛집에 대한 추가 정보(메모/댓글) 제공
    - 메모 : 나만 확인할 수 있는 정보로 맛집으로 등록한 음식점의 장단점을 메모할 수 있음 
    - 댓글 : 친구에게 공유되는 정보로 주변인들에게 해당 맛집에 대한 장단점을 댓글로 알릴 수 있음


<br>

### 차별점/독창성

1.  Elastic Search를 통한 검색 로직 최적화  
    -  카카오 검색으로부터 가져온 정보, 사용자가 입력한 메모, 댓글을 기반으로 연관검색 기능을 제공 
    -  스프링 배치를 활용하여 연관검색 데이터에 대한 주기적 업데이트

2.  Redis를 활용한 쿼리 캐싱 
    -  네트워킹 서비스 특성상 한번 쿼리에 연산량이 많은 것을 보완하기위해 동일쿼리에 대해 캐싱을 진행  
    -  같은 쿼리가 들어왔을때 Redis 캐시를 조회해서 최근에 검색한 결과가 있으면 해당 정보를 우선적으로 출력

3. 효율적인 운영을 위한 로그 구체화 및 주기적 데이터 백업
    -  배포 이후 발생하는 에러를 효율적으로 관리하기 위해 에러 상황을 내부 로직 에러와 서비스 에러로 분류한 후 Mattermost Webhook 기능을 활용하여 서비스에러가 발생함과 동시에 즉각적으로 반응할 수 있도록 설계
    -  데이터베이스의 오류와 손실을 막기위한 스케쥴러를 통한 주기적인 데이터 백업

4. 사용자 경험 개선을 위한 이미지 크롤링
    -  사용자의 원활한 사용을 위한 초기 데이터 구축(약 14000개의 음식점) 이후 사용자가 새로이 추가하는 음식점에 대해서 자동으로 기본정보를 가져올 수 있는 로직 구현, 동적페이지 크롤링이 필요할 경우 요청이 쌓이면 주기적으로 FastAPI로 구현된 Selenium 크롤러를 활용하여 데이터 업데이트

5. 웹과 앱을 활용한 서비스 제공  

    -  모바일 기반 서비스이므로 빠른 진입을 위해 앱 제공, 딥링크를 활용하여 빠르게 앱 진입가능

<br/>
<br/>

## [서비스 소개](#목차)


### 1️⃣ <b>메인 페이지</b>

| **Register Page** | **Main Page** | **Main Page** |
| :------: | :------: |:------: |
|<img src="./resources/gif/맛집신규등록.gif" height="400">|<img src="./resources/gif/현재위치검색.gif" height="400">| <img src="./resources/gif/맛집 페이지네이션.gif" height="400">|

| **Detail Page** | **Memo/Review Page** |**Search Page** |
| :------: | :------: |:------: |
|<img src="./resources/gif/마커클릭상세보기.gif" height="400">|<img src="./resources/gif/메모_리뷰.gif" height="400">|<img src="./resources/gif/맛집검색.gif" height="400">|


<br>

### 2️⃣ <b>친구 페이지</b>

| **DM Page** | **Friend Map Page** | **Public/Private Toggle** |
| :------: | :------: |:------: |
|<img src="./resources/gif/DM.gif" height="400">|<img src="./resources/gif/친구_친구지도.gif" height="400">| <img src="./resources/gif/공개 비공개 토글.gif" height="400">|


<br>

### 3️⃣ <b>마이 페이지</b>

| **Login Page** | **My Page** |
| :------: |:------: |
|<img src="./resources/gif/소셜로그인.gif" height="400">|<img src="./resources/gif/마이페이지.gif" height="400">



<br/>
<br/>

## [프로젝트 설계](#목차)

### 시스템 아키텍쳐

<table>
  <tr>
    <td style="text-align:center;">
      <img src="./resources/img/아키텍쳐.png" />
    </td>
    <td style="text-align:center;">
      <img src="./resources/img/서비스.png" />
    </td>
  </tr>
  <tr>
    <td style="text-align:center;">
      <img src="./resources/img/CICD.png" />
    </td>
    <td style="text-align:center;">
      <img src="./resources/img/Blue-Green-Deployment.png" />
    </td>
  </tr>
  <tr>
    <td style="text-align:center;">
      <img src="./resources/img/모니터링.png" />
    </td>
  </tr>
</table>

<br/>

### ERD
<img width="500px" src="./resources/img/ERD.png">


<br/>
<br/>

## [개발 환경 및 기술 스택](#목차)

|  개발 환경  | 기술 스택 |
|:-------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Frontend** |![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=HTML5&logoColor=white) ![CSS](https://img.shields.io/badge/CSS-1572b6?style=for-the-badge&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=JavaScript&logoColor=white) ![vite](https://img.shields.io/badge/vite-646CFF?style=for-the-badge&logo=vite&logoColor=white) ![react](https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=white) ![typescript](https://img.shields.io/badge/typescript-3178C6?style=for-the-badge&logo=typescript&logoColor=white) ![axios](https://img.shields.io/badge/axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white)  ![redux](https://img.shields.io/badge/redux-764ABC?style=for-the-badge&logo=redux&logoColor=white) |
| **Backend** | ![Java](https://img.shields.io/badge/Java_17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white) ![Gradle](https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white) ![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.3.1-6DB33F?style=for-the-badge&logo=spring&logoColor=white) ![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=spring-security&logoColor=white) ![OAuth2](https://img.shields.io/badge/OAuth2-6DB33F?style=for-the-badge&logo=spring-security&logoColor=white) ![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-gray?style=for-the-badge&logo=Spring_Data_JPA&logoColor=white) ![QueryDSL](https://img.shields.io/badge/QueryDSL-0078D4?style=for-the-badge&logo=Querydsl&logoColor=white) ![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=json-web-tokens&logoColor=white)  |
|   **DB**    | ![mysql](https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![redis](https://img.shields.io/badge/redis-DC382D?style=for-the-badge&logo=redis&logoColor=white) ![mongodb](https://img.shields.io/badge/mongodb-47A248?style=for-the-badge&logo=mongodb&logoColor=white)  ![Elastic Search](https://img.shields.io/badge/elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|   **Infra**   | ![amazonec2](https://img.shields.io/badge/amazon_ec2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)  ![docker](https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![nginx](https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white) |                                                                                                                                                                                                                      |
|**Monitoring**|![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white) ![Cadvisor](https://img.shields.io/badge/cadvisor%20-7B7D7F?style=for-the-badge&logo=cadvisor%20&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=Grafana&logoColor=white)
|   **Management Tool**   | ![Jira](https://img.shields.io/badge/jira-0052CC?style=for-the-badge&logo=jira&logoColor=white) ![Gitlab](https://img.shields.io/badge/GitLab-FC6D26?style=for-the-badge&logo=GitLab&logoColor=white) ![Mattermost](https://img.shields.io/badge/mattermost-0058CC?style=for-the-badge&logo=mattermost&logoColor=white)  ![Notion](https://img.shields.io/badge/Notion-000000.svg?style=for-the-badge&logo=notion&logoColor=white) ![Figma](https://img.shields.io/badge/figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white) ![Swagger](https://img.shields.io/badge/-Swagger-%23Clojure?style=for-the-badge&logo=swagger&logoColor=white)                                                                                                                                                                                                                                                                                                                                                                                 |
| **외부 API**  | ![kakao map API](https://img.shields.io/badge/kakao_map_api-FFCD00?style=for-the-badge&logo=kakao&logoColor=white)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|**App**|![ReactNative](https://img.shields.io/badge/ReactNative-61DAFB?style=for-the-badge)|

<br/>
<br/>

## [팀원 소개](#목차)

<table align="center">
  <tr>
    <th style="text-align: center;"><a href="https://github.com/hongsam100">김민철</a></th>
    <th style="text-align: center;"><a href="https://github.com/baebini11">배원빈</a></th>
    <th style="text-align: center;"><a href="https://github.com/maison01006">오승진</a></th>
  </tr>
  <tr>
    <td style="text-align: center;"><img src="./resources/img/김민철.png" alt="" width="150px"/></td>
    <td style="text-align: center;"><img src="./resources/img/배원빈.png" alt="" width="150px"/></td>
    <td style="text-align: center;"><img src="./resources/img/오승진.png" alt="" width="150px" /></td>
  </tr>
  <tr>
    <td style="text-align: center;"><b>Frontend</b></td>
    <td style="text-align: center;"><b>Frontend</b></td>
    <td style="text-align: center;"><b>Infra</b></td>
  </tr>
</table>

<table align="center">
  <tr>
    <th style="text-align: center;"><a href="https://github.com/BTY-97">방태연</a></th>
    <th style="text-align: center;"><a href="https://github.com/jmxx219">손지민</a></th>
    <th style="text-align: center;"><a href="https://github.com/s2hoon">조수훈</a></th>
  </tr>
  <tr>
    <td style="text-align: center;"><img src="./resources/img/방태연.png" alt="" width="150px" /></td>
    <td style="text-align: center;"><img src="./resources/img/손지민.png" alt="" width="150px"/></td>
    <td style="text-align: center;"><img src="./resources/img/조수훈.png" alt="" width="150px" /></td>
  </tr>
  <tr>
    <td style="text-align: center;"><b>Backend</b></td>
    <td style="text-align: center;"><b>Backend</b></td>
    <td style="text-align: center;"><b>Backend</b></td>
  </tr>
</table>



</br>
