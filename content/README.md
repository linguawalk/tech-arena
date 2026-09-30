# tech-arena 레슨 스키마 v1.0

math-arena·sci-arena와 같은 스키마·플레이어를 쓴다. 차이점만 적는다.

## 구조
- 레벨1 코스: c1 전기전자, c2 기계, c3 화학공학, c4 컴퓨터 (코스 0 없음)
- 경로: content/level1/{c1~c4}/ch{NN}/l{NN}.json, chapter.json, review.json / 코스 목록 content/level1/courses.json
- 과학 원리는 다시 설명하지 않고 sci-arena 해당 과목을 선수로 안내한다 (courses.json의 prereq)

## 추가 위젯: circuit (정적 회로도)
- figure: {"widget": "circuit", "static": true, "config": {"elements": [...], "dots": [[x,y]], "texts": [[x,y,"글자"]], "alt": "설명"}}
- elements[i]: {"t": 종류, "a": [x,y], "b": [x,y], "label": "R1", "side": "b"(라벨을 반대쪽에), "style": "zigzag"(미국식 저항), "open": false(닫힌 스위치)}
- 종류: wire, cell, battery, source(교류), resistor, lamp, switch, ammeter, voltmeter, fuse, diode, led, capacitor, ground
- 좌표는 격자 단위, y는 아래로 증가. 전지는 a 쪽이 (+)극, 다이오드는 a → b 방향으로 전류가 흐른다
- 빌더 도우미: tools/c1common.py (circ, P, W, left_cell)

## 빌드
- python3 tools/build_c1_ch01.py content && python3 tools/make_course_index.py content
- 단계 A 엄격 검사: 레슨당 문항 15~17개, 화면 20~24개, 예제 3개, 채점형 풀이 20자 이상, 적용·복습 문항 힌트 필수
