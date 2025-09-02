# Shashboard - Modern Dashboard Template

Nuxt 3 + shadcn-vue + Tailwind CSS로 구축된 현대적이고 반응형 대시보드 템플릿입니다.

## ✨ 주요 기능

- **최신 기술 스택**: Nuxt 3, Vue 3, TypeScript
- **Modern UI**: shadcn-vue 컴포넌트 라이브러리
- **반응형 디자인**: Tailwind CSS를 활용한 모바일 친화적 레이아웃
- **다크/라이트 테마**: CSS 변수 기반 테마 시스템
- **사이드바 네비게이션**: 데스크톱은 고정, 모바일은 햄버거 메뉴
- **대시보드 페이지**: 통계 카드, 테이블, 차트 placeholder
- **사용자 관리**: 사용자 목록 및 관리 기능
- **설정 페이지**: 일반, 보안, 알림, 시스템 설정

## 🚀 빠른 시작

### 1. 의존성 설치

```bash
npm install
# 또는
yarn install
# 또는
pnpm install
```

### 2. 개발 서버 실행

```bash
npm run dev
# 또는
yarn dev
# 또는
pnpm dev
```

브라우저에서 [http://localhost:3000](http://localhost:3000)에 접속하세요.

### 3. 프로덕션 빌드

```bash
npm run build
npm run preview
```

## 📁 프로젝트 구조

```
shashboard/
├── assets/
│   └── css/
│       └── main.css           # Tailwind CSS 및 shadcn-vue 스타일
├── components/
│   ├── icons/
│   │   └── Icon.vue           # 아이콘 컴포넌트
│   └── ui/                    # shadcn-vue UI 컴포넌트들
│       ├── Button.vue
│       ├── Card.vue
│       ├── Input.vue
│       ├── Table.vue
│       └── ...
├── layouts/
│   └── dashboard.vue          # 메인 대시보드 레이아웃
├── lib/
│   └── utils.ts               # 유틸리티 함수 (cn 등)
├── pages/
│   ├── index.vue              # 홈 페이지 (대시보드로 리다이렉트)
│   ├── dashboard.vue          # 대시보드 페이지
│   ├── users.vue              # 사용자 관리 페이지
│   └── settings.vue           # 설정 페이지
├── package.json               # 프로젝트 설정 및 의존성
├── nuxt.config.ts             # Nuxt 3 설정
├── tailwind.config.js         # Tailwind CSS 설정
└── app.vue                    # 루트 컴포넌트
```

## 🎨 UI 컴포넌트

이 템플릿에는 다음과 같은 shadcn-vue 컴포넌트가 포함되어 있습니다:

- **Button**: 다양한 variant와 size 지원
- **Card**: CardHeader, CardContent, CardTitle 포함
- **Input**: 폼 입력 요소
- **Table**: TableHeader, TableBody, TableRow, TableHead, TableCell 포함
- **Icon**: Lucide Vue Next 아이콘 래퍼

## 📱 반응형 디자인

- **데스크톱 (lg 이상)**: 사이드바가 항상 표시됨
- **태블릿/모바일**: 햄버거 메뉴로 사이드바 토글
- **Grid 시스템**: Tailwind CSS responsive 클래스 활용

## 🔧 커스터마이징

### 테마 색상 변경

`assets/css/main.css`에서 CSS 변수를 수정하여 테마 색상을 변경할 수 있습니다.

### 새 페이지 추가

1. `pages/` 디렉토리에 새 Vue 파일 생성
2. `layouts/dashboard.vue`의 navigation 배열에 메뉴 항목 추가

### 새 컴포넌트 추가

`components/ui/` 디렉토리에 shadcn-vue 스타일의 새 컴포넌트를 추가할 수 있습니다.

## 🛠 추가 개발 권장사항

- **차트 라이브러리**: Chart.js, ApexCharts, 또는 Recharts 추가
- **폼 검증**: Vee-Validate 또는 Formkit 통합
- **상태 관리**: Pinia 추가 (복잡한 상태 관리 필요 시)
- **API 연동**: Nuxt 3의 $fetch나 useFetch 활용
- **인증**: Nuxt Auth 또는 커스텀 인증 시스템
- **다국어**: @nuxtjs/i18n 모듈 추가

## 📄 라이선스

MIT License - 자유롭게 사용하세요!

## 🤝 기여하기

버그 리포트나 기능 제안은 언제든지 환영합니다.
