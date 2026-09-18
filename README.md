[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=40&pause=1000&color=F7EFEF&background=000000&center=true&vCenter=true&width=600&height=100&lines=Hi!+I'm+Taewan+Kim)](https://git.io/typing-svg)

## 📋 Intro

금융 도메인의 AI 서비스를 만드는 엔지니어입니다.

사회초년생을 위한 자산관리 서비스를 만들면서, 금융 정보의 격차가 곧 기회의 격차가 된다는 문제의식을 얻었습니다. 그래서 판단 기준이 없는 사람에게 결과만이 아니라 근거까지 전달하는 서비스에 관심이 있습니다. 종목을 추천하는 모델에 설명 기능을 붙이고, 퇴직연금 상담에서 행원이 고객 앞에서 법령과 약관 근거를 바로 확인하도록 검색 구조를 설계한 것도 같은 이유입니다.

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

### 3. [연금사수](레포_링크) — 퇴직연금 창구 상담 지원 시스템
> 상담 중 근거 문서 제시, 상담 후 점검, 본부와 현장의 지식 순환을 하나의 흐름으로 묶은 행원용 RAG 서비스
> `2026.08` · `4인 팀` · 금융 AI 공모전 출품작 · **RAG 개발 (법령, 약관 트랙 전담) / 지식 순환 기능 전담**

- 법령과 약관, 계약서 16개 문서를 조 단위로 청킹해 조 526개, 항 1,436개를 BGE-M3 임베딩과 pgvector HNSW로 색인. 2단 컬럼 조문 순서 뒤섞임 등 파싱 버그 10종을 수정해 gold coverage 30/30 확보
- **문서명 헤더 부착으로 제도유형 계열 Dense MRR 0.274 → 0.712, 답변 정확도 70.0% → 83.3%.** 질문 유형별 서브셋 분석으로 DB, DC, IRP 계열이 표준계약서를 공유해 본문만으로 구분되지 않는 원인을 특정
- 질문 증강 인덱싱은 검색 MRR이 0.623 → 0.652로 올랐지만 답변 정확도가 76.7% → 70.0%로 떨어져 기각. 이후 모든 실험을 검색 지표와 최종 답변 품질로 함께 판단
- Dense와 BM25가 각각 상위 20건을 뽑고 그 합집합에만 RRF(k=60)를 적용하는 하이브리드 검색으로 실시간 상담 환경에 맞게 재설계
- 창구 질의를 1:N 클러스터 구조로 자동 집계해 본부 Top5 현황판과 RAG 기반 게시판 초안 생성 구현. 질문 적재는 답변 스트림과 분리된 태스크로 처리해 응답 지연 방지
- 2주 만에 상담부터 본부 피드백까지 하나의 순환 흐름이 동작하는 MVP 배포

`Python` `FastAPI` `BGE-M3` `pgvector` `BM25` `Supabase` `Gemini` `Redis` `Docker`

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
