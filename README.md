# 암호화폐 순위 대시보드 🪙

실시간 암호화폐 시장 정보를 한눈에 확인할 수 있는 대시보드 애플리케이션입니다.

![Next.js](https://img.shields.io/badge/Next.js-15.2.4-black?style=for-the-badge&logo=next.js)
![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4.17-06B6D4?style=for-the-badge&logo=tailwindcss)

## 📌 주요 기능

- 🏆 **실시간 순위** - 시가총액 기준 상위 암호화폐 순위 표시
- 💰 **가격 정보** - 현재 가격 및 24시간 변동률 실시간 표시
- 📊 **시장 데이터** - 시가총액, 거래량 등 핵심 지표 제공
- 🌙 **다크 모드** - 눈의 피로를 줄이는 다크 테마 기본 지원
- 📱 **반응형 디자인** - 모바일, 태블릿, 데스크톱 완벽 지원
- 🇰🇷 **한국어 UI** - 완전한 한국어 인터페이스

## 🚀 시작하기

### 필수 요구사항

- Node.js 18.17 이상
- pnpm 9.1.1 이상

### 설치 및 실행

```bash
# 저장소 클론
git clone https://github.com/grigrigo/golden-rabbit-yojeum-claude-code-crypto-ranking-board.git
cd golden-rabbit-yojeum-claude-code-crypto-ranking-board

# 의존성 설치
pnpm install

# 개발 서버 실행
pnpm dev
```

브라우저에서 [http://localhost:3000](http://localhost:3000)을 열어 확인하세요.

### 프로덕션 빌드

```bash
# 프로덕션 빌드
pnpm build

# 프로덕션 서버 실행
pnpm start
```

## 🛠️ 기술 스택

### 프레임워크
- **Next.js 15.2.4** - React 기반 풀스택 프레임워크
- **React 19** - 사용자 인터페이스 라이브러리
- **TypeScript 5** - 타입 안정성을 위한 정적 타입 언어

### 스타일링
- **Tailwind CSS 3.4.17** - 유틸리티 우선 CSS 프레임워크
- **shadcn/ui** - Radix UI 기반 커스터마이즈 가능한 컴포넌트
- **Lucide React** - 아이콘 라이브러리

## 📊 표시되는 암호화폐

현재 다음 8개 주요 암호화폐의 정보를 표시합니다:

1. 🟠 비트코인 (BTC)
2. 🔷 이더리움 (ETH)
3. 🟢 테더 (USDT)
4. 🟡 바이낸스 코인 (BNB)
5. 🟣 솔라나 (SOL)
6. ⚫ 리플 (XRP)
7. 🔵 USD 코인 (USDC)
8. 🔴 카르다노 (ADA)

## 📱 반응형 디자인

| 화면 크기 | 표시 컬럼 |
|-----------|-----------|
| 모바일 (<768px) | 순위, 이름, 가격, 24시간 변동률 |
| 태블릿 (768px-1024px) | + 시가총액 |
| 데스크톱 (>1024px) | + 거래량 (모든 정보) |

## 🏗️ 프로젝트 구조

```
├── app/                    # Next.js App Router
│   ├── page.tsx           # 홈 페이지
│   ├── layout.tsx         # 루트 레이아웃
│   └── globals.css        # 전역 스타일
├── components/
│   └── ui/                # shadcn/ui 컴포넌트
├── public/
│   └── coin/              # 암호화폐 로고 이미지
├── crypto-ranking-board.tsx  # 메인 대시보드 컴포넌트
└── lib/
    └── utils.ts           # 유틸리티 함수
```

## 🎨 UI 컴포넌트

이 프로젝트는 shadcn/ui 컴포넌트 라이브러리를 사용합니다:
- Card - 콘텐츠 컨테이너
- Badge - 상태 표시 (가격 변동률)
- 그 외 49개의 사용 가능한 컴포넌트

## 🔧 개발 도구

```bash
# 코드 린팅
pnpm lint

# 타입 체크 (현재 빌드 시 비활성화됨)
pnpm tsc --noEmit
```

## 📝 향후 계획

- [ ] 실시간 API 연동 (CoinAPI 또는 기타)
- [ ] 60초 자동 새로고침 구현
- [ ] 검색 및 필터 기능
- [ ] 상세 정보 페이지
- [ ] 차트 시각화
- [ ] 라이트 모드 토글
- [ ] 다국어 지원
- [ ] PWA 지원

## ⚠️ 알려진 이슈

- 현재 모의 데이터 사용 중 (실시간 데이터 아님)
- ESLint 및 TypeScript 오류가 빌드 시 무시됨
- Jest 테스트 설정 수정 필요 (`@unrs/resolver` 의존성 문제)

## 🤝 기여하기

프로젝트 개선에 기여하고 싶으시다면:

1. 이 저장소를 포크하세요
2. 새로운 브랜치를 생성하세요 (`git checkout -b feature/AmazingFeature`)
3. 변경사항을 커밋하세요 (`git commit -m 'Add some AmazingFeature'`)
4. 브랜치에 푸시하세요 (`git push origin feature/AmazingFeature`)
5. Pull Request를 생성하세요

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 있습니다.

## 📞 문의

프로젝트에 대한 문의사항은 [이슈](https://github.com/grigrigo/golden-rabbit-yojeum-claude-code-crypto-ranking-board/issues)를 통해 남겨주세요.

---

Made with ❤️ using Next.js and React