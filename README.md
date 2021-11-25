# KoZIP

Python library for converting Korean ZIP code to address

우편번호를 (도로명)주소로 변환해 주는 파이썬 라이브러리입니다. 현 우편번호(5자리), 구 우편번호(6자리) 모두 사용 가능합니다.

본 라이브러리는 [우체국 홈페이지](https://www.epost.go.kr/search/zipcode/cmzcd002k01.jsp)에 고지된 정보를 바탕으로 만들어졌습니다.

|      우편번호       |  고시일자   |                              다운로드 링크                               |
| :-----------------: | :---------: | :----------------------------------------------------------------------: |
| 현 우편번호 (5자리) | 2021.11.03. | [다운로드](https://www.epost.go.kr/search/zipcode/areacdAddressDown.jsp) |
| 구 우편번호 (6자리) | 2015.08.27. |  [다운로드](https://www.epost.go.kr/search/zipcode/newAddressDown.jsp)   |

## Quick Start

```python
from kozip import KoZip

kozip = KoZIP()

kozip.ZIPtoAddr("08826", depth="full")
# 출력 :
# ['서울특별시 관악구 관악로 1 (신림동)']

kozip.ZIPtoAddr("16419", depth="full")
# 출력 :
# ['경기도 수원시 장안구 서부로 2066 (천천동)',
#  '경기도 수원시 장안구 일월로90번길 19 (천천동)',
#  '경기도 수원시 장안구 일월로90번길 7 (천천동)']
```

## Environment

- Python 3 이상

## How to install

`pip install kozip`

## Methods

### KoZIP.ZIPtoAddr(zipcode, depth, format)

우편번호를 입력받아 주소로 변환하는 메소드

- `zipcode` : 우편번호
  - 현 우편번호(5자리), 구 우편번호(6자리) 모두 사용 가능
  - 문자열 형태(`str`)로 입력해도 되고, 숫자 형태(`int`)로 입력해도 된다(단, 0으로 시작하는 우편번호는 숫자 형식으로 입력할 수 없다).
  - 구 우편번호의 경우, "123-456", "123456" 형태로 모두 사용 가능

- `depth` : [Optional(default: `2`)] 출력될 주소의 깊이

    | depth |     사용 가능한 값     |                       설명                        |
    | :---: | :--------------------: | :-----------------------------------------------: |
    |   1   |  `1`, `"1"`, `"시도"`  |                시도 단위까지 출력                 |
    |   2   | `2`, `"2"`, `"시군구"` |           시군구 단위까지 출력. 기본값            |
    |   3   | `3`, `"3"`, `"도로명"` |               도로명 단위까지 출력                |
    |   4   |  `4`, `"4"`, `"full"`  | 도로명 단위에 추가 정보(읍면동, 리 정보)까지 출력 |

- `format` : [Optional(default: `"string"`)] 출력 형식

    | format | 사용 가능한 값 |                     설명                      |
    | :----: | :------------: | :-------------------------------------------: |
    | 문자열 |    "string"    |          문자열 형태로 출력. 기본값           |
    | 리스트 |     "list"     | (`depth` 값과 같은 길이의) 리스트 형태로 출력 |

<table>
<tbody>
<tr>
    <td></td>
    <td></td>
    <th colspan="2">format</th>
</tr>
<tr>
    <td></td>
    <td></td>
    <th>문자열</th>
    <th>리스트</th>
</tr>
<tr>
    <th rowspan="4">depth</th>
    <th>1</th>
    <td><code><pre>['경기도']</pre></code></td>
    <td><code><pre>[['경기도']]</pre></code></td>
</tr>
<tr>
    <th>2</th>
    <td><code><pre>['경기도 수원시 장안구']</pre></code></td>
    <td><code><pre>[['경기도', '수원시 장안구']]</pre></code></td>
</tr>
<tr>
    <th>3</th>
    <td><code><pre>['경기도 수원시 장안구 서부로 2066', 
 '경기도 수원시 장안구 일월로90번길 19', 
 '경기도 수원시 장안구 일월로90번길 7']</pre></code></td>
    <td><code><pre>[['경기도', '수원시 장안구', '서부로 2066'],
 ['경기도', '수원시 장안구', '일월로90번길 19'],
 ['경기도', '수원시 장안구', '일월로90번길 7']]</pre></code></td>
</tr>
<tr>
    <th>4</th>
    <td><code><pre>['경기도 수원시 장안구 서부로 2066 (천천동)',
 '경기도 수원시 장안구 일월로90번길 19 (천천동)',
 '경기도 수원시 장안구 일월로90번길 7 (천천동)']</pre></code></td>
    <td><code><pre>[['경기도', '수원시 장안구', '서부로 2066 (천천동)'],
 ['경기도', '수원시 장안구', '일월로90번길 19 (천천동)'],
 ['경기도', '수원시 장안구', '일월로90번길 7 (천천동)']]</pre></code></td>
</tr>
</tbody>
</table>

