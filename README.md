

# 🏀 Court-Kok (코트콕)

<img width="294" height="295" alt="Image" src="https://github.com/user-attachments/assets/2793310a-08af-4d96-bb78-3bedff8c4fc2" />

> 농구 예약을 간단하게, 즐겁게\!

**Court-Kok**은 함께 농구 할 사람을 찾기 어려운 문제를 해결하고, 간편하게 코트를 예약하며 사람들을 모을 수 있는 실시간 농구 매칭 서비스입니다.

## 개요
| 구분 | 내용 |
| :--- | :--- |
| **프로젝트명** | Court-Kok (코트콕) |
| **개발 기간** | **2025.09.01 ~ 2025.09.04** |
| **팀 구성** | 권동민,권동하,유선목|
| **주요 기술** | Flask, MongoDB, Docker, AWS, WebSocket |

## 🌟 주요 기능

  - **회원가입 및 로그인**: JWT 기반의 안전한 인증 시스템을 통해 서비스를 이용할 수 있습니다.
  - **실시간 예약 시스템**: 월간 달력과 일일 스케줄 뷰를 통해 원하는 날짜와 시간을 직관적으로 선택하고 예약할 수 있습니다.
  - **간편한 모임 생성**: 최소/최대 인원, 진행 시간 등 상세 조건을 설정하여 농구 모임을 손쉽게 만들 수 있습니다.
  - **실시간 알림**: WebSocket을 활용하여 모임 생성, 취소, 인원 마감 등 변동 사항을 웹과 이메일로 실시간 알림을 받습니다.
  - **나의 예약 관리**: 내가 만들거나 참여한 모임의 목록과 참여자 정보를 한눈에 확인하고 관리할 수 있습니다.
  - **마이페이지**: 개인 정보를 확인하고 수정할 수 있습니다.

## 🖼️ 서비스 화면

| 로그인 | 회원가입 | 메인 페이지 (예약) |
| :---: | :---: | :---: |
| <img width="222" height="382" alt="Image" src="https://github.com/user-attachments/assets/1d6ac47c-4f99-4aa9-9cda-680fc6ed011a" /> |<img width="194" height="382" alt="Image" src="https://github.com/user-attachments/assets/cfc4b7df-79c9-4623-8d0d-4bfd9bd97d96" />| <img width="502" height="381" alt="Image" src="https://github.com/user-attachments/assets/ad72bbd7-cbe2-4a95-9879-714869557abf" /> |
| **모임 목록** | **알림** |
| <img width="452" height="313" alt="image" src="https://github.com/user-attachments/assets/a6757115-496a-4461-a17e-ded00356c08f" />| <img width="410" height="363" alt="image" src="https://github.com/user-attachments/assets/fa7b996c-3cfa-4db4-b0d5-3c54e3b74874" />|

## 🛠️ 기술 스택 및 아키텍처

### Architecture

<img width="668" height="381" alt="image" src="https://github.com/user-attachments/assets/aaca196c-8aad-4051-b773-b1b6db81b680" />


### Tech Stack

  - **Backend**: Flask, MongoDB
  - **Frontend**: HTML/CSS, JavaScript, Jinja, Tailwind CSS
  - **Infrastructure**: AWS (EC2, ELB, ECR), Docker
  - **CI/CD**: GitHub Actions
  - **Monitoring**: Grafana, Prometheus, CloudWatch
  - **Testing**: k6 (부하 테스트)
  - **Etc**: Google Apps Script (이메일 알림)
---

## 💡 기술적 과제 및 해결 노력

### 1. 실시간 동기화 문제
- **문제점 (Challenge)**: 사용자가 예약을 하거나 취소할 때, 다른 사용자들의 화면에는 변경사항이 바로 반영되지 않아 데이터 불일치가 발생할 수 있었습니다.
- **해결방안 (Solution)**: `WebSocket`을 도입하여 서버와 클라이언트 간의 양방향 통신 채널을 구축했습니다. 이를 통해 데이터 변경이 발생하면 서버가 즉시 모든 클라이언트에게 변경사항을 전송하여, 모든 사용자가 항상 최신 정보를 볼 수 있도록 사용자 경험을 향상시켰습니다.

### 2. 동시성 제어 (Concurrency Control)
- **문제점 (Challenge)**: 여러 사용자가 동시에 특정 모임에 예약/취소를 요청할 경우, 경쟁 상태(Race Condition)가 발생하여 데이터의 정합성이 깨질 위험이 있었습니다.
- **해결방안 (Solution)**: 데이터베이스 단에서 원자적(Atomic) 연산을 보장하는 MongoDB의 `find_one_and_update` 메서드를 활용했습니다. 이 덕분에 여러 요청이 동시에 들어와도 데이터가 순차적으로 처리되어 정합성을 확보할 수 있었습니다.

### 3. 인증 시스템의 확장성
- **문제점 (Challenge)**: 초기 `Session` 기반 인증 방식은 서버가 각 사용자의 상태를 저장해야 하므로, 향후 서버를 증설하거나 분산 환경으로 확장할 때 복잡성이 증가하는 문제가 있었습니다.
- **해결방안 (Solution)**: 서버가 상태를 저장하지 않는(Stateless) `JWT(JSON Web Token)` 기반 인증으로 전환했습니다. 토큰 자체에 인증 정보를 담아 서버의 의존성을 제거함으로써, 서버 확장 및 마이크로서비스 아키텍처로의 전환 가능성을 열어두었습니다.

### 4. 체계적인 협업 관리
- **문제점 (Challenge)**: 팀원 각자의 작업 스타일이 달라 코드 충돌이 잦았고, 작업 내역을 추적하기 어려웠습니다.
- **해결방안 (Solution)**: `Git-flow` 브랜치 전략을 도입하여 기능 개발, 버그 수정 등의 작업을 체계적으로 분리하고, `Git Convention`에 따라 커밋 메시지를 표준화하여 협업의 효율성과 코드 관리의 안정성을 높였습니다.

### 5. 서비스 안정성 검증
- **문제점 (Challenge)**: 서비스 출시 전, 예상되는 사용자 트래픽을 시스템이 안정적으로 처리할 수 있는지에 대한 객관적인 데이터가 부족했습니다.
- **해결방안 (Solution)**: `k6`를 이용한 부하 테스트를 통해 동시 접속자 수에 따른 시스템의 응답 속도와 성능 한계를 파악하고 병목 지점을 개선했습니다. 또한 `Prometheus`와 `Grafana`로 실시간 모니터링 대시보드를 구축하여 서비스의 안정성을 지속적으로 관리할 수 있도록 했습니다.

## 🧑‍💻 팀원 및 역할

| 이름      | 주요 역할               | 담당 업무 상세                                                                                                                                                                | GitHub                                          |
| ------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| **권동민** | **Frontend**        | - 메인 예약 페이지 UI/UX 개발 (달력, 타임라인)<br>- 모임 생성 및 관리 페이지 프론트엔드 개발<br>- Google Apps Script를 활용한 이메일 알림 시스템 구축                                                                 | **[tomk1002](https://github.com/tomk1002)**     |
| **권동하** | **Frontend**        | - 회원가입 및 로그인 페이지 UI/UX 개발<br>- JWT 인증 로직 클라이언트 연동<br>- 마이페이지 및 사용자 정보 관련 프론트엔드 개발<br> - Flask 기반 API 인증 및 비즈니스 로직 개발<br>                                                                                       | **[ssyy3034](https://github.com/ssyy3034)**     |
| **유선목** | **Backend & Infra** | - MongoDB 데이터베이스 스키마 설계<br>- **WebSocket 서버 구축 및 실시간 기능 개발**<br>- AWS, Docker 기반의 인프라 설계 및 구축<br>- GitHub Actions를 통한 CI/CD 파이프라인 자동화 | **[tjsahr9191](https://github.com/tjsahr9191)** |

