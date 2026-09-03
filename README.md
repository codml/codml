[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=40&pause=1000&color=F7EFEF&background=000000&center=true&vCenter=true&width=600&height=100&lines=Hi!+I'm+Taewan+Kim)](https://git.io/typing-svg)

## 📋 Intro

금융 도메인의 AI 서비스를 만드는 엔지니어입니다.

사회초년생을 위한 자산관리 서비스를 만들면서, 금융 정보의 격차가 곧 기회의 격차가 된다는 문제의식을 얻었습니다. 그래서 판단 기준이 없는 사람에게 결과만이 아니라 근거까지 전달하는 서비스에 관심이 있습니다. 종목을 추천하는 모델에 설명 기능을 붙이고, 카드를 추천하는 시스템에 근거 문서 없이는 상품명을 말하지 못하도록 제약을 건 것도 같은 이유입니다.

세 개의 프로젝트에서 LLM 에이전트와 데이터 파이프라인, 모델 학습까지 서비스가 동작하는 전 구간을 직접 다뤘습니다. 문제를 만나면 자원을 늘리기 전에 원인부터 특정합니다. 잘못 짚은 개선은 비용만 늘리고 문제는 남기기 때문입니다.

## 📜 Licenses & Certifications
- 정보처리기사
- SQLD
- 빅데이터분석기사

<br>

## 🗂️ Projects

### 1. [WooriPort](https://github.com/codml/ai-server) — 사회초년생 맞춤형 AI 자산관리 서비스
> 월급 분배, 절세 계좌 안내, 투자 기간별 포트폴리오 생성을 하나의 흐름으로 묶은 자산관리 서비스
> `2026.04 ~ 2026.06` · `5인 팀` · **AI 에이전트 리더 / 백엔드**

- LangGraph 기반 멀티 에이전트 설계. 월급 분배는 Plan-Reflect-Refine 구조, 포트폴리오 생성은 Planner-Executor-Verifier 구조로 구현
- **응답 시간 34.88초 → 19.02초, 약 45% 단축.** LangSmith 트레이스로 병목을 LLM 6회 순차 호출 구조로 특정한 뒤 Send API 동적 병렬 분기로 재설계
- LLM은 성향 분석과 종목 선정, 비중 산출은 HRP가 담당하도록 역할을 분리해 근거 없는 비중 생성을 차단
- Airflow 일간, 월간 DAG 단독 설계로 ETF 수집과 지표 계산, 임베딩 갱신 자동화
- 시계열 적재는 MySQL, 서비스 조회와 벡터 검색은 PostgreSQL + pgvector로 분리

`Python` `FastAPI` `LangGraph` `Airflow` `PostgreSQL(pgvector)` `MySQL` `Redis` `Docker` `ELK` `Grafana` `LangSmith`

<br>

### 2. [S2FE](https://github.com/codml/S2FE) — 기본적 분석 및 머신러닝 앙상블 기반 주식 종목 선택
> 재무제표에 비재무 공시정보와 거시경제지표를 더해 다음 분기 초과 수익 종목을 선택하는 앙상블 모델
> `2025.03 ~ 2025.08` · `5인 팀` · **팀장** · 학술지 게재, 우수 졸업작품상

- KOSPI200 중 177개 기업, 2015년 4분기부터 2024년 3분기까지의 데이터로 Walk Forward 검증 4개 페이즈, 10회 반복 평가
- **평균 수익률 16.2%, CAGR 13.9%.** 차선 비교 모델 대비 각각 +14.2%p, +12.2%p
- **절제 실험에서 공시정보와 거시경제지표를 모두 제거하면 평균 수익률이 29%p 감소.** 데이터 축 확장의 기여도를 정량 입증
- LLM 기반 뉴스 필터링 설계 및 실험 담당. Chain of Thought로 추론 단계를 제약한 결과 필터링 적용 시 CAGR 18.1%로 미적용 대비 +11%p
- 확장 파트에서 SHAP 기반 XAI와 강화학습 매매 시점 최적화를 추가해 데스크톱 앱으로 통합

`Python` `PyTorch` `scikit-learn` `SHAP` `OPENDART` `FRED` `Gemini` `PyQt`

<br>

### 3. [소비 패턴 기반 카드 추천 시스템](https://github.com/codml/fisa06-tech-seminar)
> 협업 필터링으로 소비 둔화 업종을 찾고, RAG로 해당 업종에 혜택을 주는 카드를 추천하는 개인 프로젝트
> `개인 프로젝트` · **기여도 100%**

- 후보군 압축, Top-K 선별과 둔화 업종 추출, RAG 추천의 3단계 파이프라인 설계
- 서버 시작 시점에 K-Means 클러스터링을 수행하고 인접 클러스터만 후보군으로 압축해, 요청당 수십 초 걸리던 유사도 계산을 실시간 응답 수준으로 개선. **실루엣 계수 0.5966**
- 개발 중 존재하지 않는 카드명이 생성된 사례를 확인하고, 상품 설명서 50개를 수집해 500자 단위로 청크 분할 후 ChromaDB에 적재
- **`RAG_ENABLED` 플래그를 도입해 근거 문서가 없으면 카드명과 혜택 수치 생성을 금지.** 불완전판매로 이어질 수 있는 환각을 구조적으로 차단
- 약 3GB 데이터셋을 chunksize 50,000 단위로 나눠 MySQL에 적재

`Python` `FastAPI` `scikit-learn` `ChromaDB` `MySQL` `GPT-4o-mini` `Bootstrap`

<br>

## 🦾 Skills

**Language**  
![Python](https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/c++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![SQL](https://img.shields.io/badge/sql-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

**AI / ML**  
![LangChain](https://img.shields.io/badge/langchain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![PyTorch](https://img.shields.io/badge/pytorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![OpenAI](https://img.shields.io/badge/openai-412991?style=for-the-badge&logo=openai&logoColor=white)

**Backend / Data**  
![FastAPI](https://img.shields.io/badge/fastapi-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Airflow](https://img.shields.io/badge/airflow-017CEE?style=for-the-badge&logo=apacheairflow&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/postgresql-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/redis-FF4438?style=for-the-badge&logo=redis&logoColor=white)

**Infra / Tools**  
![Docker](https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white)

<br>

## ☎️ Contact

<p align="left">
<a href="mailto:kimtaewanlol@gmail.com"><img src="https://img.shields.io/badge/Gmail-EA4335?style=flat-square&logo=Gmail&logoColor=white"/></a>
<a href="https://stepb2step.tistory.com/"><img src="https://img.shields.io/badge/Tistory-000000?style=flat-square&logo=Tistory&logoColor=white"/></a>
<a href="https://www.instagram.com/taewan512"><img src="https://img.shields.io/badge/Instagram-E4405F?style=flat-square&logo=Instagram&logoColor=white"/></a>
</p>

[![Solved.ac 프로필](http://mazassumnida.wtf/api/v2/generate_badge?boj=kimtawann)](https://solved.ac/profile/kimtawann)
