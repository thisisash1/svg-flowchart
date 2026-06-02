# 컬러 토큰 상세 레퍼런스

## 노드 타입별 전체 스펙

### 사용자 액션 노드 (파란색)
```
stroke:        #2563EB  (stroke-width: 2)
fill:          #FFFFFF
탑바:          #2563EB
스텝라벨:      fill="#93C5FD"  (연한 파랑)
메인제목:      fill="#0D1B3E"  (다크네이비)
부제목:        fill="#64748B"  (슬레이트)
화살표마커:    ah-blue (#2563EB) 또는 ah-slate (#64748B)
```

### 시스템 처리 노드 (초록색)
```
stroke:        #059669  (stroke-width: 2)
fill:          #F0FDF4
탑바:          #059669
스텝라벨:      fill="#34D399"  (연한 초록)
메인제목:      fill="#065F46"  (다크그린)
부제목:        fill="#059669"
화살표마커:    ah-green (#059669)
```

### 완료 / 발송 노드 (빨간색)
```
stroke:        #E11D48  (stroke-width: 2)
fill:          #FFF1F2
탑바:          #E11D48
스텝라벨:      fill="#FDA4AF"
메인제목:      fill="#9F1239"
부제목:        fill="#E11D48"
화살표마커:    ah-red (#E11D48)
```

### 소셜/보조 경로 노드 (보라색)
```
stroke:        #7C3AED  (stroke-width: 1.5~2)
fill:          #FAF5FF
탑바:          #7C3AED
스텝라벨:      fill="#7C3AED"  (letter-spacing: 1.2)
메인제목:      fill="#5B21B6"
부제목:        fill="#7C3AED"
화살표마커:    ah-purple (#7C3AED)
점선:          stroke-dasharray="6,3"
```

### 이탈 / 종료 노드 (회색)
```
stroke:        #CBD5E1  (stroke-width: 1.5)
fill:          #F1F5F9
메인제목:      fill="#475569" 또는 #64748B
부제목:        fill="#94A3B8"
화살표마커:    ah-slate (#64748B)
```

### 실패 / 오류 노드 (연한 빨강)
```
stroke:        #FECDD3  (stroke-width: 1.5)
fill:          #FEF2F2
메인제목:      fill="#991B1B"
부제목:        fill="#DC2626"
화살표마커:    ah-red
```

### 경고 박스 (amber 계열)
```
stroke:        #FDE68A  (stroke-width: 1.5)
fill:          #FFFBEB
메인제목:      fill="#92400E"
부제목:        fill="#92400E"
화살표마커:    ah-amber (#D97706)
```

### 성공 박스 (연한 초록)
```
stroke:        #6EE7B7  (stroke-width: 1.5)
fill:          #ECFDF5
메인제목:      fill="#065F46"
부제목:        fill="#059669"
화살표마커:    ah-green
```

---

## 보조 배지 타입

### 보안 배지 (초록)
```
fill:    #F0FDF4
stroke:  #34D399  (stroke-width: 1.5)
라벨:    fill="#059669"  (font-size: 9, letter-spacing: 1.2)
제목:    fill="#065F46"  (font-size: 13, font-weight: 700)
부제목:  fill="#059669"  (font-size: 10)
```

### 데모 콘텐츠 배지 (보라)
```
fill:    #FAF5FF
stroke:  #7C3AED  (stroke-width: 1.5, stroke-dasharray: "6,3")
라벨:    fill="#7C3AED"  (font-size: 9, letter-spacing: 1.2)
제목:    fill="#5B21B6"  (font-size: 13, font-weight: 700)
부제목:  fill="#7C3AED"  (font-size: 10)
```

---

## Sticky Note 색상 상세

### 노란 팁 노트
```
fill:   #FEF9C3
stroke: #FDE047  (1.5px)
탑바:   #FDE047  (height: 6, rx: 4)
제목:   fill="#713F12"  (font-size: 11, font-weight: 700)
항목:   fill="#78350F"  (font-size: 10)
연결선: stroke="#FDE047" stroke-dasharray="4,3"
```

### 파란 정보 노트
```
fill:   #DBEAFE
stroke: #93C5FD  (1.5px)
탑바:   #93C5FD  (height: 6, rx: 4)
제목:   fill="#1E3A8A"  (font-size: 11, font-weight: 700)
항목:   fill="#1D4ED8"  (font-size: 10)
연결선: stroke="#93C5FD" stroke-dasharray="4,3"
```

### 초록 안내 노트
```
fill:   #D1FAE5
stroke: #6EE7B7  (1.5px)
탑바:   #6EE7B7  (height: 6, rx: 4)
제목:   fill="#064E3B"  (font-size: 11, font-weight: 700)
항목:   fill="#065F46"  (font-size: 10)
연결선: stroke="#6EE7B7" stroke-dasharray="4,3"
```

### 빨간 경고 노트
```
fill:   #FFF1F2
stroke: #FECDD3  (1.5px)
탑바:   없음 (또는 #FECDD3)
제목:   fill="#9F1239"  (font-size: 12, font-weight: 700)
항목:   fill="#BE123C"  (font-size: 10~10.5)
경고항목: fill="#DC2626"
```

---

## 타이포그래피 규칙

| 요소 | font-size | font-weight | 사용처 |
|------|-----------|-------------|--------|
| 캔버스 제목 | 22px | 800 | 타이틀 헤더 메인 |
| 서비스 서브라벨 | 10px | 700 | 타이틀 헤더 상단 (대문자, letter-spacing: 2.5) |
| 섹션 제목 | 18px | 800 | 섹션 구분 헤더 |
| 섹션 서브라벨 | 10px | 700 | 섹션 헤더 상단 (letter-spacing: 2) |
| 노드 메인 제목 | 16px | 800 | 스텝 노드 제목 |
| 노드 스텝라벨 | 10px | 700 | STEP N · LABEL (letter-spacing: 1.5) |
| 노드 부제목 | 11px | 400 | 스텝 노드 설명 |
| 시스템 노드 제목 | 13px | 700 | 시스템 처리 노드 |
| 분기 다이아몬드 텍스트 | 11~12px | 700 | 판단 기준 |
| 주석 제목 | 11px | 700 | 스티키 노트 제목 |
| 주석 항목 | 10px | 400 | 스티키 노트 항목 |
| 케이스 소제목 | 11px | 700 | 예외 케이스 라벨 |
| 범례 텍스트 | 11.5px | 500 | 범례 바 항목 |
| 화살표 라벨 | 9~10px | 400~600 | 분기 라벨 (예/아니오) |
| 푸터 텍스트 | 10.5px | 400 | 푸터 좌우 |
| 버전/날짜 | 11px | 400 | 타이틀 우상단 |