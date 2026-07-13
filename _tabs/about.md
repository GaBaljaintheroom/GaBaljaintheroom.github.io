---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

## 박준수 (Junsu Park)
**Backend Developer**

📞 010-2742-3364 &nbsp;|&nbsp; ✉️ junsu1222@naver.com  
🐙 GitHub: [GaBaljaintheroom](https://github.com/GaBaljaintheroom) &nbsp;|&nbsp; 📝 Blog: [github.io](https://gabaljaintheroom.github.io)

사내 시스템의 문제를 스스로 발견하고 개선하는 것을 중요하게 생각하는 개발자입니다.

---

## 경력

### 참좋은여행 · Software Engineer (2025.04 ~ 진행중)
`#JAVA` `#Spring Boot` `#Mybatis` `#MSSQL` `#ELK` `#Jenkins`

> 여행사 Full Stack 개발자로서 400명의 임직원이 사용하는 ERP/백오피스 시스템의 개발, 운영 및 고도화 업무를 수행하고 있습니다.

**ERP 개인정보 마스킹 설계**
- ISMS 개인정보 보호 요구사항에 맞춰 ERP 274개 메뉴의 고객 개인정보를 일관되게 마스킹하는 구조 설계
- Jackson 직렬화 과정에서 커스텀 어노테이션 기반 공통 마스킹 정책을 적용하여 API별 마스킹 자동화
- Response Object의 필드 메타데이터를 ConcurrentHashMap으로 캐싱하여 직렬화 성능 최적화
- **성과**
  - Locust 부하테스트를 통해 마스킹 적용 전후 API 응답 성능을 검증하고 기존 API 수준의 성능 유지 확인
  - 신규 API 개발 시 커스텀 어노테이션 적용만으로 개인정보 마스킹이 적용되어 개발 생산성 및 유지보수성 향상

**신한은행 최초 고시 환율 배치 시스템 개발**
- 재무회계팀이 최초 고시 환율을 ERP 내 수동 입력하는 방식으로 운영되어 업무 효율 저하 및 입력 오류 가능성 존재
- 신한은행 Open API 연동 및 UPSERT 기반 환율 데이터 DB 적재 프로세스를 Jenkins 스케줄러로 자동화
- API 호출 실패 및 예외 발생 시 SMTP 장애 알림 메일을 발송하고 수동 입력 절차를 마련하여 운영 안정성 확보
- **성과**
  - 재무회계팀의 최초 고시 환율 수동 입력 업무를 일 1회 → 0회로 제거하여 반복 업무 자동화

**장애 탐지 향상을 위한 에러 알림 자동화**
- 토큰 만료 등 비장애성 오류가 하루 약 1만 건 발생하는 환경에서 운영자의 장애 탐지 효율 개선 필요
- ELK Stack 기반 로그 분석 및 장애 탐지 프로세스를 구축하여 5분 내 동일 예외 10회 이상 발생 시 Slack 알림 자동화
- 노이즈성 알림을 필터링하고 실제 장애를 우선 식별할 수 있는 모니터링 체계 구축
- **성과**
  - 운영자가 전체 로그를 수동 확인하는 방식에서 주요 장애만 선별 알림받는 체계로 개선
  - 장애 인지 시간(MTTD) 약 1시간 → 5분으로 감소

**대용량 데이터 조회로 인한 OOM 장애 개선**
- JVM Heap Dump 분석을 통해 MyBatis 조회 과정에서 약 570만 건의 데이터가 메모리에 적재되는 문제를 발견
- SQL 실행 계획 분석을 통해 약 2,700만 건 규모의 Full Table Scan 발생 원인을 식별
- 조회 조건 및 SQL을 개선하여 Full Scan을 제거하고 OOM 장애를 해결

---

## 프로젝트

### 사외업무 시스템 (2025.08 ~ 2026.03)

> 영업팀과 가이드, 인솔자가 수배서(인보이스)를 기반으로 여행 출발 전 숙소, 교통비를 협의하고 확정하는 업무 협업 시스템입니다.

**.NET 기반 레거시 시스템 Spring Boot · Next.js 재구축**
- .NET 기반 사외업무 시스템을 Spring Boot · Next.js로 재구축하며 수배서 협의 및 확정 비즈니스 프로세스를 Full Stack으로 마이그레이션
- OpenAPI(Swagger) 기반 DTO 자동 생성 환경을 구축하여 프론트엔드 타입 정의를 자동화하고 API 스펙과의 일관성을 확보
- JUnit5, Mockito, AssertJ 기반 단위 테스트를 도입하여 테스트 커버리지를 0% → 65%까지 향상시키고 코드 변경에 대한 안정성을 강화

**토큰 기반 인증 도입 및 암호화 알고리즘 고도화**
- 인증 및 암호화 체계를 통일하기 위해 세션 기반을 JWT 기반으로 전환하고, SHA-1 암호화를 SHA-512 + Salt 방식으로 개선
- 기존 사용자는 로그인 시 자동으로 신규 암호화 방식으로 전환되도록 점진적 마이그레이션을 구현
- 사용자 비밀번호 재설정 없이 기존 계정을 유지하면서 인증 체계와 보안 수준을 향상

**다운타임 제거를 위한 Blue-Green 배포 환경 구축**
- 기존 배포 방식은 애플리케이션 재기동 과정에서 다운타임이 발생하여 사용자 요청이 실패할 수 있는 문제 존재
- 온프레미스 환경에 적합한 배포 전략으로 Nginx Reverse Proxy와 Docker를 활용한 Blue-Green 배포를 적용
- 무중단 배포와 신속한 롤백이 가능한 운영 환경을 구축하여 배포 안정성과 서비스 가용성을 향상

---

## 활동

**개인 서비스**
- [기술 블로그 요약 슬랙 봇](https://github.com/GaBaljaintheroom/bloblo-public): IT 기술 블로그를 자동으로 수집하고, Ollama AI로 요약하여 Slack으로 전송하는 알림 봇

**오픈소스 기여**
- Spring-Batch: [Upgrade Testcontainers from 1.21.3 to 2.0.3](https://github.com/spring-projects/spring-batch/pull/5348)

**커뮤니티 & 봉사활동**
- `2026.03 ~ 2026.07` SIPE 현직자 동아리 회원 참여
- `2024.09 ~ 2025.03` YAPP IT 동아리 25기 Server 파트 운영진 참여
- `2024.05 ~ 2024.09` YAPP IT 동아리 24기 Server 파트 참여
- `2024.04 ~ 2024.07` 코드클럽 SW 교육기부단 초등부 대상 Scratch 교육 봉사활동 참여
- `2023.02 ~ 2025.03` 글또 8, 9, 10기 IT 개발 블로깅 공유 커뮤니티 참여

---

## 자격증 & 수상내역
- SQLD
- AWS Certified Cloud Practitioner
- 정보처리기사
- 컴퓨터활용능력 1급

---

## 교육
- 한국공학대학교 컴퓨터공학과 소프트웨어학부 학사 (2019.03 ~ 2025.08)
