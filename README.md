## 1. 데이콘 머신러닝 경진대회 소개 및 개요
- 주제 : AI 알고리즘 활용 카드 사용 금액 예측

- 목표 : 신용카드 사용 내역 데이터를 활용한 지역별, 업종별 월간 카드 사용 총액 예측

- 배경 : 신용카드 사용량을 분석을 통한  ‘Post COVID-19 시대’ 신용카드 사용량 예측 모델 

- 주최/주관
    + 주최 : 제주특별자치도청, 제주테크노파크
    + 주관 : DACON
- 웹사이트 : [제주 신용카드 빅데이터 경진대회](https://dacon.io/competitions/official/235615/overview/)

## 2. 데이터 구성
### (1) 데이터셋 구성
- 훈련데이터 : 201901-202003.csv (2.07 GB)
    + 임의추출 후 1000개만 저장
- 데스트 데이터 : 202004.csv (116 MB)
    + 데이터 공개일 : 2020.07.28
- 제출 양식 : submission.csv (64 KB)

### (2) 데이터 정의서
- REG_YYMM : 년월
- ...
- ...

### (3) 참고
- 모든 데이터는 [구글 클라우드 빅쿼리](https://cloud.google.com/bigquery)에 적재하였고, 아래와 같이 불러와서 머신러닝 프로젝트를 수행하였음

```python
import pandas

project_id = 'cardproject-283503'
client = bigquery.Client(project=project_id)

train = client.query('''
  SELECT 
      * 
  FROM `cardproject-283503.jeju_data_ver1.201901_202003_train` 
  WHERE RAND() < 10000 / (SELECT COUNT(*) FROM `cardproject-283503.jeju_data_ver1.201901_202003_train`)
  ''').to_dataframe()
```

## 3. 개발 스펙
### (1) OS 환경
- OS 환경 : Linux, jupyter, Google Colab

### (2) Python 버전, 패키지 버전
- Python 버전 : 3.6.9
