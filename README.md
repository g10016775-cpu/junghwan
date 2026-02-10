# 북클럽 3.0 하이브리드 설정 시스템

**프로젝트명**: Universal Settings
**상태**: 🟢 Prototype Complete
**최종 업데이트**: 2025-02-10

---

## 🎯 프로젝트 개요

**하나의 앱, 두 가지 경험**

전용 패드(웅진 패드)와 개인 패드(BYOD) 환경이 공존하는 북클럽 3.0 서비스를 위한 **사용자 유형별 최적화된 설정 시스템**.

---

## 📁 파일 구조

### 1. PRD 문서
**파일**: `북클럽3.0_하이브리드설정_PRD_v1.0.md`
- 사용자 타입별 설정 정의 (2-Tier Structure)
- 핵심 기능 요구사항 (다이내믹 메뉴, 자물쇠 보호, 종료 UX)
- 기술 구현 가이드 (Device Sensing, Settings Persistence)
- 장애 및 보안 시나리오

### 2. 프로토타입 (HTML)
**파일**: `북클럽3.0_하이브리드설정_프로토타입_v1.0.html`
- **React 18** + **Tailwind CSS**
- 2가지 사용자 타입 실시간 시뮬레이션
- 웅진 브랜드 컬러 적용
- 인터랙티브 토글/슬라이더

---

## 🎨 사용자 타입 (2-Tier)

### 전용 패드 회원 🏢
```
가입 경로: 웅진 전용 패드 구매 + 통합 멤버십
is_woongjin_device = true

노출 메뉴:
✅ 기기 제어 (밝기, 음량, 블루라이트, Wi-Fi)
✅ 멤버십 🔒 (포인트, 구매내역, 쿠폰)
✅ 학습 옵션 🔒 (모드, KRS 자동조정)
✅ 앱 설정
✅ 계정 관리 🔒

하단 버튼:
[🚪 로그아웃] [🏠 서비스 나가기 🔒]

특징:
- 자물쇠 🔒 보호 (부모 통제)
- 웅진 생태계 통합 (포인트, 구매내역 연동)
- 런처 연동 (서비스 나가기)
```

### 개인 패드 회원 👤
```
가입 경로: 홈페이지/앱스토어 독립 가입
is_woongjin_device = false

노출 메뉴:
❌ 기기 제어 (숨김)
❌ 멤버십 연동 없음
✅ 북클럽 3.0 콘텐츠 이용
✅ 기본 학습 기능
✅ 앱 설정
✅ 계정 관리

하단 버튼:
[🚪 로그아웃]

특징:
- 자물쇠 없음
- 독립 구독 서비스
- 웅진 생태계 통합 없음
```

---

## 💡 핵심 기능

### 1. 다이내믹 메뉴 렌더링
- 사용자 타입에 따라 메뉴가 실시간으로 변경
- 조건부 렌더링으로 불필요한 메뉴 숨김
- 전용 패드 전용 기능 분리

### 2. 기기 제어 (전용 패드 전용)
```javascript
// 안드로이드 시스템 API 호출
- 화면 밝기: 0-100% 슬라이더
- 음량: 0-100% 슬라이더
- 블루라이트 필터: ON/OFF 토글
- Wi-Fi: 연결/해제 토글
```

### 3. 멤버십 관리 (전용 패드 전용)
```javascript
// 웅진 통합 멤버십 연동
- 포인트 통장 (실시간 API 조회)
- 구매 내역 (최근 30일)
- 쿠폰함 (사용 가능 쿠폰)

🔒 자물쇠 보호: 비밀번호 입력 필요
```

### 4. 학습 옵션 (전용 패드: 고급 / 개인 패드: 기본)
```javascript
// 전용 패드: KRS 엔진 연동
- 학습 모드: 쉬움 😊 / 보통 😎 / 어려움 🤓
- KRS 자동 조정: ON/OFF
- 학습 리포트
🔒 자물쇠 보호

// 개인 패드: 기본 기능만
- 간단한 학습 통계
```

### 5. 자물쇠 보호 (전용 패드 전용)
```javascript
// 부모 통제 (Parental Control)
목적: 아동의 무단 이탈 방지

보호 대상:
- 💎 멤버십 (결제, 포인트 사용)
- 📚 학습 옵션 (설정 변경)
- 👤 계정 관리 (탈퇴 등)
- 🏠 서비스 나가기 (런처 복귀)

클릭 시:
"보호자 비밀번호를 입력하세요"
→ 비밀번호 맞으면 접근 허용
```

### 6. 종료 UX
**전용 패드:**
- 🏠 **서비스 나가기 🔒**: 앱 종료 → 웅진 런처로 복귀 (비밀번호 필요)
- 🚪 **로그아웃**: 계정 로그아웃

**개인 패드:**
- 🚪 **로그아웃**: 계정 로그아웃 (서비스 나가기 버튼 없음)

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
2. 전용 패드 / 개인 패드 버튼 클릭
3. 메뉴가 실시간으로 변경되는 것 확인

테스트 시나리오:
- 전용 패드 → 모든 메뉴 노출, 자물쇠 확인
- 개인 패드 → 기기 제어 숨김, 간단한 UI 확인
- 슬라이더 조작 → 값 변경 확인
- 토글 클릭 → ON/OFF 전환 확인
- 자물쇠 메뉴 클릭 → 비밀번호 팝업 확인
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

/* 자물쇠 아이콘 */
color: #6B7280
size: 16px
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
{isWoongjinDevice && (
  <DeviceControlSection />
)}

// 2. 자물쇠 보호
{isWoongjinDevice && (
  <Section
    title="멤버십 🔒"
    onClick={handlePasswordPrompt}
  />
)}

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
- [ ] 사용자 타입 판별 로직 (전용 패드 vs 개인 패드)
- [ ] 2가지 타입별 레이아웃
- [ ] 섹션별 조건부 렌더링

### Phase 2: 기기 제어 (1주)
- [ ] 안드로이드 시스템 API 연동
- [ ] 밝기/음량 슬라이더
- [ ] 블루라이트 필터/Wi-Fi 토글

### Phase 3: 멤버십 연동 (2주)
- [ ] 웅진 통합 멤버십 API 연동
- [ ] 포인트 API 연동
- [ ] 구매 내역 조회
- [ ] 쿠폰 시스템

### Phase 4: 자물쇠 보호 (1주)
- [ ] 비밀번호 입력 팝업
- [ ] 보호 메뉴 설정
- [ ] 비밀번호 검증 로직
- [ ] 실패 시 에러 처리

### Phase 5: 종료 UX (1주)
- [ ] 서비스 나가기 (전용 패드)
- [ ] 서비스 나가기 자물쇠 보호
- [ ] 로그아웃 처리
- [ ] 세션 관리

### Phase 6: 학습 옵션 (1주)
- [ ] 전용 패드: 고급 학습 모드 설정
- [ ] 전용 패드: KRS 엔진 연동
- [ ] 개인 패드: 기본 학습 통계

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
| 설정 유형 | 전용 패드 | 개인 패드 |
|----------|----------|----------|
| 기기 설정 | SharedPreferences (로컬) | - |
| 멤버십 설정 | 서버 DB (웅진 통합) | - |
| 학습 옵션 | 서버 DB + KRS 연동 | 로컬 DB |
| 앱 설정 | 서버 DB + 로컬 캐시 | 로컬 DB |

### 3. Exit Strategy
**전용 패드:**
```java
// 앱 종료 → 런처 복귀 (자물쇠 보호)
if (verifyParentPassword(password)) {
  finishAndRemoveTask();
  startActivity(launcherIntent);
  System.exit(0);
}
```

**개인 패드:**
```javascript
// 표준 로그아웃
clearLocalStorage();
await api.logout();
navigateTo('/login');
```

### 4. 자물쇠 보호
```kotlin
// 보호 대상 메뉴
val lockedMenus = listOf(
  Menu.MEMBERSHIP,      // 멤버십 (포인트, 구매내역)
  Menu.LEARNING_OPTIONS, // 학습 옵션
  Menu.ACCOUNT_MANAGE,   // 계정 관리
  Menu.SERVICE_EXIT      // 서비스 나가기
)

fun handleMenuClick(menu: Menu) {
  if (isWoongjinDevice && menu in lockedMenus) {
    showPasswordPrompt { password ->
      if (verifyParentPassword(password)) {
        navigateTo(menu)
      }
    }
  } else {
    navigateTo(menu)
  }
}
```

---

## 🧪 테스트 체크리스트

### 기능 테스트
- [ ] 전용 패드 → 개인 패드 전환 시 기기 제어 숨김
- [ ] 전용 패드 → 개인 패드 전환 시 멤버십 메뉴 숨김
- [ ] 전용 패드에서 자물쇠 메뉴 클릭 시 비밀번호 팝업
- [ ] 비밀번호 정확 입력 시 메뉴 접근
- [ ] 비밀번호 오입력 시 에러 메시지
- [ ] 슬라이더 조작 시 값 즉시 반영
- [ ] 토글 클릭 시 상태 즉시 전환
- [ ] 서비스 나가기 자물쇠 보호 동작

### 성능 테스트
- [ ] 타입 전환 리렌더링 < 300ms
- [ ] API 응답 시간 < 500ms (p95)
- [ ] 메모리 사용량 < 100MB

### UX 테스트
- [ ] 웅진 브랜드 컬러 일관성
- [ ] 애니메이션 부드러움 (60fps)
- [ ] 터치 피드백 즉각성
- [ ] 자물쇠 아이콘 명확성

---

## 🚨 리스크 & 고려사항

### 1. 기기 판별 정확도
**리스크**: 웅진 패드를 개인 패드로 오인식
**대응**: 복수 판별 방법 적용 (모델명 + 런처)

### 2. 비밀번호 분실
**리스크**: 부모가 비밀번호를 잊어버림
**대응**: 고객센터 본인 인증 후 초기화

### 3. 멤버십 API 의존성
**리스크**: 오프라인 시 멤버십 메뉴 사용 불가
**대응**: 캐시 데이터 활용 + 오프라인 모드 안내

### 4. 런처 복귀 실패
**리스크**: "서비스 나가기" 시 런처 실행 실패
**대응**: Fallback으로 홈 화면 이동

---

## 📊 비즈니스 모델 비교

| 구분 | 전용 패드 회원 | 개인 패드 회원 |
|------|---------------|---------------|
| **결제 경로** | 패드 구매 + 통합 멤버십 | 홈페이지/앱 독립 구독 |
| **타겟** | 프리미엄 고객 | 가벼운 시작 고객 |
| **포인트 적립** | ✅ 통합 포인트 | ❌ 없음 |
| **구매내역 연동** | ✅ 웅진 전체 | ❌ 없음 |
| **학습 관리** | ✅ 고급 KRS | ⚪ 기본 수준 |
| **자물쇠 보호** | 🔒 적용 | ❌ 없음 |
| **서비스 연동** | ✅ 웅진 생태계 | ❌ 독립 운영 |

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
| v1.0 | 2025-02-10 | Claude | 초안 작성 (3-Tier) |
| v2.0 | 2025-02-10 | Claude | 2-Tier 구조로 단순화 |

---

**프로젝트 상태**: 🟢 Prototype Complete
**다음 단계**: Phase 1 기본 구조 개발 착수
