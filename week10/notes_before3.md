작성: Claude Code / 확인: 이병주

# tools.py 함수 정리 (3)

원본: `week09/tools.py`

## 모듈 개요

- KOBIS(영화진흥위원회) 오픈 API에서 일별 박스오피스 정보를 가져오는 도구 모듈임.
- `requests`로 KOBIS `searchDailyBoxOfficeList` 엔드포인트를 호출함.
- `BASE_URL` 상수에 API 주소가 정의되어 있음.
- `API_KEY`를 `secret` 모듈에서 가져오도록 작성되어 있음.
- 함수는 `get_boxoffice_rank_1` 하나뿐임.

## 함수

### `get_boxoffice_rank_1(date)`

- 인자: `date`, 조회할 날짜. KOBIS 요구 형식인 `YYYYMMDD` 문자열임.
- 반환값: 해당 날짜 박스오피스 1위 영화 제목(`movieNm`) 문자열임.
- 동작 순서
  1. `params` 딕셔너리를 구성함. 인증 키(`API_KEY`)와 조회 날짜(`targetDt`)를 담음.
  2. `requests.get`으로 `BASE_URL`에 요청함. 타임아웃은 10초임.
  3. 응답 JSON에서 `boxOfficeResult` → `dailyBoxOfficeList` 목록을 꺼냄.
  4. 목록 첫 번째 항목(1위)의 `movieNm`을 반환함.

## 확인이 필요한 부분

- 1행 `import requests`는 정상임.
- 2행 `import secret import API_KEY`는 문법 오류임. `from secret import API_KEY`로 고쳐야 함.
- 7행 파라미터 키 `"ket"`는 오타임. KOBIS 인증 키 파라미터명은 `key`이므로 `"key"`로 고쳐야 함.
- 예외 처리가 없음. 응답에 `boxOfficeResult`가 없으면 `KeyError`, 목록이 비어 있으면 `IndexError`가 발생함. 호출하는 쪽에서 처리가 필요함.
- 함수명 `rank_1`은 1위만 반환한다는 뜻임. 전체 순위가 필요하면 목록 전체를 반환하도록 확장할 수 있음.
- `tools.py`는 수정하지 않음(CLAUDE.md 규칙). 위 오류는 문서에만 기록함.

## 평가

함수가 하나뿐인 짧은 모듈이라 동작 흐름은 단순하나, 2행 문법 오류와 7행 파라미터 오타 때문에 현재 상태로는 실행되지 않음.
