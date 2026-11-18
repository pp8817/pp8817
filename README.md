<div align="left">
  <a href="https://velog.io/@pp8817/posts"><img src="https://img.shields.io/badge/Tech%20Blog-velog-11B57D?style=for-the-badge&amp;logo=velog&amp;logoColor=white" alt="기술 블로그"/></a>
  <a href="mailto:pp8817@naver.com"><img src="https://img.shields.io/badge/Mail-pp8817%40naver.com-03C75A?style=for-the-badge&amp;logo=naver&amp;logoColor=white" alt="이메일"/></a>
</div>

## Selected Impact

- **Landit** — 기획·개발·운영과 Meta 마케팅에 참여한 AI 영어 회화 서비스, 결제 활성화 후 약 50일간 **누적 결제액 253만 원** (2026.09.20~11.13)
- **정시 푸시** — 기기마다 반복하던 DB 저장과 SQS 예약을 묶어 처리, 운영 전후 **서버 처리 시간 중앙값 353→69초** (전 6회·후 8회, 대상 규모 상이·기기 도착 시간 제외)
- **적립 내역 조회** — 조회에서 정산을 분리해 PostgreSQL 합성 입력에서 **UPDATE 1,878→0회**, 응답 JSON 일치와 쓰기 잠금 중 조회 완료 확인
- **척척학사** — 학생 고유 이용자 **8,000명+** (2026.11), **MAU 약 4,000명** (2026.05), 초기 백엔드 단독 개발·기획·운영 주도

## Projects

### Landit | AI 영어 회화 서비스

AI와 영어 대화를 연습하고, 대화 평가에 따라 학습 난이도를 조정하는 서비스입니다.

- **기간** 2026.04 ~ 운영 중
- **팀과 역할** BE 2명·FE 1명 / 백엔드 공동 개발, AI 개발·AWS 인프라 구축과 운영 전담, 기획·Meta 마케팅 참여
- **운영 지표** 누적 가입자 **4,089명** (2026.11.08), **MAU 2,410명** (2026.10)
- **누적 결제액** **253만 원** (2026.09.20~11.13)
- **주요 기술** Java 21, Spring Boot, JPA, Python 3.12, FastAPI, PostgreSQL, SQS, AWS, Terraform

[App Store](https://apps.apple.com/kr/app/id6787414201) · [Google Play](https://play.google.com/store/apps/details?id=com.saynow.app) · [기술 설계 문서](https://github.com/Aragornnnnnn/landit-tech-docs/tree/main)

**적립 내역 조회와 정산 분리**

조회 과정에 결제 재처리와 정산이 섞여 쓰기 잠금을 잡는 것을 확인했습니다. 학습·결제 직후에는 최신 금액을 보여주도록 회차 반영과 정산을 함께 커밋하고, 날짜 마감은 스케줄러로 옮겼습니다. 회차 6개·학습 완료 930건의 PostgreSQL 합성 입력에서 조회 **UPDATE 1,878→0회**를 확인했고, 응답 JSON 일치와 쓰기 잠금 중 조회 완료를 검증했습니다.

**정시 푸시의 반복 저장과 예약 개선**

기기마다 반복하던 DB 선점·결과 저장은 최대 100건씩, SQS 확인 예약은 10건씩 묶었습니다. 운영 전 6회·후 8회의 서버 처리 시간 중앙값이 **353→69초**로 줄었습니다. 대상 규모가 다른 전후 관측이며 기기 도착 시간은 제외했습니다. PostgreSQL에서 동시 선점·재시도·롤백도 검증했습니다.

**표현 조회 OOM 대응**

사용자를 500명씩 나눠도 모든 활성 시나리오의 표현을 읽는 문제가 남아 있었습니다. 당일 시나리오로 조회 범위를 좁혀 PostgreSQL 합성 데이터에서 **700,000→3,500행**으로 줄였습니다 (500명·시나리오 200개·각 표현 7개). 첫 미완료 표현만 읽도록 추가로 좁힌 뒤에도 기존 알림의 종류·대상·문구가 같은지 확인했습니다. 조회 축소와 힙 예산 조정 후 10/22~31 정기 작업 10회의 최종 완료와 해당 기간 OOM 로그 미관측을 확인했습니다.

**LLM 평가와 사용자 레벨 반영 조건 분리**

모델의 점수 산출과 레벨 반영 조건을 나누고, 근거가 부족하거나 유효한 평가를 확보하지 못하면 기존 레벨과 승급 신호를 유지했습니다. 2026.09.28~10.02 운영 평가 410건 중 근거 부족 4건·유효 평가 미확보 8건에서 레벨 보존을 확인했습니다.

<details>
<summary>관련 기술 글</summary>

- [적립 내역 조회에서 정산을 분리하고 잠금 범위를 줄인 과정](https://velog.io/@pp8817/적립-내역-조회에서-정산을-분리하고-잠금-범위를-줄인-과정)
- [정시 푸시의 부하와 중복 발송을 제한한 방법](https://velog.io/@pp8817/정시-푸시의-부하와-중복-발송을-제한한-방법)
- [대화형 AI의 장기기억을 정정 가능한 데이터로 설계하기](https://velog.io/@pp8817/대화형-AI의-장기기억을-정정-가능한-데이터로-설계하기)
- [장기기억 생성 실패를 추적하고 재시도 정책을 고친 과정](https://velog.io/@pp8817/장기기억-생성-실패를-추적하고-재시도-정책을-고친-과정)
- [LLM의 영어 평가를 사용자 레벨에 반영하기까지](https://velog.io/@pp8817/LLM의-영어-평가를-사용자-레벨에-반영하기까지)

</details>

### 척척학사 | 수원대학교 졸업 요건 확인 서비스

학교 포털의 수강 이력과 학사 정보를 가져와 학생의 졸업 요건 충족 여부를 확인하는 서비스입니다.

- **기간** 2025.02 ~ 운영 중
- **역할** 초기 백엔드 단독 개발, 기획·운영 주도 / 졸업 요건 계산·학사 동기화·인증·캐싱, AWS 인프라·배포 담당
- **현재 팀** BE 3명·FE 2명·APP 2명·UI/UX 1명
- **운영 지표** 학생 고유 이용자 **8,000명+** (2026.11), **MAU 약 4,000명** (2026.05)
- **주요 기술** Java 17, Spring Boot, JPA, PostgreSQL, Caffeine, AWS, Terraform

[Web](https://www.cchaksa.com/) · [App Store](https://apps.apple.com/kr/app/id6747005390) · [Google Play](https://play.google.com/store/apps/details?id=com.kunize.uswtimetable)

[Backend](https://github.com/cchaksa/cchaksa-backend) · [Infrastructure](https://github.com/cchaksa/cchaksa-be-terraform) · [Scraper](https://github.com/cchaksa/suwon-scraper-v1)

**인증 필터의 반복 DB 조회 제거**

DB 연결 타임아웃의 원인을 추적해 인증 필터가 요청마다 사용자 정보를 조회하는 것을 찾았습니다. JWT 검증은 유지하고 사용자 정보를 캐시했습니다. t3.micro·Hikari 최대 연결 3개의 졸업 요건 API 부하 실험에서 **요청 26,249건 중 HTTP 실패 0건, p95 91.87ms**를 확인했습니다. k6 `ramping-arrival-rate`로 25분간 목표 요청 시작률을 5→30 req/s로 높였으며, 전체 평균 요청률은 약 17.5 req/s였습니다.

**외부 포털 동기화를 비동기 작업으로 분리**

학교 포털 조회와 DB 반영이 끝날 때까지 기다리던 요청을 접수와 실행으로 나눴습니다. 당시 DB 작업 큐와 `SKIP LOCKED`로 작업을 점유하고, 함께 반영할 학사 데이터는 한 트랜잭션에서 처리했습니다. 비동기 전환 후 워커 설정을 Core 3→7로 조정한 50건 실험에서 완료 시간이 **413.8→192.5초**로 줄었습니다 (Max 7·Queue 50 고정).

**졸업 요건의 조회와 계산 책임 분리**

하나의 CTE에 모여 있던 공통 요건 조회와 학생별 수강 이력 조회를 나누고, 집계는 Java로 옮겼습니다. 공통 요건과 최종 계산 결과를 각각 캐시했습니다. 후속 선택교양 단위 테스트에서 고유 영역 2개 집계와 영역 미지정 과목을 포함한 입력 과목명 4개 반환을 확인했습니다.

<details>
<summary>관련 기술 글</summary>

- [트래픽 피크형 서비스의 운영 구조를 요청 기반 구조로 바꾼 과정](https://velog.io/@pp8817/트래픽-피크형-서비스의-운영-구조를-요청-기반-구조로-바꾼-과정)
- [EC2에서 Lambda로 옮기며 백엔드 실행 경계를 다시 설계한 과정](https://velog.io/@pp8817/척척학사-EC2에서-Lambda로-옮기며-백엔드-실행-경계를-다시-설계한-과정)
- [외부 포털 동기화를 비동기 작업으로 분리한 과정](https://velog.io/@pp8817/트랜잭션의-감옥에서-벗어나기)
- [포털 연동 과정 16초를 0.8초로 줄인 과정](https://velog.io/@pp8817/척척학사-포털-연동-과정-16초를-0.8초로-94.8-개선한-과정)
- [졸업 요건의 조회와 계산 책임을 분리한 과정](https://velog.io/@pp8817/God-Query-해체-분석-척척학사)
- [t3.micro 부하 실험의 기준 수립](https://velog.io/@pp8817/척척학사-t3.micro-서버의-한계-측정-7-TPS는-버티고-10-TPS는-왜-무너졌나)
- [Redis와 로컬 캐시 비교](https://velog.io/@pp8817/척척학사-Redis-vs-Local-Cache-t3.micro에서-캐시는-어디까지-의미가-있을까)
- [인증 필터의 반복 DB 조회 제거](https://velog.io/@pp8817/척척학사-인증-필터-캐시-적용으로-병목은-사라졌을까)

</details>

## Experience

- **소프트웨어 마에스트로 17기 연수생** | 2026.04 ~ 2026.12 예정
  - AI 영어 회화 서비스 Landit 기획·개발·운영·Meta 마케팅 참여
- **YAPP 27기 Server Developer** | 2025.11 ~ 2026.03
  - Moit, Weddin 개발
  - YAPP 27기 성과공유회 최우수상
- **교내 개발 동아리 Semicolon 백엔드 멘토** | 2024.03 ~ 2025.07

## Tech Stack

<strong>Backend</strong>
<br>
<img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=SpringBoot&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="기술 스택 배지"/>

<strong>Infrastructure & DevOps</strong>
<br>
<img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Terraform-844FBA?style=for-the-badge&logo=terraform&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="기술 스택 배지"/>

<strong>Database</strong>
<br>
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="기술 스택 배지"/>

<strong>Operations</strong>
<br>
<img src="https://img.shields.io/badge/Sentry-362D59?style=for-the-badge&logo=sentry&logoColor=white" alt="기술 스택 배지"/>
<img src="https://img.shields.io/badge/Grafana%20Loki-F46800?style=for-the-badge&logo=grafana&logoColor=white" alt="기술 스택 배지"/>

## Certificates

- AWS Certified Solutions Architect - Associate | 2024.12
- SQLD | 2024.06
- TOEIC Speaking Intermediate High | 2025.12

## Awards

- <strong>2026</strong> | YAPP 27기 성과공유회 최우수상
- <strong>2026</strong> | AI-SW Developers 공모전 4기 최우수상
- <strong>2025</strong> | 수원대학교 창업 경진대회 제13회 최우수상
- <strong>2025</strong> | 수원대학교 창업 경진대회 제12회 우수상
- <strong>2025</strong> | AI-SW Developers 공모전 3기 우수상
