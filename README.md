# 북클럽 3.0 하이브리드 설정 시스템

**프로젝트명**: Universal Settings
**상태**: 🟢 Prototype Complete
**최종 업데이트**: 2025-02-10

---

## 🎯 프로젝트 개요

**하나의 앱, 세 가지 경험**

전용 패드(웅진 패드)와 개인 패드(BYOD) 환경이 공존하는 북클럽 3.0 서비스를 위한 **사용자 유형별 최적화된 설정 시스템**.

---

## 📁 파일 구조

### 1. PRD 문서
**파일**: `북클럽3.0_하이브리드설정_PRD_v1.0.md`
- 사용자 타입별 설정 정의 (3-Tier Structure)
- 핵심 기능 요구사항 (다이내믹 메뉴, 동기화, 종료 UX)
- 기술 구현 가이드 (Device Sensing, Settings Persistence)
- 장애 및 보안 시나리오

### 2. 프로토타입 (HTML)
**파일**: `북클럽3.0_하이브리드설정_프로토타입_v1.0.html`
- **React 18** + **Tailwind CSS**
- 3가지 사용자 타입 실시간 시뮬레이션
- 웅진 브랜드 컬러 적용
- 인터랙티브 토글/슬라이더

---

## 🎨 사용자 타입 (3-Tier)

### Type 1: 전용 패드 회원 🏢
```
is_woongjin_device = true
is_member = true

노출 메뉴:
✅ 기기 제어 (밝기, 음량, 블루라이트, Wi-Fi)
✅ 멤버십 (포인트, 구매내역, 쿠폰)
✅ 학습 옵션 (모드, KRS 자동조정)
✅ 앱 설정
✅ 계정 관리

하단 버튼:
[🚪 로그아웃] [🏠 서비스 나가기]
```

### Type 2: 개인 패드 회원 👤
```
is_woongjin_device = false
is_member = true

노출 메뉴:
❌ 기기 제어 (숨김)
✅ 멤버십 (포인트, 구매내역, 쿠폰)
✅ 학습 옵션 (모드, KRS 자동조정)
✅ 앱 설정
✅ 계정 관리

하단 버튼:
[🚪 로그아웃]
```

### Type 3: 일반 회원 🎈
```
is_woongjin_device = false
is_member = false

노출 메뉴:
❌ 기기 제어 (숨김)
🔒 멤버십 (마스킹 - "✨ 정규 회원 전용")
🔒 학습 옵션 (마스킹 - "✨ 정규 회원 전용")
✅ 앱 설정
✅ 계정 관리

하단 버튼:
[🚪 로그아웃]
```

---

## 💡 핵심 기능

### 1. 다이내믹 메뉴 렌더링
- 사용자 타입에 따라 메뉴가 실시간으로 변경
- 조건부 렌더링으로 불필요한 메뉴 숨김
- 마스킹 처리로 전환 유도

### 2. 기기 제어 (Type 1 전용)
```javascript
// 안드로이드 시스템 API 호출
- 화면 밝기: 0-100% 슬라이더
- 음량: 0-100% 슬라이더
- 블루라이트 필터: ON/OFF 토글
- Wi-Fi: 연결/해제 토글
```

### 3. 멤버십 관리 (Type 1, 2)
```javascript
// 계정 기반 동기화
- 포인트 통장 (실시간 API 조회)
- 구매 내역 (최근 30일)
- 쿠폰함 (사용 가능 쿠폰)
```

### 4. 학습 옵션 (Type 1, 2)
```javascript
// KRS 엔진 연동
- 학습 모드: 쉬움 😊 / 보통 😎 / 어려움 🤓
- KRS 자동 조정: ON/OFF
- 학습 리포트
```

### 5. 마스킹 & 전환 유도 (Type 3)
```javascript
// 클릭 시 팝업
showUpgradeModal({
  title: '✨ 정규 회원 전환',
  benefits: [
    '포인트 적립 & 사용',
    '구매 내역 관리',
    '맞춤형 학습 옵션',
    '프리미엄 콘텐츠 무제한'
  ]
});
```

### 6. 종료 UX
**Type 1 (전용 패드):**
- 🏠 **서비스 나가기**: 앱 종료 → 웅진 런처로 복귀

**Type 2, 3 (개인 패드):**
- 🚪 **로그아웃**: 표준 로그아웃 처리

---

## 🎮 프로토타입 시연

### 실행 방법
```bash
# HTML 파일 열기
open 북클럽3.0_하이브리드설정_프로토타입_v1.0.html
```

### 시뮬레이터 사용법
```
1. 상단 "사용자 타입 시뮬레이터" 탭 확인
2. Type 1 / Type 2 / Type 3 버튼 클릭
3. 메뉴가 실시간으로 변경되는 것 확인

테스트 시나리오:
- Type 1 → 모든 메뉴 노출 확인
- Type 2 → 기기 제어 숨김 확인
- Type 3 → 멤버십/학습옵션 마스킹 확인
- 슬라이더 조작 → 값 변경 확인
- 토글 클릭 → ON/OFF 전환 확인
```

---

## 🎨 디자인 시스템

### 웅진 브랜드 컬러
```css
/* Primary Colors */
--woongjin-orange: #FF8C42
--woongjin-yellow: #FFB84D
--woongjin-gold: #FFC837

/* Gradient */
background: linear-gradient(135deg,
  #FF8C42 0%,
  #FFB84D 50%,
  #FFC837 100%
);

/* Background */
--bg-soft: #FFF8F0
--bg-light: #FFF4E6
```

### 컴포넌트 스타일
```css
/* 섹션 카드 */
border-radius: 16px
shadow: 0 2px 8px rgba(0,0,0,0.1)

/* 토글 스위치 */
width: 52px
height: 28px
background: woongjin-gradient (active)

/* 슬라이더 */
track-height: 8px
thumb-size: 20px
thumb-color: woongjin-gradient
```

---

## 🔧 기술 스택

### Frontend
- **React 18** (Hooks: useState, useEffect, useMemo)
- **Tailwind CSS** (Utility-first CSS)
- **Babel Standalone** (JSX 트랜스파일)

### 주요 기능
```javascript
// 1. 조건부 렌더링
{currentType.isWoongjinDevice && (
  <DeviceControlSection />
)}

// 2. 마스킹 오버레이
<div className={!isMember ? 'masked-overlay' : ''}>
  <Section />
  {!isMember && <MaskLabel />}
</div>

// 3. 인터랙티브 컨트롤
<input
  type="range"
  value={brightness}
  onChange={(e) => setBrightness(e.target.value)}
/>
```

---

## 📊 구현 로드맵

### Phase 1: 기본 구조 (1주)
- [ ] 사용자 타입 판별 로직
- [ ] 3가지 타입별 레이아웃
- [ ] 섹션별 조건부 렌더링

### Phase 2: 기기 제어 (1주)
- [ ] 안드로이드 시스템 API 연동
- [ ] 밝기/음량 슬라이더
- [ ] 블루라이트 필터/Wi-Fi 토글

### Phase 3: 멤버십 연동 (2주)
- [ ] 포인트 API 연동
- [ ] 구매 내역 조회
- [ ] 쿠폰 시스템
- [ ] 실시간 동기화

### Phase 4: 학습 옵션 (1주)
- [ ] 학습 모드 설정
- [ ] KRS 엔진 연동
- [ ] 학습 리포트

### Phase 5: 종료 UX (1주)
- [ ] 서비스 나가기 (Type 1)
- [ ] 로그아웃 처리
- [ ] 세션 관리

### Phase 6: 마스킹 및 유도 (1주)
- [ ] Type 3 마스킹 UI
- [ ] 회원 전환 유도 팝업
- [ ] A/B 테스트 준비

**총 예상 기간**: 7주

---

## 🔍 주요 의사결정 사항

### 1. Device Sensing
```kotlin
// 방법 1: 단말기 모델명
Build.MODEL.contains("WOONGJIN")

// 방법 2: 전용 런처 설치 여부
packageManager.getPackageInfo("com.woongjin.launcher", 0)

// 최종 판별
val isWoongjinDevice = isWoongjinDevice() || hasWoongjinLauncher()
```

### 2. Settings Persistence
| 설정 유형 | 저장 위치 | 동기화 |
|----------|----------|--------|
| 기기 설정 | SharedPreferences (로컬) | ❌ |
| 학습/멤버십 | 서버 DB | ✅ |
| 앱 설정 | 서버 DB + 로컬 캐시 | ✅ |

### 3. Exit Strategy
**Type 1 (전용 패드):**
```java
// 앱 종료 → 런처 복귀
finishAndRemoveTask();
startActivity(launcherIntent);
System.exit(0);
```

**Type 2, 3 (개인 패드):**
```javascript
// 표준 로그아웃
clearLocalStorage();
await api.logout();
navigateTo('/login');
```

---

## 🧪 테스트 체크리스트

### 기능 테스트
- [ ] Type 1 → Type 2 전환 시 기기 제어 숨김
- [ ] Type 2 → Type 3 전환 시 멤버십/학습 마스킹
- [ ] Type 3 마스킹 클릭 시 유도 팝업
- [ ] 슬라이더 조작 시 값 즉시 반영
- [ ] 토글 클릭 시 상태 즉시 전환
- [ ] 네트워크 단절 시 오프라인 메시지
- [ ] 로그아웃 시 캐시 삭제 및 UI 업데이트

### 성능 테스트
- [ ] 타입 전환 리렌더링 < 300ms
- [ ] API 응답 시간 < 500ms (p95)
- [ ] 메모리 사용량 < 100MB

### UX 테스트
- [ ] 웅진 브랜드 컬러 일관성
- [ ] 애니메이션 부드러움 (60fps)
- [ ] 터치 피드백 즉각성

---

## 🚨 리스크 & 고려사항

### 1. 기기 판별 정확도
**리스크**: 웅진 패드를 개인 패드로 오인식
**대응**: 복수 판별 방법 적용 (모델명 + 런처)

### 2. 네트워크 의존성
**리스크**: 오프라인 시 멤버십 메뉴 사용 불가
**대응**: 캐시 데이터 활용 + 오프라인 모드 안내

### 3. 마스킹 우회 시도
**리스크**: Type 3 사용자의 API 직접 호출
**대응**: 서버 측 멤버십 검증 필수

### 4. 런처 복귀 실패
**리스크**: "서비스 나가기" 시 런처 실행 실패
**대응**: Fallback으로 홈 화면 이동

---

## 📞 문의 및 협업

### 문서 관련
- **PRD**: 비즈니스 요구사항, 기능 명세
- **Prototype**: 실제 동작 확인, 시뮬레이션

### 다음 회의
- **일시**: 2025-02-17 (월) 14:00
- **안건**: 프로토타입 데모, Phase 1 착수
- **준비 자료**: 기술 스펙 확정, API 설계

---

## 📝 변경 이력

| 버전 | 날짜 | 작성자 | 변경 내용 |
|------|------|--------|----------|
| v1.0 | 2025-02-10 | Claude | 초안 작성 (PRD + Prototype) |

---

**프로젝트 상태**: 🟢 Prototype Complete
**다음 단계**: Phase 1 기본 구조 개발 착수
