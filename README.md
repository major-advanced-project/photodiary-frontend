# 📸 PhotoDiary Frontend

AI 기반 자동 일기 생성 & 사진 기록 서비스 프론트엔드

포토다이어리는 사용자가 사진을 업로드하면, BLIP2 + GPT를 이용해 자동으로 감성 일기를 생성해주는 서비스입니다.
이 저장소는 그 중 웹 프론트엔드(Next.js/React 기반) 프로젝트입니다.

## 🚀 시연 영상  
https://youtu.be/NsSTa1Wh3iM

## UI
<img width="511" height="301" alt="image" src="https://github.com/user-attachments/assets/50771965-6e50-40c3-9cab-59ddf5d44fc2" />
<img width="524" height="281" alt="image" src="https://github.com/user-attachments/assets/ea537f2b-72f7-4a89-8d87-2c76ea77df47" />
<img width="516" height="271" alt="스크린샷 2025-11-20 오후 6 00 56" src="https://github.com/user-attachments/assets/fa89f147-a667-4d76-86e0-fae0bc2fbc14" />
<img width="533" height="326" alt="image" src="https://github.com/user-attachments/assets/d1e168e6-d73c-40a0-9e65-5f5c82b15ab1" />
<img width="1082" height="450" alt="image" src="https://github.com/user-attachments/assets/e76294e8-3057-46eb-8f73-f2704eed3cdc" />



## 🚀 주요 화면 & 기능
| 구분               | 기능                                      |
| ---------------- | --------------------------------------- |
| **인덱스 / 랜딩 페이지** | 서비스 소개, 시작하기/로그인/회원가입 진입                |
| **회원가입 페이지**     | 이메일, 비밀번호, 닉네임을 입력해 계정 생성               |
| **로그인 페이지**      | JWT 기반 로그인, 토큰 저장 및 인증 상태 관리            |
| **일기 작성 페이지**    | 이미지 업로드 → 자동 일기 생성 요청 → 결과 확인 및 수정 후 저장 |
| **내 일기 목록 페이지**  | 내가 작성한 일기 카드 리스트 조회, 상세보기/수정 진입         |
| **일기 상세 페이지**    | 생성된 일기 내용 확인, 수정하기 버튼 제공                |
| **친구 목록 페이지**    | 친구 리스트 조회, 친구 추가 화면 진입, 친구 일기 목록으로 이동   |
| **친구 일기 목록 페이지** | 선택한 친구의 공개된 일기 목록 조회                    |
| **친구 일기 상세 페이지** | 친구가 공개한 일기 상세 조회                        |



## 🧠 기술 스택
| 영역             | 사용 기술                                      |
| -------------- | ------------------------------------------ |
| **Framework**  | React                      |
| **Language**   | JavaScript / TypeScript (프로젝트 설정에 맞게)      |
| **UI / 스타일링**  | Tailwind CSS                               |
| **상태 / 서버 통신** | React Query, axios                         |
| **인증**         | JWT 기반 토큰 저장 및 Axios 인터셉터 활용               |
| **배포**         | Vercel / Netlify / AWS EC2 중 하나 |


##  프로젝트 실행 방법 (Next.js)

### 1. 저장소 클론

```bash
git clone https://github.com/major-advanced-project/photodiary-frontend.git
cd photodiary-frontend
```
### 2. 의존성 설치

```bash
npm install
```

### 3. 개발 서버 실행
```bash
npm run dev
```
### 4. 브라우저에서 확인
```bash
http://localhost:3000
```


## 🔐 인증 흐름
| 단계 | 설명                                                                |
| -- | ----------------------------------------------------------------- |
| 1  | 로그인 시 이메일/비밀번호를 백엔드로 전송                                           |
| 2  | 백엔드에서 JWT accessToken 발급                                          |
| 3  | 프론트엔드는 토큰을 `localStorage` 또는 `cookie` 등에 저장                       |
| 4  | 이후 API 요청 시 axios 인터셉터에서 `Authorization: Bearer <token>` 헤더 자동 추가 |
| 5  | 토큰 만료/에러 발생 시 재로그인 유도                                             |

## 📸 일기 작성 플로우
| 단계 | 설명                                           |
| -- | -------------------------------------------- |
| 1  | 사용자가 일기 작성 페이지에서 사진 여러 장을 업로드                |
| 2  | “일기 생성” 버튼 클릭 시 백엔드 `/diary/generate` API 호출 |
| 3  | 백엔드는 BLIP2 서버 + GPT를 호출해 일기 초안을 생성           |
| 4  | 프론트는 응답으로 받은 일기 내용을 에디터에 채워 보여줌              |
| 5  | 사용자가 내용과 공개 범위를 확인/수정 후 “저장” 버튼 클릭           |
| 6  | `/diary` 저장 API 호출 후 내 일기 목록 페이지로 이동         |

## 🤝 친구/공유 기능
| 화면       | 역할                                              |
| -------- | ----------------------------------------------- |
| 친구 목록 화면 | 친구 리스트 표시, 친구 ID 입력 → 친구 추가 요청                  |
| 친구 추가 폼  | 친구 ID 입력 → `/friend` API 호출 결과에 따라 성공/오류 메시지 표시 |
| 친구 일기 목록 | 선택한 친구의 공개 일기를 카드 형태로 표시                        |
| 친구 일기 상세 | 일기 내용 보여주기 (수정 버튼 없음, 읽기 전용)                    |

## 🧪 개선 아이디어
| 항목     | 내용                                            |
| ------ | --------------------------------------------- |
| 로딩 UX  | 일기 생성/이미지 업로드 중에 Skeleton UI, Progress Bar 추가 |
| 오류 처리  | 토스트(Notification) 컴포넌트를 만들어 공통으로 사용           |
| 반응형 개선 | 모바일·태블릿·데스크톱 레이아웃 세분화                         |
| 접근성    | 버튼/폼에 aria-label, 키보드 네비게이션 지원                |

## 📎 관련 저장소
| 역할              | Repository                                                                                                                           |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Backend         | [https://github.com/major-advanced-project/photodiary-backend](https://github.com/major-advanced-project/photodiary-backend)         |
| Frontend        | [https://github.com/major-advanced-project/photodiary-frontend](https://github.com/major-advanced-project/photodiary-frontend)       |
| BLIP2 AI Server | [https://github.com/major-advanced-project/photodiary-blip-server](https://github.com/major-advanced-project/photodiary-blip-server) |

