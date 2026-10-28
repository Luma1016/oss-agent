# week09 - 일별 박스오피스 1위 영화 조회

## 무엇을 하는 코드인지

KOBIS(영화진흥위원회) 오픈 API의 `searchDailyBoxOfficeList`를 호출해서, 지정한 날짜의 일별 박스오피스 순위 중 **1위 영화 제목**을 반환합니다.

- `tools.py` / `tools_nodoc.py`: `get_boxoffice_rank_1(date)` 함수가 들어 있습니다. `date`는 `YYYYMMDD` 형식의 문자열입니다.
- `main.py`: `tools` 모듈을 불러와 함수의 docstring을 출력하는 예제입니다.

## 무엇을 설치해야 하는지

- Python 3
- 필요한 패키지: `requests` (나머지 항목은 `requests`의 의존 패키지)

```bash
pip install -r requirements.txt
```

- KOBIS 오픈 API 인증키가 필요합니다. [KOBIS 오픈 API](https://www.kobis.or.kr/kobisopenapi/)에서 발급받을 수 있습니다.
- 발급받은 키를 `week09/secret.py` 파일에 다음과 같이 저장합니다. (이 파일은 저장소에 올리지 마세요.)

```python
API_KEY = "발급받은_인증키"
```

## 어떻게 실행하는지

```bash
cd week09
python main.py
```

직접 함수를 호출하려면 다음과 같이 사용합니다.

```python
from tools import get_boxoffice_rank_1

print(get_boxoffice_rank_1("20260101"))  # 해당 날짜 1위 영화 제목
```
