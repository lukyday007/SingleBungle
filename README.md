# 🚀 SGBG - 인터넷 밈과 이미지 공유가 중심이 되는 현대 디지털 문화에서, 유저가 선호하는 콘텐츠를 간편하게 저장, 관리하고 이를 토대로 트렌드를 분석하는 플랫폼
> **AI 기반 키워드 추출과 Elasticsearch를 활용한 고성능 이미지 검색 및 실시간 랭킹 시스템**
> <br>
> Google Vision/ChatGPT API로 정교한 메타데이터를 추출하고, Elasticsearch의 가중치 쿼리와 Redis SortedSet을 결합하여 대규모 데이터 환경에서도 빠른 검색과 실시간 트렌드를 제공합니다.


## 🛠 Architecture
<img src="SGBG-architecture.png" width="800" alt="SGBG Architecture">

### Storage & Search Engine
<img src="https://img.shields.io/badge/MySQL_8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white" /> <img src="https://img.shields.io/badge/Elasticsearch_7.17-005571?style=for-the-badge&logo=elasticsearch&logoColor=white" /> <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" /> <img src="https://img.shields.io/badge/AWS_S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white" />

### AI & external API
<img src="https://img.shields.io/badge/Google_Vision_API-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white" /> <img src="https://img.shields.io/badge/ChatGPT_API-412991?style=for-the-badge&logo=openai&logoColor=white" /> <img src="https://img.shields.io/badge/Swagger_OpenAPI_3.0-85EA2D?style=for-the-badge&logo=swagger&logoColor=white" />

<br>

## 💡 Key Features

### 1. AI 기반 이미지 메타데이터 자동 추출
* **Multi-Modal 분석**: S3에 업로드된 이미지 URL을 분석하여 Google Vision과 ChatGPT를 통해 관련 키워드 및 태그를 자동 추출합니다.
* **데이터 정규화**: 추출된 비정형 데이터를 가공하여 MySQL에 최적화된 형태로 저장함으로써 이미지 검색의 기초 인덱스를 확보했습니다.

### 2. Elasticsearch 기반 고성능 검색 엔진
* **가중치 기반 쿼리 설계**: Wildcard 필터링 후 **접두어(Prefix) 일치**에 높은 가중치를 부여하고, **짧은 단어 우선순위** 배치를 통해 사용자 의도에 부합하는 결과를 상단에 노출합니다.
* **실시간 검색 제안**: 사용자가 한 글자씩 입력할 때마다 Elasticsearch를 통해 해당 글자가 포함된 키워드 결과를 지연 없이 반환합니다.

### 3. Redis 기반 실시간 랭킹 및 캐싱 전략
* **실시간 랭킹 구현**: 검색 및 상세 페이지 방문으로 발생하는 조회수 변동을 **Redis SortedSet**에 실시간 반영하여 인기 순위를 관리합니다.
* **Cache-Aside 패턴**: DB 데이터 갱신 전 Redis Cache를 우선 참조하여 빠른 렌더링 성능을 보장하고 메인 DB의 조회 부하를 경감했습니다.

### 4. 시스템 안정성 및 확장성
* **Spring Retry 적용**: 스케줄러 및 외부 AI API 호출 실패 시 재시도 로직을 적용하여 데이터 동기화 안정성을 강화했습니다.
* **Spring Cloud AWS 연동**: AWS S3와의 유연한 통합을 통해 이미지 파일 업로드 및 URL 관리를 효율화했습니다.
