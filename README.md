# Backend Developer, 박상민

**사용자 경험을 지탱하는 견고한 인프라와 서버를 설계합니다.** <br>
비즈니스 로직 구현을 넘어, 안정적인 서비스 운영을 위한 아키텍처 설계에 관심이 많습니다. <br>

<div align="left">
  <a href="https://docs.google.com/document/d/1ocVEA9Xrdy9ZU2CZ-eVPX09A7GbpnjQuTFhHyOqKPns/edit?usp=sharing"><img src="https://img.shields.io/badge/Resume-Google%20Docs-4285F4?style=for-the-badge&logo=google-docs&logoColor=white"/></a>
  <a href="https://velog.io/@pp8817/posts"><img src="https://img.shields.io/badge/Tech%20Blog-velog-11B57D?style=for-the-badge&logo=velog&logoColor=white"/></a>
  <a href="mailto:pp8817@naver.com"><img src="https://img.shields.io/badge/Mail-pp8817%40naver.com-03C75A?style=for-the-badge&logo=naver&logoColor=white"/></a>
</div>

<br>

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=pp8817&bg_color=180,ffffff,00000000&title_color=000000&text_color=000000" />
  <img src="http://mazassumnida.wtf/api/v2/generate_badge?boj=pp8817" />
</div>

## 💼 Experience
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

- **외부 포털 연동 단일 트랜잭션 구조 해체 및 비동기 상태 머신 기반 재설계 (성공률 0% → 100%)**
  - **문제:** 외부 I/O(7s), DB 동기화(16s)를 단일 트랜잭션으로 묶어 약 23초간 DB 커넥션을 독점하는 병목 식별
  - **해결:** 트랜잭션을 변경 최소 단위로 재정의하고, 외부 I/O와 비즈니스 프로세스를 분리한 **비동기 아키텍처 도입**
  - **성과:** 외부 포털 지연 상황에서도 **에러율 0% 달성** 및 커넥션 대기 시간(p95) **90% 개선 (5s → 0.5s)**
  - **Blog:** [DB 커넥션 23초 점유 해결: 비동기 상태 머신으로 가용성 100% 확보하기](https://velog.io/@pp8817/트랜잭션의-감옥에서-벗어나기)

- **복잡한 졸업 요건 계산 로직의 DB 의존 구조 해소 및 애플리케이션 주도 재설계 (891ms → 32ms)**
  - **문제:** 졸업 요건 조회, 수강 이력 추출, 최종 집계를 하나의 거대 CTE(Common Table Expression) 쿼리로 처리하던 구조 식별
  - **해결:** 거대 SQL을 ‘졸업 요건 조회 → 수강 이력 조회 → 애플리케이션 집계’의 3단계 책임 분리 구조로 재설계, 단계별 캐싱 도입
  - **성과:** API 응답 시간을 891ms에서 32ms로 약 **96% 단축**
  - **Blog:** [거대 SQL(CTE)에서 애플리케이션 조합으로의 전환](https://velog.io/@pp8817/God-Query-해체-분석-척척학사)

- **저사양 환경(t3.micro) 성능 최적화 (7 TPS → 96 TPS)**
  - **문제:** API 부하 테스트 시 10 TPS에서 응답 지연(20s+) 및 시스템 붕괴 발생
  - **해결:** 병목 구간인 '인증 필터 DB 접근'을 식별하여 **Local Cache(Caffeine)** 도입 및 HikariCP 튜닝
  - **성과:** 처리량 **13배 개선** (7 TPS → 96 TPS) 및 병목 지점을 CPU/Heap 한계까지 이동시킴
  - **Blog:** [1.Baseline 수립](https://velog.io/@pp8817/척척학사-t3.micro-서버의-한계-측정-7-TPS는-버티고-10-TPS는-왜-무너졌나) / [2.캐시 전략 검증](https://velog.io/@pp8817/척척학사-Redis-vs-Local-Cache-t3.micro에서-캐시는-어디까지-의미가-있을까) / [3.핵심 병목 제거](https://velog.io/@pp8817/척척학사-인증-필터-캐시-적용으로-병목은-사라졌을까)

- **트래픽 폭주 대응 고가용성 아키텍처 (ALB + ASG)**
  - **문제:** 수강신청 기간 평시 대비 **20배 트래픽 스파이크** 발생, 단일 서버 CPU 크레딧 고갈
  - **해결:** **ALB(L7) + Auto Scaling Group** 기반의 탄력적 아키텍처 전환
  - **성과:** 가용성 99.9% 확보 (에러율 10% → 0.1% 미만), 인프라 비용 **85% 절감** ($66 → $10)
  - **Blog:** [트래픽 폭주 대응 아키텍처 구축](https://velog.io/@pp8817/척척학사-트래픽이-몰리는-서비스는-어떻게-버텨야-할까-서버-장애-대응)

- **로그 모니터링 스택 경량화 (ELK → Grafana Loki)**
  - **문제:** ELK 스택의 과도한 메모리 점유(5GB+)로 인한 고사양 인스턴스 강제 사용 비효율
  - **해결:** 검색 빈도가 낮은 로그 특성을 반영하여 **Grafana Loki + Sentry** 조합으로 재설계
  - **성과:** 메모리 사용량 **80% 감소** 및 월 인프라 비용 **87% 절감** ($60 → $7.5)
  - **Blog:** [ELK → Grafana Loki 전환기](https://velog.io/@pp8817/척척학사-로그-시스템-리빌드-ELK-Grafana-Loki)

- **Cloud DB 연결 병목 트러블슈팅 (Supabase)**
  - **문제:** 활성 커넥션이 여유로움에도 `Max client connections reached` 에러 발생
  - **해결:** Supabase Free Plan의 PgBouncer 모드를 Transaction(Limit 15)에서 **Session(Direct, Limit 60)** 방식으로 전환
  - **성과:** 가용 커넥션 수 **4배 확장** 및 장애 해결
  - **Blog:** [DB 커넥션 병목 원인 규명](https://velog.io/@pp8817/트러블슈팅-DB-커넥션이-텅-비었는데-꽉-찼다고-Supabase-Max-client-connections-에러)

- **Terraform 기반 인프라 재현성 확보 및 비용 최적화**
  - **문제:** 콘솔 중심의 수동 관리로 인한 계정 종속성 및 비용 통제 어려움
  - **해결:** **Terraform(IaC)** 도입으로 인프라 코드로 관리, 비용 발생 시점 통제 전략 수립
  - **성과:** 계정 간 이식성 확보 및 월 비용 **57% 절감** ($127 → $54)
  - **Blog:** [Terraform 비용 최적화 전략](https://velog.io/@pp8817/DevOps-Terraform으로-AWS-계정-간-인프라를-재현-가능하게-만들기)

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
- **2026** | AI-SW Developers 공모전 4기 **최우수상**
- **2025** | 수원대학교 창업 경진대회 제13회 **최우수상**
- **2025** | 수원대학교 창업 경진대회 제12회 **우수상**
- **2025** | AI-SW Developers 공모전 3기 **우수상**
