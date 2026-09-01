# Backend Developer, 박상민

응답 시간과 운영 비용은 숫자로 확인하고, 장애는 로그와 재현 가능한 근거로 좁혀 갑니다.

Java와 Spring Boot를 중심으로 백엔드를 개발합니다. 최근에는 Python 기반 AI 서비스와 AWS 인프라까지 함께 다루고 있습니다.

<div align="left">
  <a href="https://docs.google.com/document/d/1ocVEA9Xrdy9ZU2CZ-eVPX09A7GbpnjQuTFhHyOqKPns/edit?usp=sharing"><img src="https://img.shields.io/badge/Resume-Google%20Docs-4285F4?style=for-the-badge&logo=google-docs&logoColor=white"/></a>
  <a href="https://velog.io/@pp8817/posts"><img src="https://img.shields.io/badge/Tech%20Blog-velog-11B57D?style=for-the-badge&logo=velog&logoColor=white"/></a>
  <a href="mailto:pp8817@naver.com"><img src="https://img.shields.io/badge/Mail-pp8817%40naver.com-03C75A?style=for-the-badge&logo=naver&logoColor=white"/></a>
</div>

## Selected Impact

- 누적 가입자 `7,000명`, MAU 약 `4,000명`의 서비스 기획, 백엔드 개발, 운영 (2026.08 기준)
- 피크 트래픽 구간에서 가용성 `99.9%`, 에러율 `0.1% 미만`을 유지하면서 인프라 비용 `87% 절감`
- 인프라/서버 비용을 유지하면서 API 처리량을 `7 TPS → 96 TPS`로 약 13배 개선
- 외부 포털 연동 성공률을 `0% → 100%`로 높이고 커넥션 대기 시간 p95를 `5s → 0.5s`로 단축

## Experience

- **AISW Maestro 17기** | 2026.04 ~ 현재
  - AI 영어 회화 학습 서비스 Landit 기획, 개발, 운영
- **YAPP 27기 Server Developer** | 2025.11 ~ 2026.03
  - Moit, Weddin 개발
  - YAPP 27기 성과공유회 최우수상

## Projects

### Landit | AI 영어 회화 학습 서비스

> **기간:** 2026.04 ~ 현재 | **출시:** 2026.07, App Store / Google Play  
> **담당:** Backend / AI / Infrastructure  
> **기술:** Java, Spring Boot, Python, PostgreSQL, AWS, Terraform

Service: [App Store](https://apps.apple.com/us/app/landit-%EB%9E%9C%EB%94%A7-%EC%9B%90%EC%96%B4%EB%AF%BC%EC%97%90%EA%B2%8C-%ED%86%B5%ED%95%98%EB%8A%94-%EC%98%81%EC%96%B4-%EC%8A%A4%ED%94%BC%ED%82%B9/id6787414201) | [Google Play](https://play.google.com/store/apps/details?id=com.saynow.app)

Repositories: [Backend](https://github.com/Aragornnnnnn/landit-be) | [AI](https://github.com/Aragornnnnnn/landit-ai) | [Infrastructure](https://github.com/Aragornnnnnn/landit-iac)

- Backend API, AI 응답 생성, 인프라 설정이 맞물리는 지점을 함께 관리했습니다.
- Sentry 이벤트와 실제 응답을 추적해 AI 응답 검증 실패 원인을 찾고, 복구 경로를 수정한 뒤 운영 배포까지 확인했습니다.
- 장기 기억 기능은 쓰기와 사용 단계를 분리했습니다. 토큰 사용량, 지연 시간, 저장 결과를 먼저 측정한 뒤 단계적으로 적용할 수 있게 설계했습니다.
- EventBridge Scheduler, SQS, Backend Consumer로 예약 알림 실행 경계를 나눴습니다. 스케줄 활성화 여부는 배포와 분리해 관리했습니다.

### 척척학사 | 졸업 요건 자동 비교 및 관리 서비스

> **기간:** 2025.02 ~ 현재  
> **역할:** Backend Lead  
> **기술:** Java, Spring Boot, PostgreSQL, Redis, Caffeine, AWS, Terraform, Docker

Service: [Web](https://www.cchaksa.com/) | [App Store](https://apps.apple.com/kr/app/%EC%B2%99%EC%B2%99%ED%95%99%EC%82%AC/id6747005390) | [Google Play](https://play.google.com/store/apps/details?id=com.kunize.uswtimetable)

Repositories: [Backend](https://github.com/cchaksa/cchaksa-backend) | [Infrastructure](https://github.com/cchaksa/cchaksa-be-terraform) | [Scraper](https://github.com/cchaksa/suwon-scraper-v1)

- 요청이 없을 때도 비용이 발생하던 서버 구조를 `API Gateway + Lambda` 중심으로 바꿨습니다. 오래 걸리는 스크래핑 작업은 `SQS + EventBridge Pipe + ECS RunTask`로 분리했습니다.
- 외부 포털 호출과 데이터 동기화를 하나의 트랜잭션에서 분리하고 비동기 상태 관리 구조를 도입했습니다. 연동 성공률을 `0%에서 100%`로 높이고 커넥션 대기 시간 p95를 `5s에서 0.5s`로 줄였습니다.
- 반복 조회와 INSERT 병목을 계측한 뒤 bulk 처리와 JDBC batch를 적용했습니다. 데이터 반영 시간을 `16s에서 0.83s`로 줄였습니다.
- 거대한 CTE 쿼리를 조회, 이력 추출, 애플리케이션 집계 단계로 나눴습니다. API 응답 시간은 `891ms에서 32ms`로 줄었습니다.
- 인증 필터의 반복 DB 접근을 Caffeine 캐시로 줄여 t3.micro 환경 처리량을 `7 TPS에서 96 TPS`로 높였습니다.

<details>
<summary>관련 기술 글</summary>

- [트래픽 피크형 서비스의 운영 구조를 요청 기반 구조로 바꾼 과정](https://velog.io/@pp8817/트래픽-피크형-서비스의-운영-구조를-요청-기반-구조로-바꾼-과정)
- [EC2에서 Lambda로 옮기며 백엔드 실행 경계를 다시 설계한 과정](https://velog.io/@pp8817/척척학사-EC2에서-Lambda로-옮기며-백엔드-실행-경계를-다시-설계한-과정)
- [DB 커넥션 23초 점유 해결](https://velog.io/@pp8817/트랜잭션의-감옥에서-벗어나기)
- [포털 연동 과정 16초를 0.8초로 줄인 과정](https://velog.io/@pp8817/척척학사-포털-연동-과정-16초를-0.8초로-94.8-개선한-과정)
- [거대 SQL에서 애플리케이션 조합으로 전환한 과정](https://velog.io/@pp8817/God-Query-해체-분석-척척학사)
- t3.micro 성능 개선 기록
  - [1. Baseline 수립](https://velog.io/@pp8817/척척학사-t3.micro-서버의-한계-측정-7-TPS는-버티고-10-TPS는-왜-무너졌나)
  - [2. 캐시 전략 검증](https://velog.io/@pp8817/척척학사-Redis-vs-Local-Cache-t3.micro에서-캐시는-어디까지-의미가-있을까)
  - [3. 핵심 병목 제거](https://velog.io/@pp8817/척척학사-인증-필터-캐시-적용으로-병목은-사라졌을까)

</details>

## Tech Stack

**Backend**
<br>
<img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Boot-6DB33F?style=for-the-badge&logo=SpringBoot&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Data JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>

**Infrastructure & DevOps**
<br>
<img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white"/>
<img src="https://img.shields.io/badge/Terraform-844FBA?style=for-the-badge&logo=terraform&logoColor=white"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white"/>
<img src="https://img.shields.io/badge/GitHub Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>

**Database**
<br>
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white"/>
<img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white"/>

**Operations**
<br>
<img src="https://img.shields.io/badge/Sentry-362D59?style=for-the-badge&logo=sentry&logoColor=white"/>
<img src="https://img.shields.io/badge/Grafana Loki-F46800?style=for-the-badge&logo=grafana&logoColor=white"/>

## Certificates

- AWS Certified Solutions Architect - Associate | 2024.12
- SQLD | 2024.06
- TOEIC Speaking Intermediate High | 2025.12

## Awards

- **2026** | YAPP 27기 성과공유회 최우수상
- **2026** | AI-SW Developers 공모전 4기 최우수상
- **2025** | 수원대학교 창업 경진대회 제13회 최우수상
- **2025** | 수원대학교 창업 경진대회 제12회 우수상
- **2025** | AI-SW Developers 공모전 3기 우수상
