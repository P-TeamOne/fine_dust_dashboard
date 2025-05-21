# 국내 미세먼지와 호흡계 질환 분석 대시보드
프로젝트 기간: 25.05.15 ~ 25.05.21

팀원 : 지영민, 양창우, 양민식, 박시영
## 🎯 분석 배경 및 목적
최근 국내에서 미세먼지로 인한 건강 문제가 사회적으로 중요한 이슈로 부각되고 있으며, 특히 미세먼지는 대표적인 **호흡기 질환의 유발 요인**으로 알려져 있다. 이에 따라 본 프로젝트에서는 다음과 같은 분석 목표를 설정하였다.

- **국내 지역별 미세먼지와 호흡기 질환 간의 상관관계 분석**
    
    시군구 단위로 미세먼지(PM10) 농도와 폐암, 만성 폐쇄성 폐질환, 하기도감염 등의 발생률 간의 연관성을 통계적으로 분석한다.
     
- **지역 및 시기별 미세먼지 농도 변화 추이 파악**
    
    연도와 분기 단위로 지역별 미세먼지 농도의 변화 양상을 시각화하여 계절적 또는 지역적 패턴을 탐색한다.
    
- **지도 기반 시각화를 통한 지역 간 미세먼지 격차 확인**
    
    위도·경도 정보를 활용한 지도 시각화를 통해 지역 간 pm10 과의 격차를 직관적으로 파악할 수 있도록 한다.
  
- **질병 발생률과 평균 연령 간의 비교 분석**

    남녀 평균 연령과 주요 호흡기 질환 발생률을 지역별로 비교함으로써, 고령 인구 분포가 질병 발생에 어떤 영향을 주는지 분석한다.
    
## 🛠️ 기술 및 프레임워크
| TASK | 활용 기술 | 비고 |
| --- | --- | --- |
| Data Collection | kdx(한국 데이터 거래소),  행정안전부, 기상청  | 보도자료에서 기간 필터링하여 하나의 통합 csv파일로 저장 |
| Data preprocessing | python, pandas | 결측치 제거 및 형식 통일 처리 |
| Data Lake | AWS S3 | 원천 데이터 백업 및 정제 전 데이터 저장소로 활용 |
| Data Warehouse | Redshift | 정제된 데이터를 적재하여 시각화 도구와 연동 |
| Visualization & Dashboard | preset, superset | 지도,통계,상관관계 등 각종 시각화 대시보드 작성 및 협업 |
| Team Management | Slack, Notion, Github, Zep | 업무 공유, 코드 협업, 회의 및 자료 관리에 활용 |

## ✅ 프로젝트 진행과정
### 1. 데이터 수집
    
    한국데이터거래소 - 국내 주요 도시 미세먼지 및 질병 데이터(https://kdx.kr/data/view/28441)

    행정안전부 API

    기상청 API 

    공간정보시스템 (GIS 딥러닝 연구소 @지오서비스)
    
### 2. EDA 및 전처리

    결측치 제거 및 이상치 확인

    yyyymm → year, month 컬럼 분리

    분기별 quarter 컬럼 추가

    wide → long 포맷 변환 (질병별 컬럼 → disease_type, value 형태)

    시군구 단위 구분을 위해 sido + sigungu → region 컬럼 생성

    지도 시각화를 위한 GeoJSON 매핑 처리

### 3. 데이터 적재

    전처리 완료된 CSV 파일을 Amazon S3 버킷에 업로드
  
    Google Colab → Redshift 연결 설정
  
    Redshift에 스키마 및 테이블 생성 → COPY 명령어로 대량 적재
  
    정제된 테이블을 BI 도구에서 사용 가능하도록 구성

### 4. 데이터 시각화 및 대시보드

    주요 시각화 유형:

    Choropleth Map – 시군구별 PM10 농도 및 질병 진단 수 지도 표시

    Heatmap – 연도/월/질병별 환자 수 분포

    Treemap, Line Chart, Bar Chart 등 다양한 통계 시각화

    대시보드 기능:

    year, month, disease_type, region 등 다중 필터 지원

    정책 수립 및 분석용으로 바로 활용 가능한 인터랙티브 구조


## 📊 프로젝트 결과

![9](https://github.com/user-attachments/assets/88b13d7e-fc8d-45de-8b08-bc9571efbd40)
![10](https://github.com/user-attachments/assets/656fd6a1-4a43-44f5-b202-3c138927c9e8)
![11](https://github.com/user-attachments/assets/73676fbe-0214-4732-bb32-9fe720c288b9)
![12](https://github.com/user-attachments/assets/6e9ac093-b07f-4523-a3ef-ada348a399cb)
![13](https://github.com/user-attachments/assets/6abd7705-752d-4e05-b138-f1dd2e44a65e)
![14](https://github.com/user-attachments/assets/acb36de6-d48c-43b1-9cc1-71bacb15e23e)

