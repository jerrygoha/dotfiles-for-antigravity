# Agoda Hunter UI 디자인 가이드

다른 프로젝트에서 Agoda Hunter의 UI 디자인을 재사용하기 위한 가이드입니다.

---

## 1. 기술 스택

| 항목 | 사용 기술 |
|------|----------|
| **프레임워크** | Next.js 16+ (App Router) |
| **스타일링** | Tailwind CSS v4 |
| **폰트** | Pretendard (한글), Inter (영문) |
| **색상 시스템** | OKLCH (지각적으로 균일한 색상 공간) |
| **아이콘** | Inline SVG, Emoji |

---

## 2. 색상 시스템 (OKLCH)

### 왜 OKLCH인가?
- 지각적으로 균일한 색상 공간 (밝기, 채도가 자연스럽게 변함)
- `oklch(밝기 채도 색상)` 형식

### 브랜드 컬러

```css
:root {
  /* Primary: Indigo/Violet */
  --primary: oklch(0.55 0.25 265);
  --brand-primary: oklch(0.55 0.25 265);
  --brand-secondary: oklch(0.6 0.2 290);  /* Purple */
  
  /* 성공/최저가 그린 */
  --success: oklch(0.55 0.18 155);
  --success-light: oklch(0.92 0.08 155);
  
  /* 경고 오렌지 */
  --warning: oklch(0.75 0.18 55);
  --orange: oklch(0.7 0.2 45);
  
  /* 정보 블루 */
  --info: oklch(0.6 0.18 240);
}
```

### 색상 사용 예시

```tsx
// Tailwind에서 사용
<div className="text-primary bg-success-light" />

// CSS 변수로 사용
<div style={{ color: 'var(--brand-primary)' }} />
```

---

## 3. 타이포그래피

### 폰트 설정

```css
/* globals.css */
@theme inline {
  --font-sans: "Pretendard", "Inter", system-ui, sans-serif;
}
```

### 폰트 CDN

```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.min.css"
/>
```

### 헤딩 스타일

| 용도 | 클래스 |
|------|--------|
| Hero 타이틀 | `text-3xl sm:text-5xl md:text-7xl font-bold tracking-tight` |
| 섹션 타이틀 | `text-2xl sm:text-3xl font-bold` |
| 카드 타이틀 | `text-xl font-bold` |
| 본문 | `text-base text-slate-600 leading-relaxed` |
| 캡션 | `text-sm text-slate-500` |

---

## 4. 그라데이션 패턴

### 텍스트 그라데이션

```tsx
<span className="bg-gradient-to-r from-violet-600 via-indigo-600 to-purple-600 bg-clip-text text-transparent">
  Secret Prices
</span>
```

### 애니메이션 그라데이션



```css
.animate-gradient {
  animation: gradient-x 3s ease infinite;
  background-size: 200% auto;
}

@keyframes gradient-x {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

### 버튼 그라데이션

```tsx
<button className="bg-gradient-to-r from-violet-600 to-indigo-600 hover:from-violet-700 hover:to-indigo-700 shadow-lg shadow-violet-500/30">
  최저가 찾기
</button>
```

### 배경 그라데이션

```tsx
<div className="bg-gradient-to-br from-violet-50/50 via-white to-indigo-50/50" />
```

---

## 5. 카드 컴포넌트

### 기본 카드 (호버 효과)

```tsx
<div className="group relative bg-white border border-slate-200/70 rounded-2xl p-8 hover:border-slate-300 transition-all duration-200 hover:shadow-lg hover:-translate-y-0.5">
  {/* 호버 시 그라데이션 오버레이 */}
  <div className="absolute inset-0 bg-gradient-to-br from-violet-500/5 to-purple-500/5 rounded-2xl opacity-0 group-hover:opacity-100 transition-opacity" />
  
  <div className="relative">
    {/* 아이콘 */}
    <div className="w-12 h-12 bg-violet-100 rounded-xl flex items-center justify-center text-2xl mb-4 group-hover:scale-110 transition-transform duration-300">
      🛡️
    </div>
    <h3 className="text-xl font-bold text-slate-900 mb-2">제목</h3>
    <p className="text-slate-600 leading-relaxed text-sm">설명</p>
  </div>
</div>
```

### 글로우 효과 (입력 폼)

```tsx
<div className="relative group">
  {/* 글로우 배경 */}
  <div className="absolute -inset-0.5 bg-gradient-to-r from-violet-500 to-indigo-500 rounded-2xl blur opacity-30 group-hover:opacity-60 transition duration-1000 group-hover:duration-200" />
  
  {/* 실제 컨텐츠 */}
  <div className="relative bg-white rounded-xl shadow-xl p-2">
    {/* ... */}
  </div>
</div>
```

---

## 6. 애니메이션

### Fade In Up

```css
.animate-fade-in-up {
  animation: fade-in-up 0.8s ease-out forwards;
  opacity: 0;
  transform: translateY(20px);
}

@keyframes fade-in-up {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

### Shake (에러)

```css
.animate-shake {
  animation: shake 0.5s cubic-bezier(.36, .07, .19, .97) both;
}

@keyframes shake {
  10%, 90% { transform: translate3d(-1px, 0, 0); }
  20%, 80% { transform: translate3d(2px, 0, 0); }
  30%, 50%, 70% { transform: translate3d(-4px, 0, 0); }
  40%, 60% { transform: translate3d(4px, 0, 0); }
}
```

---

## 7. 배지 & 라벨

### 상단 배지

```tsx
<div className="inline-block mb-4 px-4 py-1.5 rounded-full border border-violet-200 bg-violet-50 text-sm font-medium text-violet-700 shadow-sm">
  ✨ 숨겨진 가격을 찾아드려요
</div>
```

### 태그 배지

```tsx
<span className="text-violet-600 text-xs font-semibold bg-violet-50 inline-block px-2 py-1 rounded">
  안전한 접속 보장
</span>
```

### 절약액 배지

```css
.badge-savings {
  @apply inline-flex items-center gap-1 px-2.5 py-1 rounded-full text-xs font-semibold;
  background: oklch(0.92 0.08 155);
  color: oklch(0.35 0.15 155);
}
```

---

## 8. 레이아웃

### 컨테이너

```tsx
<div className="container max-w-screen-xl mx-auto px-4 py-12 md:py-20">
```

### 그리드

```tsx
{/* 2열 그리드 */}
<div className="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto">

{/* 3열 그리드 */}
<div className="grid md:grid-cols-3 gap-8">
```

---

## 9. 인터랙션 패턴

### 호버 효과

```tsx
// 스케일 업
className="hover:scale-[1.02] active:scale-[0.98] transition-all"

// Y축 이동
className="hover:-translate-y-0.5 transition-all duration-200"

// 아이콘 확대
className="group-hover:scale-110 transition-transform duration-300"
```

### 트랜지션

```tsx
// 표준 트랜지션
className="transition-all duration-200"

// 호버 시 빠른 반응
className="transition duration-1000 group-hover:duration-200"
```

---

## 10. 복사해서 사용하기

### globals.css 필수 변수

```css
@import "tailwindcss";

@theme inline {
  --color-primary: var(--primary);
  --font-sans: "Pretendard", "Inter", system-ui, sans-serif;
}

:root {
  --radius: 0.625rem;
  --primary: oklch(0.55 0.25 265);
  --background: oklch(0.985 0.002 247);
  --foreground: oklch(0.145 0.02 265);
  --success: oklch(0.55 0.18 155);
  --warning: oklch(0.75 0.18 55);
}
```

### 필수 CDN

```html
<!-- Pretendard 폰트 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.min.css" />
```

---

## 11. 디자인 원칙 요약

| 원칙 | 적용 |
|------|------|
| **색상** | Violet/Indigo 그라데이션 중심, OKLCH 시스템 |
| **그림자** | `shadow-lg shadow-violet-500/30` (컬러 섀도우) |
| **모서리** | `rounded-xl`, `rounded-2xl` (부드러운 곡선) |
| **호버** | 스케일업 + 그라데이션 오버레이 |
| **깊이** | 글로우 배경, 멀티레이어 그라데이션 |
