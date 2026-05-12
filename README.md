# Backend Developer, 박상민

**사용자 경험을 지탱하는 견고한 인프라와 서버를 설계합니다.** <br>
비즈니스 로직 구현을 넘어, 안정적인 서비스 운영을 위한 아키텍처 설계에 관심이 많습니다. <br>

<div align="left">
  <a href="https://docs.google.com/document/d/1ocVEA9Xrdy9ZU2CZ-eVPX09A7GbpnjQuTFhHyOqKPns/edit?usp=sharing"><img src="https://img.shields.io/badge/Resume-Google%20Docs-4285F4?style=for-the-badge&logo=google-docs&logoColor=white"/></a>
  <a href="https://velog.io/@pp8817/posts"><img src="https://img.shields.io/badge/Tech%20Blog-velog-11B57D?style=for-the-badge&logo=velog&logoColor=white"/></a>
  <a href="mailto:pp8817@naver.com"><img src="https://img.shields.io/badge/Mail-pp8817%40naver.com-03C75A?style=for-the-badge&logo=naver&logoColor=white"/></a>
</div>

<br>

## 💼 Experience
- SW Maestro 17기  <sub>2026.04 ~ ing</sub></a>
- <a href="https://www.yapp.co.kr/"><strong>YAPP</strong></a> | 27기 Server Developer <sub>2025.11 ~ 2026.03</sub>
  - 최우수상: `Moit`(모임 일정 관리 서비스), `Weddin`(청첩장 모임 주최자를 위한 모임 관리 서비스)

## 🛠 Tech Stack

**Backend**
<br>
<img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Boot-6DB33F?style=for-the-badge&logo=SpringBoot&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Data JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white"/>

**Infrastructure & DevOps**
<br>
<img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white"/>
<img src="https://img.shields.io/badge/Github Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>

**Database**
<br>
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white"/>
<img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white"/>

---

## 🚀 Projects

### 🎓 [척척학사](https://github.com/pp8817/Chukchuk-haksa_Server): 졸업 요건 자동 비교 및 관리 서비스
> **Role:** 백엔드 팀장 | **Period:** 2025.02 ~ (진행 중) <br>
> **Stack:** Java, Spring Boot, PostgreSQL, Redis, Caffeine, AWS, Terraform, Docker <br>
> **Awards:** 🏆 **제13회 수원대학교 창업 경진대회 최우수상** 외 2건 수상

#### 📈 Key Achievements & Troubleshooting

- **트래픽 피크형 서비스의 운영 구조를 요청 기반 구조로 전환**
  - **문제:** 수강신청 기간처럼 짧은 피크가 중요한 서비스 특성상, `EC2 + ASG + ALB`와 상시 `ECS Fargate Service` 구조는 요청이 없는 시간에도 고정 비용이 발생
  - **해결:** 백엔드는 `API Gateway + Lambda`, 무거운 스크래핑 작업은 `SQS + EventBridge Pipe + ECS RunTask` 기반으로 분리하여 요청 중심 실행 구조로 재설계
  - **성과:** 상시 실행 인프라를 호출 기반 구조로 전환하고, 사용자 요청 흐름과 긴 작업 실행 경계를 분리
  - **Blog:** [트래픽 피크형 서비스의 운영 구조를 요청 기반 구조로 바꾼 과정](https://velog.io/@pp8817/트래픽-피크형-서비스의-운영-구조를-요청-기반-구조로-바꾼-과정)

- **EC2에서 Lambda로 옮기며 백엔드 실행 경계 재설계**
  - **문제:** Lambda 전환 이후에도 서버형 애플리케이션의 내부 async, scheduler, callback 처리 전제를 일부 유지하면서 timeout과 후처리 실패가 발생
  - **해결:** SQS 발행은 Lambda 요청 경로 안에서 확정하고, 주기 작업은 Spring 내부 scheduler 대신 EventBridge Scheduler의 Lambda 직접 호출로 이전
  - **성과:** Lambda 내부 in-memory 실행에 숨어 있던 실패 지점을 DB 상태, SQS 메시지, S3 결과, Scheduler 로그로 분리해 관측 가능하게 개선
  - **Blog:** [EC2에서 Lambda로 옮기며 백엔드 실행 경계를 다시 설계한 과정](https://velog.io/@pp8817/척척학사-EC2에서-Lambda로-옮기며-백엔드-실행-경계를-다시-설계한-과정)

- **외부 포털 연동 단일 트랜잭션 구조 해체 및 비동기 상태 머신 기반 재설계 (성공률 0% → 100%)**
  - **문제:** 외부 I/O(7s), DB 동기화(16s)를 단일 트랜잭션으로 묶어 약 23초간 DB 커넥션을 독점하는 병목 식별
  - **해결:** 트랜잭션을 변경 최소 단위로 재정의하고, 외부 I/O와 비즈니스 프로세스를 분리한 **비동기 상태 관리 구조** 도입
  - **성과:** 외부 포털 지연 상황에서도 **성공률 100% 달성** 및 커넥션 대기 시간(p95) **90% 개선 (5s → 0.5s)**
  - **Blog:** [DB 커넥션 23초 점유 해결: 비동기 상태 머신으로 가용성 100% 확보하기](https://velog.io/@pp8817/트랜잭션의-감옥에서-벗어나기)

- **포털 연동 처리 시간 개선 (16s → 0.83s)**
  - **문제:** 포털 연동 이후 내부 데이터 반영 과정에서 약 16초의 지연 발생
  - **해결:** 구간별 계측으로 반복적인 `getOrCreate` DB 왕복과 `StudentCourse INSERT` 병목을 분리하고, bulk 조회/삽입 및 JDBC batch 적용
  - **성과:** 사용자 체감 처리 시간을 약 **16초에서 0.83초로 94.8% 개선**
  - **Blog:** [포털 연동 과정 16초를 0.8초로 94.8% 개선한 과정](https://velog.io/@pp8817/척척학사-포털-연동-과정-16초를-0.8초로-94.8-개선한-과정)

- **복잡한 졸업 요건 계산 로직의 DB 의존 구조 해소 및 애플리케이션 주도 재설계 (891ms → 32ms)**
  - **문제:** 졸업 요건 조회, 수강 이력 추출, 최종 집계를 하나의 거대 CTE(Common Table Expression) 쿼리로 처리하던 구조 식별
  - **해결:** 거대 SQL을 ‘졸업 요건 조회 → 수강 이력 조회 → 애플리케이션 집계’의 3단계 책임 분리 구조로 재설계하고, 단계별 캐싱 도입
  - **성과:** API 응답 시간을 891ms에서 32ms로 약 **96% 단축**
  - **Blog:** [거대 SQL(CTE)에서 애플리케이션 조합으로의 전환](https://velog.io/@pp8817/God-Query-해체-분석-척척학사)

- **저사양 환경(t3.micro) 성능 최적화 (7 TPS → 96 TPS)**
  - **문제:** API 부하 테스트 시 10 TPS에서 응답 지연(20s+) 및 시스템 붕괴 발생
  - **해결:** 병목 구간인 인증 필터의 반복 DB 접근을 식별하고, **Local Cache(Caffeine)** 도입 및 HikariCP 튜닝 적용
  - **성과:** 처리량 **13배 개선** (7 TPS → 96 TPS) 및 병목 지점을 CPU/Heap 한계까지 이동
  - **Blog:** [1.Baseline 수립](https://velog.io/@pp8817/척척학사-t3.micro-서버의-한계-측정-7-TPS는-버티고-10-TPS는-왜-무너졌나) / [2.캐시 전략 검증](https://velog.io/@pp8817/척척학사-Redis-vs-Local-Cache-t3.micro에서-캐시는-어디까지-의미가-있을까) / [3.핵심 병목 제거](https://velog.io/@pp8817/척척학사-인증-필터-캐시-적용으로-병목은-사라졌을까)

#### 🔎 Related Deep Dives

- **Serverless & Traffic**
  - [Lambda 서버리스 전환 후 처리량 한계 분석](https://velog.io/@pp8817/척척학사-Lambda-서버리스-전환-후-처리량-한계-분석): Lambda 전환 이후 reserved concurrency, ramping 부하 패턴, DB 보호 관점에서 처리량 한계를 분석한 기록
  - [트래픽이 몰리는 서비스는 어떻게 버텨야 할까](https://velog.io/@pp8817/척척학사-트래픽이-몰리는-서비스는-어떻게-버텨야-할까-서버-장애-대응): ALB와 Auto Scaling Group 기반으로 피크 트래픽 대응 구조를 설계한 기록

- **Operations & Observability**
  - [ELK → Grafana Loki 전환기](https://velog.io/@pp8817/척척학사-로그-시스템-리빌드-ELK-Grafana-Loki): 로그 검색 패턴과 비용을 기준으로 모니터링 스택을 경량화한 기록
  - [Terraform 비용 최적화 전략](https://velog.io/@pp8817/DevOps-Terraform으로-AWS-계정-간-인프라를-재현-가능하게-만들기): AWS 인프라를 코드로 재현 가능하게 만들고 비용 발생 시점을 통제한 기록
  - [Supabase DB 커넥션 병목 원인 규명](https://velog.io/@pp8817/트러블슈팅-DB-커넥션이-텅-비었는데-꽉-찼다고-Supabase-Max-client-connections-에러): 실제 커넥션 수와 PgBouncer 모드 차이를 추적해 장애 원인을 확인한 기록

---

### 💬 [SUCAT](https://github.com/Suwon-University-Community-SUCAT/Sucat-BE-Server): 수원대학교 교내 커뮤니티 (실시간 채팅/게임/친구)
> **Role:** 백엔드 팀장 | **Period:** 2024.05 ~ 2024.11 <br>
> **Stack:** Java, Spring Boot, WebSocket, MySQL, Redis, AWS

- **실시간 통신:** WebSocket과 STOMP 프로토콜을 활용하여 채팅 및 게임 데이터의 실시간 동기화 구현
- **확장성 고려:** 단일 서버의 한계를 고려하여 Redis Pub/Sub 기반의 메시지 브로커 구조 설계 및 적용

---

## 🧾 Certificates & Awards

**Certificates**
- **AWS Certified Solutions Architect - Associate (SAA-C03)** | 2024.12
- **SQLD (SQL Developer)** | 2024.06
- **TOEIC Speaking (Intermediate High)** | 2025.12

**Awards**
- **2026** | IT 연합 동아리 YAPP 27기 성과공유회 **최우수상**
- **2026** | AI-SW Developers 공모전 4기 **최우수상**
- **2025** | 수원대학교 창업 경진대회 제13회 **최우수상**
- **2025** | 수원대학교 창업 경진대회 제12회 **우수상**
- **2025** | AI-SW Developers 공모전 3기 **우수상**
