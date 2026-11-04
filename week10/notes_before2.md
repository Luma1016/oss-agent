# tools.py 함수 정리 (2)

원본: `week09/tools.py`

## 모듈 개요

KOBIS(영화진흥위원회) 오픈 API에서 일별 박스오피스 정보를 가져오는 도구 모듈입니다.

- `requests`로 KOBIS `searchDailyBoxOfficeList` 엔드포인트를 호출합니다.
- `BASE_URL`에 API 주소가 상수로 정의되어 있습니다.
- `API_KEY`는 `secret` 모듈에서 가져오도록 작성되어 있습니다.

## 함수

### `get_boxoffice_rank_1(date)`

- **인자**: `date` — 조회할 날짜. KOBIS가 요구하는 `YYYYMMDD` 형식의 문자열입니다.
- **반환값**: 해당 날짜 박스오피스 1위 영화의 제목(`movieNm`) 문자열
- **동작**
  1. 쿼리 파라미터 `params`를 구성합니다. 인증 키(`API_KEY`)와 조회 날짜(`targetDt`)를 담습니다.
  2. `requests.get`으로 `BASE_URL`에 요청합니다. 타임아웃은 10초입니다.
  3. 응답 JSON에서 `boxOfficeResult` → `dailyBoxOfficeList` 목록을 꺼냅니다.
  4. 목록의 첫 번째 항목(1위)에서 `movieNm`을 꺼내 반환합니다.

## 확인이 필요한 부분

- **2행 `import secret import API_KEY`**: 문법 오류입니다. `from secret import API_KEY`로 고쳐야 합니다.
- **7행 파라미터 키 `"ket"`**: 오타입니다. KOBIS 인증 키 파라미터명은 `key`이므로 `"key"`로 고쳐야 합니다.
- **예외 처리 없음**: 응답에 `boxOfficeResult`가 없거나 목록이 비어 있으면 `KeyError` 또는 `IndexError`가 발생합니다. 호출하는 쪽에서 처리해야 합니다.
- **함수 이름 `rank_1`**: 1위만 반환한다는 뜻입니다. 전체 순위가 필요하면 목록 전체를 반환하도록 확장할 수 있습니다.
