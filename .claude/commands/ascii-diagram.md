---
description: Draw an ASCII box-diagram in a code block without breaking alignment
---

사용자가 요청한 내용을 박스 그림(ASCII box-drawing diagram)으로 그려서 마크다운 코드 블록(```)에 넣어줘: $ARGUMENTS

## 왜 이 절차가 필요한가

한글은 대부분의 모노스페이스 폰트에서 영문자의 2배 폭(가변폭)을 차지함. `┌─┐│└┘` 같은 박스 문자와 한글이 같은 줄에 섞이면 열이 어긋나서 박스 테두리가 깨짐. 따라서:

- **박스 안(테두리 `┌┐└┘│`로 둘러싸인 영역)에는 영어, 숫자, 기호만 사용**하고 한글을 넣지 않는다.
- 한글 설명은 코드 블록 **밖**에 캡션(`>` 인용문이나 일반 문단)으로 작성한다.
- 화살표 연결선(`│`, `▼` 등 박스 사이 커넥터)은 박스가 아니므로 이 제약에서 자유롭지만, 일관성을 위해 가급적 영어/기호만 쓴다.

## 절차

1. 박스 안에 들어갈 내용을 영어로 구성한다 (예: 컨슈머 이름, 파티션 번호, 상태 등).
2. 각 박스마다 내용 중 가장 긴 줄을 기준으로 테두리 폭을 계산하고, 모든 줄을 그 폭에 맞춰 패딩한다. 손으로 세지 말고 아래 스크립트로 생성/검증한다.
3. 코드 블록을 작성한 뒤, 아래 검증 스크립트를 실행해서 모든 박스의 테두리와 내용 줄 길이가 일치하는지 확인한다. 어긋나면 반드시 수정한다.

## 박스 생성 스크립트 (참고용)

```python
def box(lines, pad=1, center_first=True):
    width = max(len(l) for l in lines) + pad * 2
    top = '┌' + '─' * width + '┐'
    bot = '└' + '─' * width + '┘'
    body = []
    for idx, l in enumerate(lines):
        total_pad = width - len(l)
        if idx == 0 and center_first:
            left = total_pad // 2
        else:
            left = pad
        right = total_pad - left
        body.append('│' + ' ' * left + l + ' ' * right + '│')
    return [top] + body + [bot]
```

## 검증 스크립트 (파일 작성 후 반드시 실행)

```bash
python3 -c "
import re
with open('<파일경로>', encoding='utf-8') as f:
    content = f.read()
blocks = re.findall(r'\`\`\`\n(.*?)\`\`\`', content, re.S)
bad = False
for i, b in enumerate(blocks):
    prev_border = None
    for l in b.split(chr(10)):
        s = l.strip()
        if s.startswith('┌') or s.startswith('└'):
            prev_border = len(l)
        elif s.startswith('│') and prev_border is not None:
            if len(l) != prev_border:
                print(f'Block {i} MISMATCH: border={prev_border} line_len={len(l)} -> {l!r}')
                bad = True
if not bad:
    print('All box content lines aligned with their borders.')
"
```

검증에서 MISMATCH가 나오면, 해당 박스만 다시 `box()` 함수로 폭을 재계산해서 고친다. 커넥터 줄(`│  │  │` 형태로 여러 박스 사이를 잇는 줄)은 박스 본문이 아니므로 이 검증에서 걸려도 무시해도 됨.
