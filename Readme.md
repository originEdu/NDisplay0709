
# NDisplay — 프로젝트 문서

> Unreal Engine **5.7** 기반 nDisplay(다중 디스플레이 / LED 월 / 돔) 실시간 렌더링 프로젝트

<img width="400" height="225" alt="요약본" src="https://github.com/user-attachments/assets/f3f9cacd-847f-41c9-ad54-c277acc9c425" />

---

## 1. 프로젝트 개요

언리얼 엔진의 **nDisplay** 기능을 활용한 프로젝트입니다. 우주 공간을 여러 대의 디스플레이(또는 곡면 LED 월·돔)에 클러스터 렌더링하는 것이 목표

| 항목 | 내용 |
|------|------|
| 엔진 버전 | Unreal Engine 5.7 |
| 렌더링 기법 | nDisplay 클러스터 렌더링 |
| 대상 플랫폼 | Windows (Editor), Linux (Editor) |
| 그래픽 API | DirectX 12 (SM6) / Vulkan (SM6) |
| 저장소 | https://github.com/originEdu/NDisplay0709 |

---

## 2. 핵심 기술 스택 (플러그인)

`.uproject`에 활성화된 주요 플러그인입니다.

- **nDisplay** — 다중 노드 클러스터 렌더링 (다중 스크린 / LED 월 / 돔 / CAVE)
- **Switchboard** — nDisplay 클러스터 노드의 원격 실행·제어 및 동기화 관리
- **ICVFX (In-Camera VFX)** — 버추얼 프로덕션용 인카메라 VFX 파이프라인

---

## 3. 렌더링 설정 (Config/DefaultEngine.ini)

고품질 실시간 렌더링을 위해 다음 기능이 활성화되어 있습니다.

- **Lumen** — 다이내믹 글로벌 일루미네이션 & 리플렉션 (`DynamicGlobalIlluminationMethod=1`, `ReflectionMethod=1`)
- **Substrate** — 차세대 머티리얼 시스템 활성화
- **Ray Tracing** — 레이트레이싱 및 레이트레이싱 프록시 사용
- **Virtual Shadow Maps** — 고해상도 그림자
- **Mesh Distance Fields** 생성 활성화
- Static Lighting 비활성화 (완전 다이내믹 라이팅 워크플로우)
- Bloom / Auto Exposure / Motion Blur 기본값 Off (nDisplay 멀티뷰 일관성 목적)
- 기본 그래픽 RHI: **DX12**, 셰이더 모델 **SM6**

---

## 4. 씬 구성 요소

### 4.1 커스텀 액터 / 블루프린트 (`Content/CustomActor`)
- **BP_Earth** — 지구 (자전 회전 컴포넌트 포함)
- **BP_Satlelite** — 위성 (공전 로직)
- **BP_Terrain** — 지형 (달/사막 지형 표면)
- **C_Obital** — 공전(궤도) 로직 컴포넌트

### 4.2 에셋 (Fab / 무료 마켓플레이스)
- Space Station Module (우주 정거장)
- Earth (지구 모델)
- Free Desert Terrain / Landscape (지형)
- 1300 Followers Celebration – Space Station
- **StarfieldFree** — 별 필드, 성운, 실제 별 텍스처, 관련 머티리얼·레벨

### 4.3 사운드
- `IReallyWantToStayAtYourHouse` — 배경 음악(I Really Want to Stay at Your House)

---

## 5. nDisplay 구성

- **NDC_Origin_01** (`Content/nDisplay`) — 본 프로젝트의 nDisplay 클러스터 설정 에셋 (커스텀 구성)
- **ExampleConfigs** — 언리얼 제공 참고용 예제 구성
  - `NDC_Basic`, `NDC_Cave`, `NDC_CaveUnwrap`, `NDC_DualMonitor`, `NDC_DualAppWindows`, `NDC_MultiViewports`, `NDC_WallCurved3x2`, `NDC_XRStage`
  - EasyBlend 로컬 캘리브레이션(Cylinder / Flat) 예제 포함

> 패키징 시 `ExampleConfigs` 디렉터리는 Non-UFS로 항상 스테이징되도록 설정되어 있습니다.

---

## 6. LiveLink

- **PreSet01** (`Content/LiveLinkPresets`) — 기본 LiveLink 프리셋으로 지정
- 외부 트래킹/모션 데이터를 실시간으로 받아 씬에 반영하기 위한 설정 (버추얼 프로덕션 / 카메라 트래킹 연동 목적)

---

## 7. 프로젝트 구조

```
NDisplay0709/
├── Config/                 # 엔진·게임·입력 설정 (Windows / Linux)
├── Content/
│   ├── Actor/Terrain       # 지형 액터
│   ├── CustomActor         # BP_Earth, BP_Satlelite, BP_Terrain, C_Obital ...
│   ├── ExampleConfigs      # nDisplay 예제 구성 (.ndisplay)
│   ├── Fab                 # Fab 마켓플레이스 에셋 (우주정거장/지구/지형)
│   ├── StarfieldFree       # 별·성운 에셋
│   ├── LiveLinkPresets     # PreSet01
│   ├── Maps                # Main, MainDumy, MainTest, Test
│   ├── nDisplay            # NDC_Origin_01 (클러스터 구성)
│   └── Sound
└── NDisplay0709.uproject
```

---

## 8. 주요 개발 히스토리 (git)

- 지구/위성 회전·공전 로직 구현 (`BP_Earth` 회전 컴포넌트, `공전 로직`, `Add satellite`)
- 지형(Terrain) 액터 추가 및 달 지형 에셋 통합
- 배경 사운드 추가
- nDisplay(NDC) 구성 추가 및 오류 해결
- LiveLink 프리셋(PreSet01) 수정
- 레벨 레이아웃 조정 (MainTest / MainDumy)

---
