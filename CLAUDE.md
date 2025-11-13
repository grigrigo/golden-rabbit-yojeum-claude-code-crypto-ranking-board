# CLAUDE.md

이 파일은 이 저장소의 코드 작업 시 Claude Code (claude.ai/code)에 대한 가이드를 제공합니다.

## 프로젝트 개요

실시간 암호화폐 시장 데이터를 표시하는 암호화폐 순위 대시보드입니다. Next.js 15.2.4, React 19, TypeScript, Tailwind CSS로 구축되었습니다. 현재는 한국어 UI로 8개 주요 암호화폐의 모의 데이터를 표시합니다.

## 개발 명령어

```bash
# 의존성 설치 (pnpm 필요 - v9.1.1)
pnpm install

# 개발
pnpm dev          # localhost:3000에서 개발 서버 시작

# 프로덕션
pnpm build        # 프로덕션 빌드 생성
pnpm start        # 프로덕션 서버 실행

# 코드 품질
pnpm lint         # ESLint 실행

# 테스팅 (Jest 설정되어 있으나 테스트는 아직 없음)
npm test          # 테스트가 있다면 실행됨
```

## 아키텍처 및 컴포넌트 계층구조

### 특이한 프로젝트 구조
**중요**: 메인 컴포넌트 `crypto-ranking-board.tsx`가 app 디렉토리가 아닌 **프로젝트 루트**에 위치합니다. 이는 의도적이지만 Next.js 프로젝트에서는 일반적이지 않은 구조입니다.

### 컴포넌트 플로우
```
app/layout.tsx (한국어 메타데이터, 다크 테마)
  └── app/page.tsx (최소한의 래퍼)
      └── ../crypto-ranking-board.tsx (메인 컴포넌트 - 루트 레벨)
          ├── Card, CardHeader, CardContent (shadcn/ui)
          ├── Badge (색상 코딩된 가격 변화)
          └── TrendingUp/TrendingDown 아이콘 (lucide-react)
```

### 데이터 아키텍처
앱은 `crypto-ranking-board.tsx:16-97`에 직접 정의된 **하드코딩된 모의 데이터**를 사용합니다. `CoinData` 인터페이스에 필요한 항목:
- `rank`, `name` (한국어), `symbol`, `price`, `change24h`, `marketCap`, `volume`, `logo`

**API 라우트나 데이터 페칭**은 현재 존재하지 않습니다. 푸터에 "Powered by CoinAPI"와 "60초 업데이트"가 언급되지만 구현되지 않았습니다.

### 반응형 브레이크포인트
- **모바일 (<768px)**: 순위, 이름, 가격, 24시간 변동률만 표시
- **태블릿 (768px-1024px)**: 시가총액 컬럼 추가
- **데스크톱 (>1024px)**: 거래량 포함 모든 컬럼 표시

숨겨진 컬럼은 Tailwind 클래스 사용:
- 시가총액: `hidden md:table-cell`
- 거래량: `hidden lg:table-cell`

## 중요한 설정 문제

### 빌드 오류 억제됨 (next.config.mjs)
```javascript
eslint: { ignoreDuringBuilds: true }      // ESLint 오류 무시됨
typescript: { ignoreBuildErrors: true }   // TypeScript 오류 무시됨
images: { unoptimized: true }            // 이미지 최적화 비활성화됨
```
**경고**: 타입 오류나 린팅 문제가 있어도 프로덕션 빌드가 성공합니다.

### 테스팅 설정 고장
Jest가 설정되어 있지만 (`jest.config.mjs`) 설치되지 않은 `@unrs/resolver`를 임포트합니다. 테스트 실행이 즉시 실패합니다.

## 주요 구현 패턴

### 숫자 포맷팅 (crypto-ranking-board.tsx:99-120)
- `formatNumber()`: T/B/M/K 접미사와 $ 접두사로 변환
- `formatPrice()`: ≥$1 가격은 로케일 포맷팅 사용, <$1은 소수점 4자리

### 스타일링 접근법
- 다크 테마만 (라이트 모드 토글 없음)
- `app/globals.css`에 CSS 변수 정의됨
- 컴포넌트 스타일링에 Tailwind 유틸리티 사용
- 교대로 나타나는 행 배경: `index % 2 === 0 ? "bg-gray-900/20" : "bg-gray-900/40"`

### UI 컴포넌트 라이브러리
`components/ui/`에 49개의 shadcn/ui 컴포넌트가 있지만 3개만 사용됨:
- Card (Header, Title, Content 포함)
- Badge
- lucide-react의 아이콘

## 일반적인 개발 작업

### 새로운 암호화폐 추가
1. `public/coin/[name].png`에 로고 추가
2. `crypto-ranking-board.tsx:16-97`의 `mockCoinData` 배열에 추가
3. 로고 경로가 정확히 일치하는지 확인 (대소문자 구분)

### 실제 데이터 구현
1. `app/api/coins/route.ts`에 API 라우트 생성
2. `mockCoinData`를 fetch 호출로 교체
3. 로딩/에러 상태 추가 (현재 없음)
4. 필요시 60초 폴링 구현

### 빌드 설정 수정
적절한 오류 체크를 활성화하려면:
```javascript
// next.config.mjs
const nextConfig = {
  eslint: { ignoreDuringBuilds: false },
  typescript: { ignoreBuildErrors: false },
  // 필요시 이미지 최적화 비활성화 유지
}
```

### 한국어 로컬라이제이션
- 페이지 제목: "암호화폐 순위 - 실시간 가격 정보"
- 테이블 헤더는 한국어 용어 사용
- 코인 이름이 한국어 (비트코인, 이더리움 등)
- 숫자 포맷팅은 기본 로케일 사용 (아마도 en-US)

## 프로젝트 의존성 컨텍스트

### 핵심 스택
- App Router가 포함된 Next.js 15.2.4
- React 19 (최신)
- strict mode가 활성화된 TypeScript 5
- Tailwind CSS 3.4.17

### 무거운 의존성
- 27개 @radix-ui 패키지 (Card와 Badge만 사용됨)
- recharts 2.15.0 (사용되지 않음)
- react-hook-form 7.54.1 (사용되지 않음)
- 많은 shadcn/ui 컴포넌트가 임포트되었지만 사용되지 않음

### 경로 별칭
`@/`가 프로젝트 루트로 매핑됨 (tsconfig.json:paths)