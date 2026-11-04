# audrbsdl.github.io 운영 가이드

GitHub Pages + Jekyll + [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) 테마로 만든 개인 블로그입니다.
이 문서는 블로그를 **직접 고칠 때** 어디를 어떻게 바꾸면 되는지 정리한 것입니다.

> 이 README는 `_config.yml`의 `exclude`에 들어 있어서 블로그 화면에는 나오지 않고, GitHub 저장소에서만 보입니다.

---

## 목차

1. [폴더 구조 한눈에 보기](#1-폴더-구조-한눈에-보기)
2. [내 컴퓨터에서 미리 보기](#2-내-컴퓨터에서-미리-보기)
3. [글 쓰기](#3-글-쓰기)
4. [사이트 정보·메뉴·소개 페이지](#4-사이트-정보메뉴소개-페이지)
5. [디자인 바꾸기](#5-디자인-바꾸기)
6. [라이트/다크 전환 기능](#6-라이트다크-전환-기능)
7. [파비콘 바꾸기](#7-파비콘-바꾸기)
8. [블로그에 반영하기](#8-블로그에-반영하기)
9. [자주 겪는 문제](#9-자주-겪는-문제)

---

## 1. 폴더 구조 한눈에 보기

| 경로 | 하는 일 | 자주 고치나요? |
|---|---|---|
| `_posts/` | 블로그 글 (`YYYY-MM-DD-제목.md`) | ⭐ 매번 |
| `_config.yml` | 블로그 이름·소개·작성자·전역 설정 | 가끔 |
| `_data/navigation.yml` | 상단 메뉴 항목 | 가끔 |
| `_pages/` | 소개·카테고리·태그·전체 글·404 페이지 | 가끔 |
| `index.html` | 홈 화면 (상단 소개 박스 + 글 목록) | 드물게 |
| `assets/css/main.scss` | **다크** 테마 색 | 디자인 바꿀 때 |
| `assets/css/main-light.scss` | **라이트** 테마 색 | 디자인 바꿀 때 |
| `_sass/custom/_shared.scss` | 두 테마 공통 글꼴·크기·폭·둥글기 | 디자인 바꿀 때 |
| `_sass/custom/_overrides.scss` | 두 테마 공통 세부 스타일 (메뉴, 본문, 버튼…) | 디자인 바꿀 때 |
| `_includes/head/custom.html` | 글꼴 불러오기, 파비콘, 테마 전환 초기화 | 드물게 |
| `_includes/footer/custom.html` | 상단 메뉴의 테마 전환 버튼 | 드물게 |
| `assets/images/` | 이미지 (파비콘은 `assets/images/favicon/`) | 글에 이미지 넣을 때 |
| `favicon.ico` | 브라우저가 기본으로 찾는 파비콘 | 드물게 |
| `Gemfile` | **내 컴퓨터에서 실행할 때만** 쓰는 Ruby 패키지 목록 | 거의 안 함 |

테마 원본 파일은 이 저장소에 없습니다. `_config.yml`의 `remote_theme: mmistakes/minimal-mistakes`로 빌드할 때 받아옵니다.
테마가 원래 어떻게 생겼는지 보고 싶으면 [테마 저장소](https://github.com/mmistakes/minimal-mistakes)에서 `_sass/`, `_includes/`, `_layouts/`를 찾아보세요.

---

## 2. 내 컴퓨터에서 미리 보기

Windows + Ruby 3.3 기준입니다.

```powershell
cd C:\workspace\audrbsdl.github.io
bundle install                # 처음 한 번, 또는 Gemfile을 바꾼 뒤
bundle exec jekyll serve      # http://localhost:4000 에서 확인
```

- 글이나 CSS를 고치면 저장할 때마다 **자동으로 다시 빌드**됩니다. 브라우저만 새로고침하세요.
- **`_config.yml`을 고쳤다면 서버를 껐다가(Ctrl+C) 다시 켜야** 반영됩니다.
- 작성 중인 글까지 보려면 `bundle exec jekyll serve --drafts` (→ [3-4](#3-4-임시-글-초안)).
- `_site/` 폴더는 빌드 결과물입니다. 직접 고치지 말고, 커밋하지도 않습니다 (`.gitignore`에 들어 있음).

---

## 3. 글 쓰기

### 3-1. 새 글 만들기

`_posts/` 안에 `YYYY-MM-DD-영문-제목.md` 파일을 만듭니다. 예: `_posts/2026-11-10-python-generator.md`

```yaml
---
title: "파이썬 제너레이터 제대로 이해하기"
excerpt: "글 목록에 보일 한 줄 요약"
categories:
  - Python
tags:
  - 제너레이터
  - yield
---

여기부터 본문을 마크다운으로 씁니다.
```

- **파일 이름은 영문·숫자·하이픈**으로 쓰는 걸 권합니다. 파일 이름이 글 주소(URL)가 됩니다.
- 날짜가 미래이면 그날이 되기 전까지 블로그에 나오지 않습니다.
- 목차, 읽는 시간, 작성자 사이드바는 `_config.yml`의 `defaults`가 **모든 글에 자동으로** 붙여 줍니다. 특정 글에서만 끄고 싶으면 그 글의 머리말에 `toc: false`처럼 적으세요.

### 3-2. 카테고리와 태그

- **카테고리**는 큰 주제(한 글에 보통 1개), **태그**는 세부 키워드(여러 개)입니다.
- 카테고리는 홈 상단 소개 박스와 `/categories/` 페이지에 **글 수와 함께 자동으로** 모입니다. 따로 등록할 필요가 없습니다.
- ⚠️ 글 주소가 `/:categories/:title/` 형식이라 **카테고리 이름이 URL에 들어갑니다.** 이미 올린 글의 카테고리를 바꾸면 주소도 바뀌어 기존 링크가 깨집니다. 카테고리 이름은 처음에 신중히 정하세요.
- 같은 주제는 **철자를 똑같이** 써야 한 카테고리로 묶입니다 (`Python` ≠ `python`).

### 3-3. 이미지 넣기

이미지는 `assets/images/posts/` 아래에 두는 걸 권합니다.

```markdown
![설명 문장](/assets/images/posts/2026-11-10-diagram.png)
```

### 3-4. 임시 글 (초안)

저장소 맨 위에 `_drafts/` 폴더를 만들고 **날짜 없이** `제목.md`로 저장하면, 블로그에는 올라가지 않고 `--drafts` 옵션으로 실행할 때만 보입니다. 다 쓰면 `_posts/`로 옮기면서 파일 이름 앞에 날짜를 붙이세요.

### 3-5. 자주 쓰는 마크다운

````markdown
## 소제목 (목차에 들어감)

`인라인 코드`

```python
print("코드 블록 — 언어 이름을 적으면 색이 입혀집니다")
```

> 인용문

**알림 박스** — 문단 바로 아래 줄에 붙여 씁니다.
{: .notice--info}
````

알림 박스 종류: `.notice`, `.notice--primary`, `.notice--info`, `.notice--warning`, `.notice--success`, `.notice--danger`

---

## 4. 사이트 정보·메뉴·소개 페이지

### 4-1. `_config.yml`에서 자주 바꾸는 값

| 항목 | 지금 값 | 어디에 보이나요 |
|---|---|---|
| `title` | `audrbsdl.log` | 상단 왼쪽 타이틀 (`~/` 뒤), 브라우저 탭 |
| `subtitle` | `배우고, 만들고, 기록합니다` | 타이틀 아래 작은 글씨, 홈 소개 박스 제목 |
| `description` | 개인 기술 블로그 소개 문장 | 홈 소개 박스 설명, 검색 엔진 |
| `author.name` / `author.bio` | `audrbsdl` / 한 줄 소개 | 왼쪽 작성자 사이드바 |
| `author.avatar` | (주석 처리됨) | 사이드바 프로필 사진 — 이미지를 `assets/images/`에 넣고 주석을 푸세요 |
| `author.links`, `footer.links` | GitHub, RSS | 사이드바·푸터 링크 |
| `paginate` | `8` | 홈 한 페이지에 보이는 글 수 |

> 상단 타이틀 앞의 `~/`는 설정값이 아니라 CSS로 붙인 장식입니다 (`_overrides.scss`의 `.greedy-nav .site-title::before`).

**고친 뒤에는 `jekyll serve`를 다시 시작하세요.**

### 4-2. 상단 메뉴 — `_data/navigation.yml`

```yaml
main:
  - title: "글"
    url: /posts/
  - title: "새 메뉴"        # 추가 예시
    url: /projects/
```

순서대로 표시되고, 화면이 좁으면 넘치는 항목은 자동으로 `≡` 버튼 안으로 들어갑니다.

### 4-3. 소개·기타 페이지 — `_pages/`

- 소개 페이지: `_pages/about.md` 본문을 고치면 됩니다.
- 새 페이지를 만들려면 `_pages/`에 파일을 만들고 머리말에 `permalink: /주소/`를 적은 뒤, 위 메뉴에 연결하세요.

---

## 5. 디자인 바꾸기

### 5-1. 원리 — 이것만 알면 됩니다

```
assets/css/main.scss        (다크)     assets/css/main-light.scss  (라이트)
  ├─ 색 변수 선언                         ├─ 색 변수 선언
  ├─ @import custom/shared  ← 공통 글꼴·크기
  ├─ @import 테마 스킨 + 테마 본체          ← 테마가 내 변수 값으로 만들어짐
  └─ @import custom/overrides ← 공통 세부 스타일 (변수만 사용)
```

- **색은 테마 파일 두 개에만** 있고, `_overrides.scss`는 `$primary-color` 같은 **변수 이름으로만** 색을 씁니다. 그래서 세부 스타일을 한 번만 써도 라이트·다크에 각각 맞는 색이 들어갑니다.
- 변수는 반드시 **`@import`보다 위에** 선언해야 적용됩니다 (테마 값이 `!default`라서 먼저 선언한 값이 이깁니다).
- 새 세부 스타일을 넣을 때 `#5eead4` 같은 **색 코드를 직접 쓰지 마세요.** 한쪽 테마에서만 어울리게 됩니다. 필요한 색이 없으면 두 테마 파일에 같은 이름의 변수를 하나씩 만들어 쓰세요.

### 5-2. 색 바꾸기

`main.scss`(다크)와 `main-light.scss`(라이트)에서 **같은 변수를 둘 다** 고칩니다.

| 변수 | 역할 | 다크 | 라이트 |
|---|---|---|---|
| `$primary-color` | 포인트 색 (`~/`, 버튼, 강조) | `#5eead4` | `#0d9488` |
| `$link-color` / `$link-color-hover` | 링크 / 링크에 마우스 올렸을 때 | `#5eead4` / `#99f6e4` | `#0d9488` / `#0f766e` |
| `$background-color` | 배경 | `#0f1216` | `#ffffff` |
| `$text-color` | 본문 글자 | `#d5d9e0` | `#2b3038` |
| `$heading-color` | 제목 글자 | `#f1f3f6` | `#111418` |
| `$muted-text` | 날짜·설명 등 흐린 글자 | `#8b94a3` | `#6b7280` |
| `$border-color` | 테두리·구분선 | `#232a33` | `#e5e7eb` |
| `$code-background-color` | 코드·인용 배경 | `#161b22` | `#f6f8fa` |
| `$inline-code-color` | `인라인 코드` 글자 | `#f0a8d0` | `#c0367a` |
| `$base00` ~ `$base0f` | 코드 블록 문법 색 (base16 규칙) | GitHub Dark 계열 | GitHub Light 계열 |

> 포인트 색을 바꿀 때는 라이트 쪽을 **조금 더 진하게** 잡아야 흰 배경에서 글자가 잘 읽힙니다.
> 다크 배경색을 바꿨다면 `_includes/head/custom.html` 안의 `#0f1216`(모바일 브라우저 상단 색, 2곳)도 같이 바꾸세요.

### 5-3. 글꼴·글자 크기·폭 — `_sass/custom/_shared.scss`

| 변수 | 지금 값 | 설명 |
|---|---|---|
| `$sans-serif` | Pretendard … | 본문·제목 글꼴 |
| `$monospace` | JetBrains Mono … | 코드, 타이틀, 날짜 글꼴 |
| `$doc-font-size` | `15px` | 기본 글자 크기 (큰 화면에서는 테마가 자동으로 키움) |
| `$border-radius` | `8px` | 카드·버튼 모서리 둥글기 |
| `$max-width` | `1200px` | 전체 화면 최대 폭 |

**글꼴을 바꾸려면 두 곳을 고칩니다.**
1. `_includes/head/custom.html` 맨 위의 글꼴 `<link>` (웹폰트 불러오기)
2. `_shared.scss`의 `$sans-serif` 또는 `$monospace` (맨 앞에 새 글꼴 이름)

### 5-4. 세부 스타일 — `_sass/custom/_overrides.scss`

섹션별로 나뉘어 있으니 주석 제목으로 찾아가세요.

| 섹션 | 담당 |
|---|---|
| 전역 | 한글 줄바꿈, 드래그 선택 색, 링크 밑줄 |
| 상단 메뉴 | 고정 메뉴, 반투명 배경, `~/` 타이틀, 부제 |
| 사이드바 (작성자) | 이름·소개 |
| 본문 | 줄 간격, 제목, 링크, 인용, 표, 인라인 코드, 코드 블록, 목차, 태그 버튼, 알림, 버튼 |
| 글 목록 (홈·아카이브) | 글 카드, 카테고리·태그 목록 버튼, 페이지 번호 |
| 홈 상단 소개 | `$ whoami` 박스 (`.home-hero`), 카테고리 바로가기 (`.home-cats`) |
| 푸터 | 하단 영역 |
| 테마 전환 버튼 | 해/달 버튼 |

**테마의 기존 스타일이 내 스타일을 이길 때**: 테마 원본의 선택자가 더 구체적인 경우입니다. 실제로 `.site-title`은 테마의 `.greedy-nav a { display: block }`에 밀려서 `.greedy-nav .site-title`로 써야 했습니다. 브라우저 개발자 도구(F12)에서 해당 요소를 찍어 보고, 줄이 그어진 규칙이 있으면 그보다 구체적인 선택자로 쓰세요.

### 5-5. 홈 화면 소개 박스 — `index.html`

`$ whoami` 문구, 제목(`site.subtitle`), 설명(`site.description`), 카테고리 바로가기가 들어 있습니다. 문구만 바꾸려면 **`_config.yml`의 `subtitle`·`description`**을 고치는 게 가장 간단합니다.

---

## 6. 라이트/다크 전환 기능

**동작**
- 처음 방문하면 기기 설정(시스템 다크/라이트 모드)을 따릅니다.
- 상단 메뉴의 해/달 버튼을 누르면 바뀌고, 고른 테마는 그 브라우저에 기억됩니다 (`localStorage`의 `theme` 값).
- 다크는 `main.css`, 라이트는 `main-light.css`라는 **완전히 별개의 CSS 파일**이고, 스크립트가 둘 중 하나만 켭니다.

**관련 파일**
- `_includes/head/custom.html`: 첫 화면의 테마를 정하고 CSS를 켜고 끄는 스크립트
- `_includes/footer/custom.html`: 버튼을 만들어 상단 메뉴에 끼워 넣는 스크립트

⚠️ **이 스크립트는 되도록 건드리지 마세요.** 라이트 모드에서 CSS 없는 화면이 잠깐 보이던 문제를 막으려고 실행 순서를 정밀하게 맞춰 두었습니다.
- `window.__theme` 정의가 `document.write`보다 **위에** 있어야 합니다.
- 스크립트가 다크 CSS를 `/assets/css/main.css` 경로로 찾습니다. CSS 파일 이름을 바꾸면 이 부분도 같이 바꿔야 합니다.

**라이트/다크 중 하나만 쓰고 싶다면**: `_includes/footer/custom.html`을 비우면 버튼이 사라집니다. 이 경우에도 기기 설정은 계속 따라가므로, 다크로 고정하려면 `head/custom.html` 스크립트의 `var initial = …` 줄을 `var initial = 'dark';`로 바꾸세요.

---

## 7. 파비콘 바꾸기

| 파일 | 용도 |
|---|---|
| `assets/images/favicon/favicon.svg` | 원본 (최신 브라우저). **이것부터 고치세요** |
| `favicon.ico` (저장소 맨 위) | 16·32·48px 묶음. 브라우저가 기본으로 찾는 주소 |
| `assets/images/favicon/favicon-32.png`, `favicon-192.png` | PNG만 지원하는 환경, 안드로이드 |
| `assets/images/favicon/apple-touch-icon.png` (180px) | 아이폰 홈 화면 추가. iOS가 모서리를 깎으므로 **꽉 찬 사각형** |

- SVG는 텍스트 파일이라 메모장으로 열어 색(`#5eead4`, `#0f1216`)만 바꿀 수도 있습니다. 바꾼 뒤에는 PNG·ICO도 다시 만들어야 모든 브라우저에서 같게 보입니다 (온라인 "SVG to ICO" 변환기를 써도 됩니다).
- 파일 이름을 바꾸면 `_includes/head/custom.html`의 파비콘 `<link>` 줄도 고치세요.
- 브라우저가 예전 파비콘을 오래 기억합니다. 안 바뀌면 **Ctrl+F5** 또는 시크릿 창으로 확인하세요.

---

## 8. 블로그에 반영하기

```powershell
git add .
git commit -m "무엇을 바꿨는지 한 줄로"
git push
```

- `master` 브랜치에 푸시하면 GitHub Pages가 **자동으로 빌드해서 1~2분 안에** https://audrbsdl.github.io 에 반영합니다.
- 반영이 안 되면 GitHub 저장소의 **Actions** 탭에서 `pages build and deployment`가 성공했는지 확인하세요. 실패했다면 그 항목을 눌러 오류 메시지를 보면 어느 파일이 문제인지 나옵니다.
- 큰 변경은 먼저 `bundle exec jekyll serve`로 **로컬에서 확인한 뒤** 푸시하는 습관을 들이세요. 푸시하는 순간 실제 블로그가 바뀝니다.

---

## 9. 자주 겪는 문제

**`_config.yml`을 고쳤는데 안 바뀌어요**
→ `jekyll serve`를 껐다가 다시 켜세요. `_config.yml`만은 자동 반영이 안 됩니다.

**로컬에선 되는데 실제 블로그에선 안 돼요**
→ GitHub Pages는 저장소의 `Gemfile`을 **읽지 않고**, 자체 [`github-pages` gem](https://pages.github.com/versions/)과 허용된 플러그인만 씁니다. 새 플러그인을 `Gemfile`에 추가해도 허용 목록에 없으면 실제 블로그에서는 동작하지 않습니다.

**`Gemfile`은 언제 고치나요?**
→ 내 컴퓨터에서 실행이 안 될 때만입니다. 지금 내용(`github-pages ~> 232`, Ruby 3.3용 `webrick`·`csv` 등)은 로컬 실행용입니다. 배포 결과에는 영향이 없습니다.

**CSS 문법 오류로 빌드가 깨졌어요**
→ `jekyll serve` 터미널에 `Conversion error: ... _overrides.scss line 123` 같은 메시지가 나옵니다. 해당 줄의 괄호 `{ }`나 세미콜론 `;`을 확인하세요. `assets/css/main*.scss` 맨 위의 `---` 두 줄은 **지우면 안 됩니다** (Jekyll이 CSS로 변환하라는 표시입니다).

**`git status`에 안 고친 파일이 전부 수정됨으로 떠요**
→ Windows 줄바꿈(CRLF) 설정 차이입니다. 내용이 바뀐 게 아니니 `git config core.autocrlf true` 상태로 쓰면 됩니다.

**카테고리를 바꿨더니 예전 글 링크가 깨졌어요**
→ 글 주소에 카테고리가 들어가기 때문입니다 ([3-2](#3-2-카테고리와-태그)). 그 글의 머리말에 `permalink: /예전/주소/`를 적으면 예전 주소를 유지할 수 있습니다.

---

### 참고 문서

- [Minimal Mistakes 설정 문서](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) · [글 머리말 옵션](https://mmistakes.github.io/minimal-mistakes/docs/layouts/) · [유틸리티 클래스(알림 박스 등)](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/)
- [Jekyll 공식 문서](https://jekyllrb.com/docs/) · [GitHub Pages와 Jekyll](https://docs.github.com/ko/pages/setting-up-a-github-pages-site-with-jekyll)
