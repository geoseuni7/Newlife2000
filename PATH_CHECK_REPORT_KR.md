# 경로 점검 보고서 — Render 전용 100파일판

- Cloudflare 배포 설정과 R2 업로드 구조를 사용하지 않습니다.
- Express 서버가 `/data/index.json`, `/data/universe.json`, `/data/bundles/part-XX.json`을 `market-data/`에서 제공합니다.
- 게임 클라이언트는 `index.json`의 `bundle_map`을 읽어 선택한 월의 데이터가 포함된 묶음 JSON을 요청합니다.
- 각 묶음에서 요청한 월 키의 배열만 읽으며, 클라이언트가 `asset_id` 중복 및 데이터 배열을 검사합니다.
- 로그인/저장/랭킹/멀티플레이 API는 `server.js`가 처리합니다. PostgreSQL과 `DATABASE_URL`, `JWT_SECRET` 환경변수가 필요합니다.
- 확인 결과: 총 파일 100개, 가격 묶음 JSON 60개, 인덱스/종목목록 JSON 2개, 앱·서버·이미지·설정 파일 38개.
- 월별 매핑 321개(2000-01~2026-09), 자산 16,013개, 가격 행 2,021,232개를 묶음 데이터에서 확인했습니다.
- `node --check server.js` 문법 검사를 통과했습니다.
- 실제 Render 원격 배포, PostgreSQL 연결, 브라우저에서의 완전한 UI/멀티플레이 테스트는 아직 수행하지 않았습니다.
