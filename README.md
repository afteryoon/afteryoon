<div align="center">

# afteryoon.

**Backend Engineer · Java / Spring → TypeScript · AI 워크플로 설계**

서버 쪽 일을 좋아하는 백엔드 엔지니어입니다.  
요즘은 AI를 "붙이는" 것보다, **믿고 맡길 수 있게 울타리를 치는 일**에 시간을 가장 많이 씁니다.

[![Velog](https://img.shields.io/badge/Velog-20C997?style=flat-square&logo=velog&logoColor=white)](https://velog.io/@afteryoon)
[![Solved.ac](https://img.shields.io/badge/Solved.ac-Profile-blue?style=flat-square)](https://solved.ac/khsso10)

</div>

---

## 🙋 About Me

Java/Spring으로 API와 DB를 다루며 시작했고, 비개발자 인터뷰 → 요구사항 정리 → 구현까지 혼자 이어서 해 본 경험이 제 기본기입니다.
올해 하반기부터는 회사 안에서 쓰는 AI 콘텐츠 도구를 직접 기획하고 만들고 있습니다. 모델이 글과 영상을 만들어 주는 건 쉬운데, 그걸 **사람이 검수하고, 규정에 맞고, 사고 없이 게시되도록** 만드는 부분이 진짜 일이라는 걸 배우는 중입니다.

| | |
|---|---|
| ⚙️ **Backend** | Spring Boot REST API, JPA / MyBatis. 최근엔 NestJS + PostgreSQL로 넓혔습니다 |
| 🤖 **AI 활용** | 프롬프트 설계, 에이전트 역할 분담, "AI가 못 하게 막는 것"의 설계 |
| 🧹 **데이터 정제** | 원문을 먼저 정제해서 DB에 쌓고, 운영 중에는 모델을 부르지 않는 구조 |
| 🧭 **기획 → 구현** | 결정은 문서로 남기고, 구현은 테스트로 고정합니다 |

---

## 🧪 지금 만들고 있는 것들

### 콘텐츠 생성·게시 관리 시스템 (사내용, 비공개)
기획부터 DB, 서버, 화면까지 한 사람이 끌고 가는 가장 큰 프로젝트입니다.
AI가 만든 글·카드뉴스·만화를 **사람이 보고 승인해야만** SNS에 나가도록 만든 관리 도구예요.

- **NestJS + Next.js + PostgreSQL**, 공용 규칙은 별도 패키지로 빼서 서버와 화면이 같은 기준을 씁니다
- 발행 달력의 규칙(쉬는 날, 밀리면 뒤로 연쇄 이동, 연재 순서)을 **서버의 순수 함수**로 만들어 테스트로 고정했습니다
- 자동 게시 스케줄러는 **기본값을 꺼짐**으로 두고, 켜는 건 사람이 합니다
- 마이그레이션 27개, 테스트 파일 780여 개, API 경로 200여 개. 커밋은 800개를 넘겼습니다

**데이터 정제**가 이 프로젝트의 핵심 아이디어였습니다. 운영 중에 모델을 계속 부르면 비용도 품질도 흔들려서, 반대로 갔습니다.
원문을 상위 에이전트가 **미리 정제 → DB에 적재 → 운영에서는 불러다 쓰기만** 하는 방식이고, 만화 소재는 운영 단계 모델 호출을 0으로 만들었습니다. 원문을 얼마나 재사용해도 되는지는 등급 4단계 규칙으로 나눠 두었고, 게시되지 않은 버전은 보관 기간이 지나면 정리하는 배치도 같이 설계했습니다.

### HR 마케팅 영상 제작 파이프라인 (사내용, 비공개)
주제 → 대본 → 장면 → 클립 → 음성·자막 → **사람 승인** → 유튜브 비공개 업로드까지 이어지는 Python(FastAPI) 파이프라인입니다.
자동 승인과 자동 공개 업로드는 일부러 만들지 않았습니다.

- 대본은 2단계로 확정한 뒤에 장면을 만듭니다. 한 번에 다 만들면 틀린 곳을 찾기가 어려웠습니다
- **규제 요건을 한곳에 모았습니다.** AI 생성물 고지(표시 설정, 설명란 첫 줄, 영상 시작 구간)와 근거 없는 1인칭 체험담 표현 검출을 하나의 기준 모듈이 맡고, 어디서 만들든 같은 검사를 지나가게 했습니다
- 법률 검토 의견은 문서로 보관하고, 코드의 기준과 문서가 어긋나지 않게 맞춰 둡니다
- 제작하다 터진 문제는 규칙 로그에 쌓아서 다음 프롬프트에 자동으로 반영되도록 했습니다

### 에이전트 관제실 (개인용 로컬 앱)
Claude Code 세션을 여러 개 병렬로 돌리다 보니 "어느 세션이 지금 내 결정을 기다리고 있지?"가 안 보였습니다. 그래서 만들었어요.
세션 상태, 결정 대기, 일정을 한 화면에 모아 보는 **읽기 전용** 앱이고, 내 컴퓨터 안(127.0.0.1)에서만 열립니다. 비밀값은 키체인에 두고, 서버나 DB에는 쓰지 않는다는 원칙을 처음부터 못 박았습니다. Next.js 16 / React 19 / TypeScript로 만들었고 커밋 140여 개입니다.

---

## 🧰 AI를 쓰는 방식

도구를 많이 쓰는 것보다 **일하는 구조**를 정하는 쪽에 공을 들입니다.

**1. 에이전트도 조직처럼 굴립니다 (ensemble)**
오너 → PM → 부서 리더 → 실무 노드 순으로 책임을 나누고, 리더가 1차 검수한 뒤에만 위로 보고합니다. 막힐 때만 상위 모델에게 자문을 구하고, 같은 방향으로 맴도는 에이전트는 세션을 유지하지 않고 교체합니다. 조직 상태는 대화가 아니라 **파일**에 남겨서 세션이 끊겨도 이어집니다.

**2. 반복되는 노하우는 스킬로 만듭니다 (company-hub)**
프로젝트마다 같은 실수를 반복하는 게 싫어서, 공통 스킬 20개와 에이전트 11개를 단일 원본 저장소로 관리하고 기기 간에 동기화합니다. 그중 제가 가장 아끼는 것들이에요.

- `llm-io-security-audit`: 프롬프트로 들어가는 값과 모델이 내놓은 값을 **실제 호출 없이** 점검합니다. 프롬프트 주입, 위험한 출력값, 로그 유출을 시험으로 고정합니다
- `llm-response-replay-corpus`: 모델 응답을 파일로 모아 두고 파서·검증기를 다시 돌려 봅니다. 유료 호출 전에 구멍부터 찾을 수 있습니다
- `verify-sources`: 두 검증자가 서로의 조사 결과를 블라인드로 다시 확인합니다. 출처가 틀린 자료가 콘텐츠에 섞이는 걸 막으려고 만들었습니다
- `staged-publisher-fake-fetch-testing`: 인스타그램·페이스북·X처럼 단계가 나뉜 게시 API를 가짜 서버로 시험합니다. "게시 직전 단계"와 "끊겼을 때 재호출 금지"까지 확인합니다
- `db-seed-reset-rehearsal`: DB 시드를 넣고 되돌리는 연습을 먼저 해 봅니다

광고 심의나 법무 같은 **규제 규칙은 아직 스킬로 옮기는 중**입니다. 영상 파이프라인에서 코드로 굳힌 기준을 일반화하는 게 다음 숙제예요.

**3. 모델을 믿기보다 막다른 길을 먼저 만듭니다**
모델이 쓴 문장은 항상 틀릴 수 있다고 가정하고, 사람 승인 단계, 꺼진 채로 시작하는 자동화, 호출 전 가드를 먼저 놓고 기능을 얹습니다.

---

## 🛠 Tech Stack

**Languages**  
![Java](https://img.shields.io/badge/Java-007396?style=flat-square&logo=openjdk&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

**Frameworks**  
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![JPA](https://img.shields.io/badge/JPA-59666C?style=flat-square&logo=hibernate&logoColor=white)
![MyBatis](https://img.shields.io/badge/MyBatis-000000?style=flat-square)

**Databases**  
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Oracle](https://img.shields.io/badge/Oracle-F80000?style=flat-square&logo=oracle&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

**AI & Tools**  
![Claude Code](https://img.shields.io/badge/Claude_Code-D97757?style=flat-square&logo=anthropic&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=flat-square&logo=googlecloud&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)

---

## 📊 Stats

<div align="center">
  <img height="160" src="https://github-readme-stats.vercel.app/api/top-langs/?username=afteryoon&layout=compact&langs_count=6&theme=default&hide_border=true" />
  &nbsp;
  <a href="https://solved.ac/khsso10">
    <img height="160" src="http://mazassumnida.wtf/api/v2/generate_badge?boj=khsso10" />
  </a>
</div>

> 위 프로젝트들은 회사 내부용이라 저장소가 비공개입니다. 구조나 설계 이야기가 궁금하시면 편하게 물어봐 주세요.

---

## 📝 Blog Posts

<!-- BLOG-POST-LIST:START -->
<!-- BLOG-POST-LIST:END -->

<div align="center">

[![Velog's GitHub stats](https://velog-readme-stats.vercel.app/api/list?name=afteryoon)](https://velog.io/@afteryoon)

</div>
