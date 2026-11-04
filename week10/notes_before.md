# tools.py 함수 정리

원본: `week09/tools.py`

## 모듈 개요

KOBIS(영화진흥위원회) 오픈 API에서 일별 박스오피스 정보를 가져오는 도구 모듈입니다.

- `requests`로 KOBIS `searchDailyBoxOfficeList` 엔드포인트를 호출합니다.
- `BASE_URL`에 API 주소가 상수로 정의되어 있습니다.
- `API_KEY`는 `secret` 모듈에서 가져옵니다.

## 함수

### `get_boxoffice_rank_1(date)`

- **인자**: `date` — 조회할 날짜 (KOBIS 형식 `YYYYMMDD` 문자열로 보입니다)
- **반환값**: 해당 날짜 박스오피스 1위 영화의 제목(`movieNm`) 문자열
- **동작**
  1. `key`(API 키)와 `targetDt`(날짜)를 쿼리 파라미터로 구성합니다.
  2. `requests.get`으로 `BASE_URL`에 요청합니다 (타임아웃 10초).
  3. 응답 JSON에서 `boxOfficeResult.dailyBoxOfficeList` 목록을 꺼냅니다.
  4. 첫 번째 항목(1위)의 `movieNm`을 반환합니다.

## 확인이 필요한 부분

- **1행 `import requests`** 이후 2행이 `import secret import API_KEY`로 되어 있어 문법 오류입니다. 올바른 형태는 `from secret import API_KEY`로 보입니다.
- **6~7행**: 파라미터 키가 `"ket"`으로 오타입니다. KOBIS API 명세상 인증 키 파라미터는 `key`이므로 `"key"`로 고쳐야 할 것으로 보입니다.
- 응답에 `boxOfficeResult`가 없거나 목록이 비어 있으면 `KeyError` / `IndexError`가 발생합니다. 현재 예외 처리는 없습니다.
- 함수 이름의 `rank_1`은 1위만 반환한다는 뜻으로 보이며, 전체 순위가 필요하면 목록을 반환하도록 확장할 수 있습니다.
