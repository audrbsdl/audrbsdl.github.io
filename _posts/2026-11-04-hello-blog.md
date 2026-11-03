---
title: "블로그를 시작합니다"
excerpt: "이 블로그를 어떻게 운영할지, 글은 어떻게 쓰는지 정리한 첫 글"
categories:
  - 블로그
tags:
  - 시작
  - jekyll
---

배우고 만든 것들을 주제별로 기록하려고 블로그를 열었습니다.

## 글 쓰는 방법

`_posts` 폴더에 `YYYY-MM-DD-제목.md` 형식으로 파일을 만들고, 맨 위에 이렇게 적으면 됩니다.

```yaml
---
title: "글 제목"
excerpt: "목록에 보일 한 줄 요약"
categories:
  - 카테고리이름
tags:
  - 태그1
  - 태그2
---
```

카테고리는 홈 상단과 [카테고리 페이지](/categories/)에 자동으로 모입니다.

## 코드 예시

```python
def hello(name: str) -> str:
    return f"안녕하세요, {name}님"

print(hello("audrbsdl"))
```

> 이 글은 예시라서 언제든 지워도 됩니다.
