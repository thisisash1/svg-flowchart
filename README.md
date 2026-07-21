# Figma-Ready SVG Flowchart

Claude Code 스킬 기반으로 **Figma에 바로 import 가능한 SVG 플로우차트**를 생성하는 프로젝트입니다.
아이디어 → 인터뷰 → 좌표 검증 → SVG 파일까지 한 번에 처리합니다.

---

## 데모

| 파일 | 설명 |
|------|------|
| [`outputs/parcel-tracking-system.svg`](outputs/parcel-tracking-system.svg) | 택배 조회 시스템 전체 아키텍처 플로우 |
| [`outputs/finance-transfer-flow.svg`](outputs/finance-transfer-flow.svg) | 금융 송금 서비스 플로우 |
| [`outputs/haezum-power-flow.svg`](outputs/haezum-power-flow.svg) | 해줌 태양광 발전량 조회 서비스 플로우 |
| [`outputs/re100-roadmap-flow.svg`](outputs/re100-roadmap-flow.svg) | RE100 달성 로드맵 의사결정 플로우 |
| [`outputs/sns-architecture.svg`](outputs/sns-architecture.svg) | SNS 플랫폼 시스템 아키텍처 (21노드 이상, 레이어별 분할 처리) |

---

## 사용법

Claude Code가 설치된 환경에서 아래처럼 요청하면 스킬이 자동 실행됩니다.

```
플로우차트 만들어줘 — [서비스/기능 설명]
```

**트리거 키워드 예시**

- `플로우차트 만들어줘` / `다이어그램 그려줘`
- `서비스 플로우 설계해줘` / `피그마용 SVG`
- `유저 플로우` / `시스템 아키텍처` / `의사결정 흐름`
- `조직도` / `OKR 로드맵` / `process diagram` / `roadmap`
- 기존 플로우차트 수정/업데이트 요청 시도 자동 트리거

출력 파일은 항상 `outputs/` 폴더에 `.svg` + `.md` 쌍으로 저장됩니다.

---

## 동작 방식

스킬은 세 Phase로 실행됩니다.

### Phase 0 — 아키텍처 완성도 검증

SVG를 만들기 전에 플로우의 빈틈을 찾습니다.

- **다이어그램 유형 감지**: 서비스 플로우 / 시스템 아키텍처 / 유저 저니 / 의사결정 트리 / API 플로우
- **Round 1**: 목적, 액터, 시작 트리거, 종료점, 핵심 단계
- **Round 2**: 유형별 심화 질문 (인증, 분기 조건, 데이터 흐름 등)
- **Round 3**: 12가지 갭 탐지 (오류 케이스, 타임아웃, 재시도, 권한 분기 등)
- **블루프린트 제시**: 텍스트로 전체 구조 요약 후 사용자 확인

### Phase 0.5 — 좌표 레지스트리 + 충돌 검증

> SVG 코드를 한 줄도 작성하기 전에 완료해야 합니다.

**0.5-0. 복잡도 게이트** — 총 노드 수에 따라 처리 방식을 자동 분기합니다:

| 노드 수 | 처리 방식 |
|---------|----------|
| **≤ 20노드** | 통합 레지스트리 방식 (전체 좌표를 한 번에 계산) |
| **≥ 21노드** | **레이어별 분할 처리** (최대 8노드 단위로 분할 → API 타임아웃 방지) |

**레이어별 분할 처리 (21노드 이상)**: 전체 좌표를 한 번에 계산하면 모델 thinking token이 10만개+ 소모되어 세션이 종료됩니다. 레이어(Layer) 단위로 쪼개어 각 단위를 4~8노드로 줄인 뒤, SVG 파일에 `cat >>` 로 누적 저장합니다.

**통합 레지스트리 방식 (20노드 이하)**: 모든 노드의 좌표를 테이블로 계산하고, 5가지 충돌 규칙을 검증합니다.

| Rule | 검증 내용 |
|------|-----------|
| 1 | 노드 bbox 겹침 없음 (여백 ≥ 20px) |
| 2 | 화살표 시작/끝 좌표가 노드 경계와 ±5px 이내 일치 |
| 3 | 우회 경로 경유점이 메인 플로우 노드와 겹치지 않음 |
| 4 | 예외 컨테이너가 모든 예외 노드를 포함 |
| 5 | 0-길이 요소 없음, 모든 화살표에 marker-end 존재 |

규칙 위반 발견 시 자동 수정 후 재검증합니다.

### Phase 1 — SVG 제작

레지스트리 좌표만 사용해서 SVG를 생성합니다.
- **20노드 이하**: 전체 SVG를 한 번에 파일로 저장
- **21노드 이상**: Phase 0.5-L에서 이미 누적 저장 완료 → 기획 MD만 추가 저장

생성 후 동일한 파일명으로 `.md` 기획 명세도 함께 저장합니다.

---

## 프로젝트 구조

```
.
├── .claude/
│   └── commands/
│       └── figma-svg-flowchart.md   # 스킬 정의 (Phase 0 / 0.5 / 1)
├── outputs/                          # 생성된 SVG + 기획 MD
│   ├── parcel-tracking-system.svg
│   ├── parcel-tracking-system.md
│   ├── finance-transfer-flow.svg
│   ├── finance-transfer-flow.md
│   ├── haezum-power-flow.svg
│   ├── haezum-power-flow.md
│   ├── re100-roadmap-flow.svg
│   ├── re100-roadmap-flow.md
│   ├── sns-architecture.svg
│   └── sns-architecture.md
├── references/
│   ├── color-tokens.md               # 노드 타입별 컬러 스펙
│   ├── componet-examples.md          # SVG 컴포넌트 스니펫
│   └── layout-guide.md              # 레이아웃 패턴 + 간격 공식
└── README.md
```

---

## 디자인 시스템

### 노드 컬러 체계

| 역할 | stroke | fill | 사용처 |
|------|--------|------|--------|
| 사용자 액션 | `#2563EB` | `#FFFFFF` | 사용자가 직접 하는 행동 |
| 시스템 처리 | `#059669` | `#F0FDF4` | 서버/시스템 내부 처리 |
| 외부 시스템 | `#7C3AED` | `#FAF5FF` | 외부 API, 서드파티 |
| 완료 / 저장 | `#E11D48` | `#FFF1F2` | 데이터 저장, 완료 처리 |
| 분기 판단 | `#D97706` | `#FFFBEB` | 다이아몬드 분기 노드 |
| 종료 / 이탈 | `#CBD5E1` | `#F1F5F9` | 플로우 종료 노드 |
| 예외 / 오류 | `#FECDD3` | `#FEF2F2` | 에러 처리 노드 |

### 레이아웃 패턴

| 패턴 | 캔버스 | 적용 상황 |
|------|--------|-----------|
| **세로형** | 1800 × 3200~4000 | 사용자 여정, 결제, 로그인 플로우 |
| **가로형** | 3200~4800 × 1400 | 시스템 아키텍처, API 데이터 플로우 |
| **스윔레인** | 2400~3600 × 1800~2400 | 역할별 책임 분리 다이어그램 |
| **혼합형** | 2400 × 2400~3200 | 의사결정 트리, 복잡한 분기 구조 |

레이아웃 선택 기준 및 간격 공식은 `references/layout-guide.md` 참조.

### 주요 컴포넌트

- **스텝 노드**: 컬러 탑바(5px) + 스텝 레이블 + 메인 제목 + 부제목
- **분기 다이아몬드**: ±120px (기본) 또는 ±160px (확장)
- **START/END**: pill shape (rx=24)
- **주석(Sticky Note)**: 좌우 여백 배치, 색상별 용도 구분
- **섹션 헤더**: `#0D1B3E` 다크 배경, 초록 서브라벨
- **예외 컨테이너**: dashed border, 모든 예외 노드 포함 보장

### 화살표 마커

```
ah-slate  #64748B  메인 플로우 기본
ah-blue   #2563EB  사용자 액션 경로
ah-green  #059669  성공 / 정상 경로
ah-purple #7C3AED  외부 시스템 연결
ah-red    #E11D48  오류 / 예외 경로
ah-amber  #D97706  조건부 분기 경로
```

---

## Figma 임포트

1. SVG 파일을 Figma 캔버스에 드래그 & 드롭
2. 모든 요소는 `<g id="...">` 로 그룹화되어 있어 개별 선택 가능
3. 폰트: Pretendard → Apple SD Gothic Neo → Noto Sans KR 순 fallback

---

## 스킬 커스터마이징

`.claude/commands/figma-svg-flowchart.md`를 수정해서 스킬을 확장할 수 있습니다.

- **새 노드 타입 추가**: `references/color-tokens.md`에 컬러 스펙 추가 후 스킬에 패턴 등록
- **레이아웃 패턴 추가**: `references/layout-guide.md`에 새 패턴 정의
- **Phase 0 질문 커스텀**: Round 3 갭 탐지 체크리스트 항목 추가/수정
- **Phase 0.5 검증 규칙 추가**: 충돌 검증 Rule 추가
- **복잡도 게이트 기준 변경**: Phase 0.5-0의 노드 수 임계값(현재 21) 조정

---

## 변경 이력

| 날짜 | 버전 | 내용 |
|------|------|------|
| 2026-07-21 | v3 | Phase 0.5-0 복잡도 게이트 신설 (≤20 통합 / ≥21 레이어별 분할), Phase 0.5-L 레이어별 분할 처리 신설, references/layout-guide.md 분리, 데모 파일 3개 추가 |
| 2026-06-02 | v2 | Phase 0.5 신설 (좌표 레지스트리 + 5가지 충돌 검증 규칙) |
| 2026-05-29 | v1 | figma-svg-flowchart 스킬 최초 작성, 첫 플로우차트 생성 |
