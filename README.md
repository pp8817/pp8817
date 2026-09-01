# Backend Developer, 박상민

응답 시간과 운영 비용은 숫자로 확인하고, 장애는 로그와 재현 가능한 근거로 좁혀 갑니다.

Java와 Spring Boot를 중심으로 백엔드를 개발합니다. 최근에는 Python 기반 AI 서비스와 AWS 인프라까지 함께 다루고 있습니다.

<div align="left">
  <a href="https://docs.google.com/document/d/1ocVEA9Xrdy9ZU2CZ-eVPX09A7GbpnjQuTFhHyOqKPns/edit?usp=sharing"><img src="https://img.shields.io/badge/Resume-Google%20Docs-4285F4?style=for-the-badge&logo=google-docs&logoColor=white"/></a>
  <a href="https://velog.io/@pp8817/posts"><img src="https://img.shields.io/badge/Tech%20Blog-velog-11B57D?style=for-the-badge&logo=velog&logoColor=white"/></a>
  <a href="mailto:pp8817@naver.com"><img src="https://img.shields.io/badge/Mail-pp8817%40naver.com-03C75A?style=for-the-badge&logo=naver&logoColor=white"/></a>
</div>

## Selected Impact

- <strong>누적 가입자 <code>7,000명</code>, MAU 약 <code>4,000명</code></strong>의 서비스 기획, 백엔드 개발, 운영 (2026.08 기준)
- <strong>상시 실행 인프라를 요청 기반 구조로 전환</strong>해 월 비용 추정치를 <strong><code>$110.98 → $3.79~$20.79</code></strong>로 낮춤
- 인증 필터의 요청당 DB 조회를 제거해 k6 안정성 테스트를 <strong>성공률 <code>99.99%</code>, p95 <code>91ms</code></strong>로 완주
- <strong>외부 포털 7초 지연과 50 VU를 재현한 부하 테스트</strong>에서 요청 수락 성공률을 <strong><code>0% → 100%</code></strong>로 높이고, 커넥션 획득 대기 피크를 <strong><code>5s → 약 0.5s</code></strong>로 단축

## Experience

- <strong>AISW Maestro 17기</strong> | 2026.04 ~ 현재
  - AI 영어 회화 학습 서비스 Landit 기획, 개발, 운영
- <strong>YAPP 27기 Server Developer</strong> | 2025.11 ~ 2026.03
  - Moit, Weddin 개발
  - YAPP 27기 성과공유회 최우수상

## Projects

### Landit | AI 영어 회화 학습 서비스

> <strong>기간:</strong> 2026.04 ~ 현재 | <strong>출시:</strong> 2026.07, App Store / Google Play  
> <strong>담당:</strong> Backend / AI / Infrastructure  
> <strong>기술:</strong> Java, Spring Boot, Python, PostgreSQL, AWS, Terraform

Service: [App Store](https://apps.apple.com/us/app/landit-%EB%9E%9C%EB%94%A7-%EC%9B%90%EC%96%B4%EB%AF%BC%EC%97%90%EA%B2%8C-%ED%86%B5%ED%95%98%EB%8A%94-%EC%98%81%EC%96%B4-%EC%8A%A4%ED%94%BC%ED%82%B9/id6787414201) | [Google Play](https://play.google.com/store/apps/details?id=com.saynow.app)

Repositories: [Backend](https://github.com/Aragornnnnnn/landit-be) | [AI](https://github.com/Aragornnnnnn/landit-ai) | [Infrastructure](https://github.com/Aragornnnnnn/landit-iac)

- <strong>Backend API, AI 응답 생성, 인프라 설정</strong>이 맞물리는 지점을 함께 관리했습니다.
- <strong>Sentry 이벤트와 실제 응답을 함께 추적</strong>해 AI 응답 검증 실패 원인을 찾고, 복구 경로를 수정한 뒤 운영 배포까지 확인했습니다.
- 장기 기억 기능은 <strong>쓰기와 사용 단계를 분리</strong>했습니다. 토큰 사용량, 지연 시간, 저장 결과를 먼저 측정한 뒤 단계적으로 적용할 수 있게 설계했습니다.
- EventBridge Scheduler, SQS, Backend Consumer로 예약 알림의 <strong>실행 경계를 분리</strong>했습니다. 스케줄 활성화 여부는 배포와 별도로 관리했습니다.

### 척척학사 | 졸업 요건 자동 비교 및 관리 서비스

> <strong>기간:</strong> 2025.02 ~ 현재  
> <strong>역할:</strong> Backend Lead  
> <strong>기술:</strong> Java, Spring Boot, PostgreSQL, Redis, Caffeine, AWS, Terraform, Docker

Service: [Web](https://www.cchaksa.com/) | [App Store](https://apps.apple.com/kr/app/%EC%B2%99%EC%B2%99%ED%95%99%EC%82%AC/id6747005390) | [Google Play](https://play.google.com/store/apps/details?id=com.kunize.uswtimetable)

Repositories: [Backend](https://github.com/cchaksa/cchaksa-backend) | [Infrastructure](https://github.com/cchaksa/cchaksa-be-terraform) | [Scraper](https://github.com/cchaksa/suwon-scraper-v1)

- 짧은 API는 `API Gateway + Lambda`, 스크래핑은 `SQS + EventBridge Pipe + ECS RunTask`로 분리해 <strong>상시 실행 비용을 사용량 기반 비용으로 전환</strong>했습니다. 월 비용 추정치는 <strong><code>$110.98 → $3.79~$20.79</code></strong>로 낮아졌습니다.
- 외부 포털 호출과 DB 반영을 단일 요청에서 분리하고 <strong>비동기 큐와 상태 머신</strong>을 도입했습니다. 외부 포털 7초 지연과 50 VU 부하 테스트에서 <strong>요청 수락 성공률 <code>0% → 100%</code></strong>, 커넥션 획득 대기 피크 <strong><code>5s → 약 0.5s</code></strong>를 확인했습니다.
- 학생 1명의 수강 이력 50건 신규 반영 경로를 계측해 건별 `getOrCreate`가 만든 반복 DB 왕복을 찾았습니다. bulk 조회와 삽입, JDBC batch를 적용해 내부 처리 시간을 <strong><code>16초 → 0.83초</code></strong>로 줄였습니다.
- 거대한 CTE 쿼리를 졸업 요건 조회, 수강 이력 조회, 애플리케이션 집계로 나눴습니다. Redis 캐시를 적용한 부하 테스트에서 졸업 요건 계산 평균 시간을 <strong><code>893ms → 32ms</code></strong>로 약 96% 줄였습니다.
- 인증 필터의 매 요청 DB 조회를 Caffeine 캐시로 제거했습니다. `maxPoolSize=3`을 유지한 k6 안정성 테스트를 <strong>성공률 <code>99.99%</code>, p95 <code>91ms</code></strong>로 완주했고, 추가 한계 테스트에서는 <strong>약 <code>100 TPS</code> 부근에서 CPU와 JVM Heap이 먼저 한계에 도달</strong>하는 것을 확인했습니다.

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

<strong>Backend</strong>
<br>
<img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Boot-6DB33F?style=for-the-badge&logo=SpringBoot&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Data JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
<img src="https://img.shields.io/badge/Spring Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>

<strong>Infrastructure & DevOps</strong>
<br>
<img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white"/>
<img src="https://img.shields.io/badge/Terraform-844FBA?style=for-the-badge&logo=terraform&logoColor=white"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white"/>
<img src="https://img.shields.io/badge/GitHub Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>

<strong>Database</strong>
<br>
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white"/>
<img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white"/>

<strong>Operations</strong>
<br>
<img src="https://img.shields.io/badge/Sentry-362D59?style=for-the-badge&logo=sentry&logoColor=white"/>
<img src="https://img.shields.io/badge/Grafana Loki-F46800?style=for-the-badge&logo=grafana&logoColor=white"/>

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
