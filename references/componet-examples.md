# 컴포넌트 SVG 예시 코드

실제 붙여 쓸 수 있는 완성형 SVG 스니펫 모음.
Y값은 `{Y}`, cx는 `{CX}` 등 플레이스홀더로 표기.

---

## 컬러 시스템

| 역할 | stroke | fill | 탑바 | 텍스트 |
|------|--------|------|------|--------|
| 사용자 액션 | `#2563EB` | `#FFFFFF` | `#2563EB` | `#0D1B3E` / `#93C5FD` |
| 시스템 처리 | `#059669` | `#F0FDF4` | `#059669` | `#065F46` / `#34D399` |
| 완료 / 발송 | `#E11D48` | `#FFF1F2` | `#E11D48` | `#9F1239` / `#FDA4AF` |
| 소셜/보조 경로 | `#7C3AED` | `#FAF5FF` | `#7C3AED` | `#5B21B6` / `#7C3AED` |
| 분기 다이아몬드 | `#D97706` | `#FFFBEB` | — | `#92400E` |
| 이탈/종료 | `#CBD5E1` | `#F1F5F9` | — | `#475569` |
| 경고/실패 | `#FECDD3` | `#FEF2F2` | — | `#991B1B` |

주석(Sticky Note):

| 용도 | fill | stroke | 탑바 | 텍스트 |
|------|------|--------|------|--------|
| 노란 팁 | `#FEF9C3` | `#FDE047` | `#FDE047` | `#713F12` |
| 파란 정보 | `#DBEAFE` | `#93C5FD` | `#93C5FD` | `#1E3A8A` |
| 초록 안내 | `#D1FAE5` | `#6EE7B7` | `#6EE7B7` | `#064E3B` |
| 빨간 경고 | `#FFF1F2` | `#FECDD3` | — | `#9F1239` |

**텍스트 넘침 규칙**:
- 스텝 레이블(상단 소문자): 최대 40자
- 메인 제목: 최대 18자 (초과 시 font-size 14로 축소)
- 부제목/설명: 최대 36자 (초과 시 두 `<text>` 요소로 분리, y += 14px)

---

## 1. 전체 문서 뼈대

```svg
<svg xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 1800 3200"
  width="1800" height="3200"
  font-family="'Pretendard', 'Apple SD Gothic Neo', 'Noto Sans KR', sans-serif">

<defs>
  <marker id="ah-slate" viewBox="0 0 10 10" refX="9" refY="5"
    markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M1 1.5 L8.5 5 L1 8.5" fill="none" stroke="#64748B" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <marker id="ah-blue" viewBox="0 0 10 10" refX="9" refY="5"
    markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M1 1.5 L8.5 5 L1 8.5" fill="none" stroke="#2563EB" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <marker id="ah-green" viewBox="0 0 10 10" refX="9" refY="5"
    markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M1 1.5 L8.5 5 L1 8.5" fill="none" stroke="#059669" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <marker id="ah-purple" viewBox="0 0 10 10" refX="9" refY="5"
    markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M1 1.5 L8.5 5 L1 8.5" fill="none" stroke="#7C3AED" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <marker id="ah-red" viewBox="0 0 10 10" refX="9" refY="5"
    markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M1 1.5 L8.5 5 L1 8.5" fill="none" stroke="#E11D48" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <marker id="ah-amber" viewBox="0 0 10 10" refX="9" refY="5"
    markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M1 1.5 L8.5 5 L1 8.5" fill="none" stroke="#D97706" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <pattern id="grid" width="24" height="24" patternUnits="userSpaceOnUse">
    <circle cx="0" cy="0" r="1" fill="#E2E8F0" opacity="0.6"/>
  </pattern>
</defs>

<!-- 배경 -->
<rect width="1800" height="3200" fill="#F8FAFC"/>
<rect width="1800" height="3200" fill="url(#grid)"/>

<!-- 타이틀 헤더 -->
<rect x="60" y="40" width="1680" height="72" rx="14" fill="#0D1B3E"/>
<text x="88" y="66" font-size="10" font-weight="700" fill="#4ADE80" letter-spacing="2.5">SERVICE NAME</text>
<text x="88" y="92" font-size="22" font-weight="800" fill="#FFFFFF" letter-spacing="-0.5">플로우 제목</text>
<text x="1720" y="80" font-size="11" fill="rgba(255,255,255,0.4)" text-anchor="end">v1</text>

<!-- 범례 바 -->
<rect x="60" y="128" width="1680" height="48" rx="10" fill="#FFFFFF" stroke="#E2E8F0" stroke-width="1.5"/>
<rect x="88" y="146" width="14" height="14" rx="3" fill="#2563EB"/>
<text x="108" y="157" font-size="11.5" fill="#334155" font-weight="500">사용자 액션</text>
<rect x="248" y="146" width="14" height="14" rx="3" fill="#059669"/>
<text x="268" y="157" font-size="11.5" fill="#334155" font-weight="500">시스템 처리</text>
<polygon points="408,153 416,146 424,153 416,160" fill="#D97706"/>
<text x="432" y="157" font-size="11.5" fill="#334155" font-weight="500">분기 / 판단</text>
<rect x="570" y="146" width="14" height="14" rx="3" fill="#E11D48"/>
<text x="590" y="157" font-size="11.5" fill="#334155" font-weight="500">완료 / 발송</text>
<rect x="720" y="146" width="14" height="14" rx="3" fill="#94A3B8"/>
<text x="740" y="157" font-size="11.5" fill="#334155" font-weight="500">이탈 / 종료</text>

<!-- ... 노드들 ... -->

<!-- 푸터 -->
<rect x="60" y="3140" width="1680" height="36" rx="8" fill="#F1F5F9" stroke="#E2E8F0" stroke-width="1"/>
<text x="80" y="3161" font-size="10.5" fill="#94A3B8">서비스명 · 플로우 제목 · v1</text>
<text x="1720" y="3161" font-size="10.5" fill="#94A3B8" text-anchor="end">FigJam Ready SVG · 1800 × 3200</text>

</svg>
```

---

## 2. 사용자 액션 노드 (파란색, 80px)

```svg
<g id="step1-example">
  <rect x="660" y="220" width="480" height="80" rx="12" fill="#FFFFFF" stroke="#2563EB" stroke-width="2"/>
  <rect x="660" y="220" width="480" height="5" rx="12" fill="#2563EB"/>
  <text x="900" y="246" font-size="10" font-weight="700" fill="#93C5FD" text-anchor="middle" letter-spacing="1.5">STEP 1 · INPUT</text>
  <text x="900" y="270" font-size="16" font-weight="800" fill="#0D1B3E" text-anchor="middle">사용자 입력</text>
  <text x="900" y="290" font-size="11" fill="#64748B" text-anchor="middle">상세 설명 텍스트</text>
</g>
```

---

## 3. 시스템 처리 노드 (초록색, 56px)

```svg
<g id="system-process">
  <rect x="660" y="350" width="480" height="56" rx="10" fill="#F0FDF4" stroke="#059669" stroke-width="2"/>
  <rect x="660" y="350" width="480" height="5" rx="10" fill="#059669"/>
  <text x="900" y="375" font-size="10" font-weight="700" fill="#34D399" text-anchor="middle" letter-spacing="1.5">SYSTEM PROCESS</text>
  <text x="900" y="396" font-size="13" font-weight="700" fill="#065F46" text-anchor="middle">시스템 처리 내용</text>
</g>
```

---

## 4. 완료/발송 노드 (빨간색, 80px)

```svg
<g id="complete-node">
  <rect x="660" y="450" width="480" height="80" rx="12" fill="#FFF1F2" stroke="#E11D48" stroke-width="2"/>
  <rect x="660" y="450" width="480" height="5" rx="12" fill="#E11D48"/>
  <text x="900" y="476" font-size="10" font-weight="700" fill="#FDA4AF" text-anchor="middle" letter-spacing="1.5">STEP N · COMPLETE</text>
  <text x="900" y="500" font-size="16" font-weight="800" fill="#9F1239" text-anchor="middle">완료 제목</text>
  <text x="900" y="520" font-size="11" fill="#E11D48" text-anchor="middle">완료 설명</text>
</g>
```

---

## 5. 분기 다이아몬드

```svg
<!-- cx=900, cy=600 기준 -->
<g id="diamond-example">
  <polygon points="900,564 1020,600 900,636 780,600"
    fill="#FFFBEB" stroke="#D97706" stroke-width="2"/>
  <text x="900" y="594" font-size="12" font-weight="700" fill="#92400E" text-anchor="middle">판단</text>
  <text x="900" y="612" font-size="12" font-weight="700" fill="#92400E" text-anchor="middle">기준?</text>
</g>

<!-- 분기 화살표 + 라벨 예시 -->
<!-- 예 (아래로) -->
<text x="920" y="680" font-size="10" fill="#059669">예</text>
<line x1="900" y1="636" x2="900" y2="700"
  stroke="#64748B" stroke-width="2" marker-end="url(#ah-slate)"/>

<!-- 아니오 (오른쪽으로) -->
<text x="1024" y="594" font-size="10" fill="#94A3B8">아니오</text>
<line x1="1020" y1="600" x2="1100" y2="600"
  stroke="#94A3B8" stroke-width="1.5" marker-end="url(#ah-slate)"/>
```

---

## 6. START pill

```svg
<g id="start">
  <rect x="700" y="200" width="400" height="48" rx="24" fill="#0D1B3E"/>
  <text x="900" y="229" font-size="14" font-weight="700" fill="#FFFFFF" text-anchor="middle">서비스 진입 (URL 접속)</text>
</g>
```

---

## 7. END pill

```svg
<g id="end">
  <rect x="700" y="1800" width="400" height="48" rx="24" fill="#F1F5F9" stroke="#94A3B8" stroke-width="2"/>
  <text x="900" y="1829" font-size="14" font-weight="700" fill="#475569" text-anchor="middle">✅ 서비스 플로우 종료</text>
</g>
```

---

## 8. 노란 주석 노트 (4줄, h=106)

```svg
<g id="note-tip">
  <rect x="1220" y="220" width="256" height="106" rx="4" fill="#FEF9C3" stroke="#FDE047" stroke-width="1.5"/>
  <rect x="1220" y="220" width="256" height="6" rx="4" fill="#FDE047"/>
  <text x="1236" y="246" font-size="11" font-weight="700" fill="#713F12">💡 팁 제목</text>
  <text x="1236" y="266" font-size="10" fill="#78350F">• 항목 1</text>
  <text x="1236" y="284" font-size="10" fill="#78350F">• 항목 2</text>
  <text x="1236" y="302" font-size="10" fill="#78350F">• 항목 3</text>
  <!-- 연결선: 주석 왼쪽 → 노드 오른쪽 -->
  <line x1="1220" y1="273" x2="1140" y2="273"
    stroke="#FDE047" stroke-width="1.5" stroke-dasharray="4,3"/>
</g>
```

---

## 9. 왼쪽 경로 노드 (cx=340, 보라색 계열)

```svg
<!-- cx=340, x=200, width=280 -->
<g id="left-node">
  <rect x="200" y="546" width="280" height="72" rx="12" fill="#FAF5FF" stroke="#7C3AED" stroke-width="2"/>
  <rect x="200" y="546" width="280" height="5" rx="12" fill="#7C3AED"/>
  <text x="340" y="570" font-size="9" font-weight="700" fill="#7C3AED" text-anchor="middle" letter-spacing="1.2">NON-MEMBER PATH</text>
  <text x="340" y="594" font-size="14" font-weight="800" fill="#5B21B6" text-anchor="middle">비회원 경로 제목</text>
  <text x="340" y="610" font-size="10" fill="#7C3AED" text-anchor="middle">부제목</text>
</g>
```

---

## 10. 메인 → 분기 경로 꺾기 화살표

```svg
<!-- 오른쪽으로 꺾어 나가는 실패 경로 -->
<path d="M {분기cx+120} {분기cy} L {목적지X-2} {분기cy}"
  stroke="#94A3B8" stroke-width="1.5" fill="none" marker-end="url(#ah-slate)"/>

<!-- 왼쪽으로 빠지는 경로 (비회원 등) -->
<path d="M {분기cx-120} {분기cy} L {왼쪽cx} {분기cy} L {왼쪽cx} {목적지Y}"
  stroke="#7C3AED" stroke-width="2" fill="none" marker-end="url(#ah-purple)"/>

<!-- 복귀 점선 (아래 → 위 → 오른쪽) -->
<path d="M {출발X} {출발Y} L {우회X} {출발Y} L {우회X} {목적Y} L {목적X} {목적Y}"
  stroke="#7C3AED" stroke-width="1.5" stroke-dasharray="6,3"
  fill="none" marker-end="url(#ah-purple)"/>
```

---

## 11. 예외 처리 구역 헤더 + 섹션 라벨

```svg
<!-- 구역 헤더 -->
<rect x="60" y="1680" width="1680" height="60" rx="12" fill="#0D1B3E"/>
<text x="100" y="1706" font-size="10" font-weight="700" fill="#4ADE80" letter-spacing="2">EXCEPTION HANDLING</text>
<text x="100" y="1728" font-size="18" font-weight="800" fill="#FFFFFF">예외 케이스 대응 플로우</text>
<text x="1720" y="1715" font-size="11" fill="rgba(255,255,255,0.4)" text-anchor="end">E1 ~ E4</text>

<!-- 섹션 라벨 (각 예외 케이스 위) -->
<rect x="60" y="1768" width="440" height="28" rx="6" fill="#EFF6FF" stroke="#BFDBFE" stroke-width="1"/>
<text x="80" y="1787" font-size="11" font-weight="700" fill="#1D4ED8">E1. 예외 케이스 제목</text>
```

---

## 12. 컨테이너 (스크래핑/API 그룹 박스)

```svg
<g id="container-group">
  <!-- 배경 컨테이너 -->
  <rect x="260" y="1212" width="840" height="260" rx="16"
    fill="#F0FDF4" stroke="#059669" stroke-width="2" stroke-dasharray="8,4" fill-opacity="0.5"/>
  <!-- 컨테이너 라벨 탭 -->
  <rect x="340" y="1200" width="300" height="22" rx="5" fill="#F4F6FA"/>
  <text x="490" y="1215" font-size="10" font-weight="700" fill="#059669"
    text-anchor="middle" letter-spacing="1.5">CONTAINER LABEL</text>

  <!-- 내부 노드들 -->
  <rect x="280" y="1240" width="240" height="64" rx="10" fill="#FFFFFF" stroke="#059669" stroke-width="1.5"/>
  <text x="400" y="1265" font-size="12" font-weight="700" fill="#065F46" text-anchor="middle">내부 항목 1</text>
  <text x="400" y="1285" font-size="9.5" fill="#059669" text-anchor="middle" font-family="'Courier New', monospace">API 코드</text>
</g>
```

---

## 13. 공통 원칙 박스 (예외 구역 우측)

```svg
<g id="common-principle">
  <rect x="1220" y="1768" width="520" height="200" rx="12" fill="#FFF1F2" stroke="#FECDD3" stroke-width="1.5"/>
  <text x="1480" y="1798" font-size="12" font-weight="700" fill="#9F1239" text-anchor="middle">공통 원칙</text>
  <text x="1240" y="1822" font-size="10.5" fill="#BE123C">• 원칙 1</text>
  <text x="1240" y="1840" font-size="10.5" fill="#BE123C">• 원칙 2</text>
  <text x="1240" y="1858" font-size="10.5" fill="#BE123C">• 원칙 3</text>
  <text x="1240" y="1876" font-size="10.5" fill="#DC2626">• 중요 항목 (빨간색)</text>
</g>
```

---

## 14. CTA 버튼 노드 (pill, 파란색)

```svg
<g id="cta-button">
  <rect x="480" y="320" width="400" height="48" rx="24" fill="#2563EB"/>
  <text x="680" y="349" font-size="14" font-weight="700" fill="#FFFFFF" text-anchor="middle">CTA 버튼 텍스트 →</text>
</g>
```

---

## 15. 경고 박스 (인라인, 컨테이너 내부)

```svg
<rect x="400" y="1420" width="360" height="34" rx="6"
  fill="#FFF1F2" stroke="#FECDD3" stroke-width="1"/>
<text x="580" y="1441" font-size="10.5" fill="#BE123C" text-anchor="middle" font-weight="600">
  ⚠ 경고 메시지 텍스트
</text>
```