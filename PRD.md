# HTML/CSS 구조 가이드라인 (PRD)

## 목차
1. HTML 구조 규칙
2. CSS 클래스명 규칙
3. ID 명명 규칙
4. 예시

---

## 1. HTML 구조 규칙

### 전체 구조
```
<body>
  <header class="header">         <!-- 고정 네비게이션 -->
    <nav class="navbar">
      <!-- 네비게이션 콘텐츠 -->
    </nav>
  </header>

  <main class="hero">             <!-- 메인 히어로 섹션 (한 번만) -->
    <!-- 히어로 콘텐츠 -->
  </main>

  <section class="[name]-section"> <!-- 각 섹션들 -->
    <!-- 섹션 콘텐츠 -->
  </section>

  <footer class="footer">         <!-- 풋터 -->
    <!-- 풋터 콘텐츠 -->
  </footer>
</body>
```

### 각 요소별 설명
- `<header class="header">`: 전체 네비게이션 래퍼 (position: fixed)
- `<nav class="navbar">`: 실제 네비게이션 바
- `<main class="hero">`: 메인 히어로 섹션 (한 페이지에 한 번만)
- `<section class="[name]-section">`: 콘텐츠 섹션들
- `<footer class="footer">`: 풋터 영역

---

## 2. CSS 클래스명 규칙

### 섹션 클래스명 규칙
섹션은 다음과 같이 명명합니다:
```
class="[section-name]-section"
```

### 예시
| 섹션 | 클래스명 | id |
|------|---------|-----|
| 갤러리 | `gallery-section` | `gallery-section` |
| 비전 | `vision-section` | `vision-section` |
| 솔루션 | `solutions-section` | `solutions-section` |
| NEXUS 시스템 | `nexus-system-section` | `nexus-system-section` |

### 컴포넌트 클래스명
- 버튼: `.btn-[type]` (예: `.btn-login`, `.btn-circle`)
- 텍스트 스타일: `.text-[style]` (예: `.text-grey`)
- 제목: `.title-[level]` (예: `.title-large`)
- 컨테이너: `.container-[type]` (예: `.container-fluid`)

---

## 3. ID 명명 규칙

### 섹션 ID
ID는 class와 동일하게 사용합니다:
```
id="[section-name]-section"
```

### 내부 요소 ID
내부 요소는 필요한 경우만 ID를 부여하며, 다음 형식을 따릅니다:
```
id="[parent]-[element]"
```

예:
- `id="gallery-container"` (갤러리 내부 컨테이너)
- `id="gallery-center-wrapper"` (갤러리 중앙 래퍼)

---

## 4. CSS 규칙

### 섹션 스타일
모든 섹션은 다음과 같은 기본 스타일을 상속합니다:

```css
.vision-section,
.solutions-section,
.gallery-section,
.nexus-system-section {
    padding: 120px 0;
}
```

특수한 요구사항이 있는 경우만 override합니다:

```css
.solutions-section {
    padding: 0;  /* 특수 사항 */
}

.gallery-section {
    padding: 0;
    width: 100vw;
    margin-left: calc(-50vw + 50%);
}
```

---

## 5. 새 섹션 추가 체크리스트

새로운 섹션을 추가할 때는 다음을 확인하세요:

- [ ] HTML: `<section class="[name]-section" id="[name]-section">`
- [ ] CSS: `.section-class { ... }` 작성
- [ ] ID 네비게이션: href="#[name]-section"와 일치 확인
- [ ] JavaScript: 필요시 selector 수정 (예: `.gallery-section`)
- [ ] 반응형: @media 쿼리 작성 (필요시)

---

## 6. 현재 적용된 구조

### HTML 구조
```
Header
  ├─ Navbar
     ├─ Logo
     ├─ Nav Links (NEXUS 소개, 대시보드, 가뭄현황, 보고서)
     └─ Login Button

Main (Hero)
  └─ Hero Content

Gallery Section
  └─ Gallery Container

Vision Section
  └─ Vision Content

Solutions Section
  ├─ Water Solution
  ├─ Energy Solution
  └─ Food Solution

NEXUS System Section
  └─ System Content

Footer
  └─ Footer Content
```

---

## 7. CSS 코딩 규칙

### 포맷 규칙
**IMPORTANT: 다음 규칙을 반드시 준수합니다**

1. **한 줄 작성**: 각 selector와 properties는 한 줄로 작성
2. **띄어쓰기 제거**: 속성과 값 사이, 선택자와 중괄호 사이의 모든 불필요한 공간 제거
3. **마지막 세미콜론 제거**: 마지막 property 뒤의 세미콜론 삭제
4. **공백 최소화**: 콜론(:), 세미콜론(;) 바로 다음에 공백 없음

### 선택자 계층 규칙 (중요)
**IMPORTANT: 중복된 CSS를 피하기 위해 부모 선택자를 명시해야 합니다**

모든 요소는 그것이 속한 부모 컨텍스트를 명시적으로 포함해야 합니다.

#### 잘못된 예시 (금지)
```css
.logo{font-weight:700;font-size:22px}
.nav-links{display:flex;gap:40px}
.btn-login{font-size:15px}
```
❌ 어느 섹션의 요소인지 불명확하고 중복 가능성 높음

#### 올바른 예시
```css
.header .logo{font-weight:700;font-size:22px}
.navbar .nav-links{display:flex;gap:40px}
.nav-actions .btn-login{font-size:15px}
```
✅ 부모 선택자를 포함하여 정확한 컨텍스트 지정

### 선택자 계층 가이드
```
.header
├─ .header .navbar
│  ├─ .header .logo
│  ├─ .navbar .nav-links
│  │  └─ .nav-links a
│  └─ .navbar .nav-actions
│     ├─ .nav-actions .btn-share
│     ├─ .nav-actions .btn-login
│     └─ .nav-actions .btn-menu

.hero
├─ .hero .hero-bg
├─ .hero .hero-content
│  ├─ .hero .hero-title
│  ├─ .hero .hero-subtitle
│  └─ .hero .hero-link

.gallery-section
├─ .gallery-section .container
├─ .gallery-container
└─ 등등...
```

### 추가 선택자 원칙
- 전역 스타일 (body, a 등)은 부모 선택자 불필요
- 고유한 이름의 클래스 (`.vision-section`, `.footer` 등)는 부모 선택자 불필요
- 재사용되는 이름 (`.logo`, `.btn-login`, `.nav-links` 등)은 **반드시** 부모 선택자 포함

### 올바른 예시
```css
.header:hover .navbar{border-bottom-color:var(--border-light)}
.share-popup{position:absolute;top:100%;left:50%;transform:translateX(-50%);margin-top:12px;background:#f5f5f5}
.share-item{width:100%;padding:8px 16px;text-align:center;color:#666666}
```

### 잘못된 예시 (금지)
```css
.nav-links a:hover {
    color: var(--accent-blue);
}

.share-popup {
    position: absolute;
    ...
}
```

## @keyframes와 @media 특수 포맷 규칙

**IMPORTANT: @keyframes와 @media는 위의 한 줄 작성 규칙의 예외입니다**

1. **@keyframes**: 각 프레임을 새 줄에 배치
2. **@media**: 각 선택자를 새 줄에 배치하고 들여쓰기 적용

### @keyframes 올바른 예시
```css
@keyframes fadeInUp{
    to{opacity:1;transform:translateY(0)}
}
```

### @keyframes 잘못된 예시 (금지)
```css
@keyframes fadeInUp{to{opacity:1;transform:translateY(0)}}
```

### @media 올바른 예시
```css
@media(max-width:768px){
    .hero-title{font-size:48px}
    .hero{padding-top:90px}
    .vision-section .row{flex-direction:column;gap:30px}
    .impact-grid{grid-template-columns:1fr}
    .container-fluid{padding:0 20px}
    .navbar .nav-links{display:none}
    .gallery-section{width:100%;margin-left:0}
}
```

### @media 잘못된 예시 (금지)
```css
@media(max-width:768px){.hero-title{font-size:48px}.hero{padding-top:90px}.vision-section .row{flex-direction:column;gap:30px}.impact-grid{grid-template-columns:1fr}.container-fluid{padding:0 20px}.navbar .nav-links{display:none}.gallery-section{width:100%;margin-left:0}}
```

---

## 8. 디자인 제약사항

### border-radius와 box-shadow 규칙
**IMPORTANT: 다음을 명시적으로 지시받지 않는 한 적용하지 않습니다**

1. **border-radius**: 사용자가 명확히 요청하지 않으면 추가하지 않음
2. **box-shadow**: 그림자 효과는 특별히 지시받지 않으면 제거

### 예외 경우
- 사용자가 "border-radius를 8px 추가해줘"라고 명시적으로 요청
- "그림자 효과를 넣어줘"라고 직접 지시

---

## 9. 주의사항

1. **class와 id 일관성**: 섹션의 class와 id는 항상 동일해야 합니다.
2. **selector 업데이트**: CSS/JS에서 클래스명을 변경했다면, 모든 selector를 확인하세요.
3. **네이밍 컨벤션**: kebab-case(소문자-하이픈) 사용
4. **padding/margin**: 섹션 기본 padding은 120px 0 (특수한 경우만 변경)

---

## 10. 참고

- 모든 섹션에는 고유한 class와 id가 필요합니다.
- 컨테이너의 max-width는 1400px입니다.
- 고정 헤더 높이는 90px입니다.
