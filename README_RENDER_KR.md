# Retro Stock Game — Render 배포판 (총 100개 파일)

## 배포 방식
- Render Node.js Web Service + PostgreSQL 데이터베이스 사용
- Cloudflare Pages/Workers/R2 전용 파일과 설정은 포함하지 않음
- 가격 데이터는 `market-data/part-01.json`~`part-60.json`으로 묶어 제공
- `market-data/index.json`의 `bundle_map`이 각 월(2000-01~2026-09)을 데이터 묶음에 연결
- `market-data/universe.json`에 종목 목록 포함

## Render 배포 설정
1. ZIP을 풀고 프로젝트 폴더를 Render가 접근할 수 있는 저장소/배포 방식으로 업로드합니다.
2. Render에서 New → Web Service를 선택합니다.
3. Runtime: Node
4. Build Command: `npm install`
5. Start Command: `npm start`
6. 환경변수: `NODE_ENV=production`, `JWT_SECRET`에 길고 무작위인 비밀값, `DATABASE_URL`에 PostgreSQL 연결 문자열, `TRUST_PROXY=1`
7. 배포 후 `/api/health`에서 DB 연결을 확인합니다.

## 파일 수 및 데이터
- 전체 파일 수: 정확히 100개 (디렉터리는 파일 수에 포함하지 않음)
- 가격 데이터: 60개 JSON 묶음
- 인덱스 및 종목 목록: JSON 2개
- 월별 범위: 2000-01~2026-09, 총 321개월
- 게임은 선택한 월을 인덱스에서 찾고 해당 묶음 파일에서 그 월의 가격 배열을 읽습니다.

## 중요
- 실제 Render 원격 배포 및 실제 DB 로그인/멀티플레이 테스트는 이 패키지 생성만으로 완료된 것이 아닙니다.
- 데이터 재분배와 클라이언트/서버 경로 연결은 로컬에서 검사해야 하며, 배포 후 `/data/index.json`, `/data/universe.json`, `/data/bundles/part-01.json`을 열어 확인하세요.
- `DATABASE_URL` 및 `JWT_SECRET`은 채팅이나 공개 저장소에 올리지 마세요.
