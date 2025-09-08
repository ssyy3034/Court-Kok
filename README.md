네, 제공해주신 발표 자료와 GitHub 저장소 링크를 바탕으로 프로젝트를 설명하는 README.md 파일을 작성해 드리겠습니다.

아래 내용을 복사하여 GitHub 저장소의 `README.md` 파일에 붙여넣으시면 됩니다.

-----

# 🏀 Court-Kok (코트콕)

<img width="294" height="295" alt="Image" src="https://github.com/user-attachments/assets/2793310a-08af-4d96-bb78-3bedff8c4fc2" />

> 농구 예약을 간단하게, 즐겁게\!

**Court-Kok**은 함께 농구 할 사람을 찾기 어려운 문제를 해결하고, 간편하게 코트를 예약하며 사람들을 모을 수 있는 실시간 농구 매칭 서비스입니다.

## 🌟 주요 기능

  - **회원가입 및 로그인**: JWT 기반의 안전한 인증 시스템을 통해 서비스를 이용할 수 있습니다.
  - **실시간 예약 시스템**: 월간 달력과 일일 스케줄 뷰를 통해 원하는 날짜와 시간을 직관적으로 선택하고 예약할 수 있습니다.
  - **간편한 모임 생성**: 최소/최대 인원, 진행 시간 등 상세 조건을 설정하여 농구 모임을 손쉽게 만들 수 있습니다.
  - **실시간 알림**: WebSocket을 활용하여 모임 생성, 취소, 인원 마감 등 변동 사항을 웹과 이메일로 실시간 알림을 받습니다.
  - **나의 예약 관리**: 내가 만들거나 참여한 모임의 목록과 참여자 정보를 한눈에 확인하고 관리할 수 있습니다.
  - **마이페이지**: 개인 정보를 확인하고 수정할 수 있습니다.

## 🖼️ 서비스 화면

| 로그인 & 회원가입 | 메인 페이지 (예약) |
| :---: | :---: |
| \<img src="[https://user-images.githubusercontent.com/81137093/228120619-32a26514-94c6-47b8-8091-a8d6e3556ddf.png](https://www.google.com/search?q=https://user-images.githubusercontent.com/81137093/228120619-32a26514-94c6-47b8-8091-a8d6e3556ddf.png)" width="300"/\> | \<img src="[https://user-images.githubusercontent.com/81137093/228120712-4d04f2f9-7101-4ec1-a1b9-ac5d898491c1.png](https://www.google.com/search?q=https://user-images.githubusercontent.com/81137093/228120712-4d04f2f9-7101-4ec1-a1b9-ac5d898491c1.png)" width="300"/\> |
| **모임 목록** | **알림** |
| \<img src="[https://user-images.githubusercontent.com/81137093/228120743-a65c4004-ca01-4475-b6d6-68045657803e.png](https://www.google.com/search?q=https://user-images.githubusercontent.com/81137093/228120743-a65c4004-ca01-4475-b6d6-68045657803e.png)" width="300"/\> | \<img src="[https://user-images.githubusercontent.com/81137093/228120760-b962776c-3a32-4404-874d-176317d7b0f0.png](https://www.google.com/search?q=https://user-images.githubusercontent.com/81137093/228120760-b962776c-3a32-4404-874d-176317d7b0f0.png)" width="300"/\> |

## 🛠️ 기술 스택 및 아키텍처

### Architecture

\<img src="[https://user-images.githubusercontent.com/81137093/228120790-2c7c729c-30c0-410e-8911-396a5d481062.png](https://www.google.com/search?q=https://user-images.githubusercontent.com/81137093/228120790-2c7c729c-30c0-410e-8911-396a5d481062.png)" width="600"/\>

### Tech Stack

  - **Backend**: Flask, MongoDB
  - **Frontend**: HTML/CSS, JavaScript, Jinja, Tailwind CSS
  - **Infrastructure**: AWS (EC2, ELB, ECR), Docker
  - **CI/CD**: GitHub Actions
  - **Monitoring**: Grafana, Prometheus, CloudWatch
  - **Testing**: k6 (부하 테스트)
  - **Etc**: Google Apps Script (이메일 알림)

## 🎯 기술적 과제 및 해결 노력

  - **실시간 데이터 동기화**: 사용자의 예약 신청, 취소 등 상태 변화를 모든 클라이언트에게 실시간으로 반영하기 위해 **WebSocket**을 구축했습니다.
  - **동시성 제어**: 여러 사용자가 동시에 특정 모임에 예약/취소를 요청할 때 발생할 수 있는 데이터 불일치 문제를 MongoDB의 원자적 연산(`find_one_and_update`)을 활용하여 해결했습니다.
  - **인증 시스템 개선**: 초기 Session 기반 인증 방식에서 확장성과 독립성을 고려하여 **JWT(JSON Web Token)** 기반으로 인증 시스템을 전환했습니다.
  - **안정적인 협업 환경**: **Git Convention**과 **Git-flow** 전략을 도입하여 팀원 간의 코드 충돌을 최소화하고 체계적인 버전 관리를 수행했습니다.
  - **성능 테스트 및 모니터링**: k6를 이용한 부하 테스트를 통해 동시 접속자 수에 따른 시스템의 응답 속도와 안정성을 검증하고, Prometheus와 Grafana로 시스템 상태를 지속적으로 모니터링했습니다.

## 🧑‍💻 팀원 소개

| 이름 | 역할 |                                   GitHub                                   |
| :---: | :---: |:--------------------------------------------------------------------------:|
| **권동민** | 프론트엔드, 이메일 알림 시스템 |  [GitHub 링크](https://www.google.com/search?q=https://github.com/tomk1002)  |
| **권동하** | 프론트엔드, 회원가입 |  [GitHub 링크](https://www.google.com/search?q=https://github.com/ssyy3034)  |
| **유선목** | 백엔드, 인프라 구축(AWS, Docker) | [GitHub 링크](https://www.google.com/search?q=https://github.com/tjsahr9191) |
