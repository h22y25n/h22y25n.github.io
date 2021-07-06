---
title: "BEM 문서 번역 - Quick Start"
categories:
  - CSS
tags:
  - CSS Methology, BEM
toc: true
toc_sticky: true
---

BEM을 익히기 위해 [BEM Methology](https://en.bem.info/methodology/) 사이트를 번역하며 학습/정리 한 내용!

BEM(Block, Element, Modifier)은 웹 개발에 대한 구성요소 기반 접근법입니다. 그 이면에 있는 아이디어는 사용자 인터페이스를 독립적인 블록으로 나누는 것입니다. 이를 통해 복잡한 UI로도 인터페이스를 쉽고 빠르게 개발할 수 있으며 복사 및 붙여넣기 없이 기존 코드를 재사용할 수 있습니다.

## Block

재사용할 수 있는, 기능적으로 독립적인 페이지의 컴포넌트입니다. HTML에서 블록은 `class` 속성으로 표시합니다.

### 특징

블록의 이름은 상태가 아니라 목적을 묘사합니다. (`menu` 또는 `button` / `red` 또는 `big` 과 같은 상태가 아님)

```html
<!-- Correct. The `error` block is semantically meaningful -->
<div class="error"></div>

<!-- Incorrect. It describes the appearance -->
<div class="red-text"></div>
```

- 블록의 외부 구조(margin)이나 포지셔닝 설정을 하지 않아 블록이 어디에 추가되어도 외부 환경에 영향을 주지 않아야합니다
- BEM을 사용할 때는 CSS tag나 `ID` 선택자를 사용할 수 없습니다

이를 통해 블록을 재사용하거나 다른 위치로 이동하는데 필요한 독립성을 확보합니다.

### 가이드라인

**중첩**

- 블록은 블록에 중첩될 수 있습니다
- 중첩 레벨은 원하는 만큼 깊어질 수 있습니다

예제:

```html
<!-- `header` block -->
<header class="header">
    <!-- `logo` 중첩 block -->
    <div class="logo"></div>

    <!-- `search-form` 중첩 block -->
    <form class="search-form"></form>
</header>
```

## Element

블록과 분리되어 사용할 수 없는 블록의 복합 부분입니다.

### 특징

- 엘리먼트 이름은 상태가 아닌 목적을 설명합니다
- 엘리먼트 전체 이름 구조는 `block-name__element-name` 입니다. 엘리먼트 이름은 블록 이름으로부터 더블 언더스코어로 구분합니다.

예제:

```html
<!-- `search-form` block -->
<form class="search-form">
    <!-- `input` element in the `search-form` block -->
    <input class="search-form__input">

    <!-- `button` element in the `search-form` block -->
    <button class="search-form__button">Search</button>
</form>
```

### 가이드라인

**중첩**

- 엘리먼트는 엘리먼트에 중첩될 수 있습니다.
- 원하는 만큼 중첩 레벨을 만들 수 있습니다.
- 엘리먼트는 항상 엘리먼트가 아닌 블록의 일부분입니다. 즉, 엘리먼트 이름에 하이라키를 적용할 수 없습니다.

예제:
```html
<!--
    Correct. The structure of the full element name follows the pattern:
    `block-name__element-name`
-->
<form class="search-form">
    <div class="search-form__content">
        <input class="search-form__input">

        <button class="search-form__button">Search</button>
    </div>
</form>

<!--
    Incorrect. The structure of the full element name doesn't follow the pattern:
    `block-name__element-name`
-->
<form class="search-form">
    <div class="search-form__content">
        <!-- Recommended: `search-form__input` or `search-form__content-input` -->
        <input class="search-form__content__input">

        <!-- Recommended: `search-form__button` or `search-form__content-button` -->
        <button class="search-form__content__button">Search</button>
    </div>
</form>
```

블록 이름은 네임스페이스를 정의하며, 엘리먼트가 블록에 종속될 수 있도록 합니다.

> 동일한 블록의 동일한 엘리먼트에는 동일한 이름이 있습니다. 예를 들어 모든 메뉴 블록의 메뉴 항목을 `menu__item` 이라고 합니다.

블록은 DOM트리에 있는 엘리먼트의 중첩 구조를 가질 수 있습니다:

예제:

```html
<div class="block">
    <div class="block__elem1">
        <div class="block__elem2">
            <div class="block__elem3"></div>
        </div>
    </div>
</div>
```

이 중첩된 블록 구조는 BEM 방법론을 통해 평면적인 리스트로 표시할 수 있습니다.

```css
.block {}
.block__elem1 {}
.block__elem2 {}
.block__elem3 {}
```

이렇게 하면 각 개별 엘리먼트의 코드를 변경하지 않고도 블록의 DOM 구조를 변경할 수 있습니다.

```html
<div class="block">
    <div class="block__elem1">
        <div class="block__elem2"></div>
    </div>

    <div class="block__elem3"></div>
</div>
```

블록 구조는 변경되지만 엘리먼트와 그 이름에 대한 규칙은 그대로 유지할 수 있습니다.

종속성

엘리먼트는 항상 블록의 일부이며, 블록에서 분리되어 사용할 수 없습니다.

예제:

```html
<!-- Correct. Elements are located inside the `search-form` block -->
<!-- `search-form` block -->
<form class="search-form">
    <!-- `input` element in the `search-form` block -->
    <input class="search-form__input">

    <!-- `button` element in the `search-form` block -->
    <button class="search-form__button">Search</button>
</form>

<!--
    Incorrect. Elements are located outside of the context of
    the `search-form` block
-->
<!-- `search-form` block -->
<form class="search-form">
</form>

<!-- `input` element in the `search-form` block -->
<input class="search-form__input">

<!-- `button` element in the `search-form` block-->
<button class="search-form__button">Search</button>
```

**옵셔널**

엘리먼트는 선택적으로 사용합니다. 모든 블록에 엘리먼트가 있는 것은 아닙니다.

예제:

```html
<!-- `search-form` block -->
<div class="search-form">
    <!-- `input` block -->
    <input class="input">

    <!-- `button` block -->
    <button class="button">Search</button>
</div>
```

## 블록을 만들까 엘리먼트를 만들까?

- Block
    - 코드가 재사용 되고 구현중인 다른 페이지 구성요소에 종속되지 않는경우

- Element
    - 부모 블록 없이 일부 코드를 별도로 분리해 사용할 수 없는 경우
    - 개발을 단순화하기 위해 더 작은 부분으로 구분해야 하는 엘리먼트는 예외입니다. BEM 방법론에서는 엘리먼트의 엘리먼트를 만들 수 없습니다. 이런 경우 엘리먼트를 생성하는 대신 서비스 블록을 생성해야합니다

## Modifier

블록 또는 엘리먼트의 모양, 상태 또는 동작을 정의하는 엔티티입니다.

### 특징

- 모디파이어의 이름은 외양과 상태, 동작을 나타냅니다 (`size_s`, `theme_island`, `disabled`, `focused`, `directions_left-top` ...)
- 모디파이어 이름은 블록이나 엘리먼트 이름으로부터 싱글 언더스코어로 구분합니다 (`_`)

### 종류

**Boolean**

- 모디파이어의 유무만 중요하고 모디파이어의 값은 무관할 때 사용합니다.(`disabvled`), 만약 부울린 모디파이어가 존재한다면, 해당 값은 `true` 로 간주됩니다
- 모디파이어의 전체 이름 구조는 아래 패턴을 따릅니다
    - `block-name_modifier-name`
    - `block-name__element-name_modifier-name`

예제:

```html
<!-- `search-form` 블록은 `focused` 부울린 모디파이어를 갖습니다 -->
<form class="search-form search-form_focused">
    <input class="search-form__input">

    <!-- `button` 엘리먼트는 `disabled` 부울린 모디파이어를 갖습니다 -->
    <button class="search-form__button search-form__button_disabled">Search</button>
</form>
```

**Key-value**

- 모디파이어 값이 중요한 경우 사용합니다. 예를 들어 `island` 디자인 테마를 갖는 메뉴의 경우 `menu_theme_islands` 와 같이 사용합니다
- 모디파이어의 전체 이름 구조는 아래 패턴을 따릅니다
    - `block-name_modifier-name_modifier-value`
    - `block-name__element-name_modifier-name_modifier-value`

예제:

```html
<!-- `search-form` 블록은 `theme` 모디파이어에 `islands`라는 값을 갖습니다 -->
<form class="search-form search-form_theme_islands">
    <input class="search-form__input">

    <!-- `button` 엘리먼트는 `size` 모디파이어에 `m` 이라는 값을 갖습니다 -->
    <button class="search-form__button search-form__button_size_m">Search</button>
</form>

<!-- 값이 다른 두개의 동일한 모디파이어를 동시에 사용할 수는 없습니다 -->
<form class="search-form
             search-form_theme_islands
             search-form_theme_lite">

    <input class="search-form__input">

    <button class="search-form__button
                   search-form__button_size_s
                   search-form__button_size_m">
        Search
    </button>
</form>
```

### 가이드라인

**모디파이어 혼자 사용될 수 없습니다**

BEM 관점에서 모디파이어는 수정된 블록 또는 엘리먼트에서 분리하여 사용할 수 없습니다. 모디파이어는 엔티티의 모양, 동작 또는 상태를 변경해야합니다.

예제:

```html
<!--
    Correct. `search-form` 블록은 `theme` 모디파이어에 `islands` 라는 값을 갖는다.
-->
<form class="search-form search-form_theme_islands">
    <input class="search-form__input">

    <button class="search-form__button">Search</button>
</form>

<!-- Incorrect. `search-form` 클래스가 없다. -->
<form class="search-form_theme_islands">
    <input class="search-form__input">

    <button class="search-form__button">Search</button>
</form>
```

## Mix

단일 DOM 노드에서 서로 다른 BEM 엔티티를 사용하는 기술입니다.

- 코드를 복제하지 않고 여러 엔티티의 동작과 스타일을 결합할 수 있습니다
- 기존 UI 콤포넌트를 바탕으로 의미론적인 새 UI 콤포넌트를 만들 수 있습니다

예제:

```html
<!-- `header` block -->
<div class="header">
    <!--
        `search-form` 블록은 `header` 블록의 `search-form` 엘리먼트와 믹스되었다
    -->
    <div class="search-form header__search-form"></div>
</div>
```

예를들어, `search-form` 블록과 `header` 블록의 `search-form` 엘리먼트의 동작과 스타일을 결합시킨다. 이러한 접근방식은 `search-form` 블록 자체는 범용적으로 사용하면서 `header__search-form` 엘리먼트에 외부 영역과 포지셔닝을 설정할 수 있습니다. 결과적으로 패딩 값을 특정하지 않기때문에 블록을 어느 환경에서든 사용할 수 있게됩니다. 우리는 이를 독립성 이라고 부릅니다.

## File Structure

BEM 방법론에 채택된 컴포넌트 접근 방식은 파일 구조의 프로젝트에도 적용됩니다. 블록, 엘리먼트, 모디파이어의 구현은 독립적인 기술 파일로 구분되고 각각을 개별적으로 연결할 수도 있습니다.

### 특징

- 단일 블록은 단일 디렉토리에 해당합니다
- 블록과 디렉토리는 이름이 동일하다. 예를들어 `header` 블록은 `header/` 디렉토리에 위치합니다
- 블록 구현(implementation)도 별도 기술 파일로 분리됩니다 (`header.css` 와 `header.js`)
- 블록의 디렉토리는 해당 블록의 엘리먼트와 모디파이어의 상위 디렉토리입니다
- 엘리먼트 디렉토리의 이름은 더블 언더스코어로 시작합니다. (`header/__logo`)
- 모디파이어 디렉토리의 이름은 싱글 언더스코어로 시작합니다. (`header_fixed` )
- 엘리먼트와 모디파이어의 구현은 별도 기술 파일로 분리됩니다. (`header__input.js`, `header_theme_island.css`)

예제:

```bash
search-form/                           # Directory of the search-form

    __input/                           # Subdirectory of the search-form__input
        search-form__input.css         # CSS implementation of the
                                       # search-form__input element
        search-form__input.js          # JavaScript implementation of the
                                       # search-form__input element

    __button/                          # Subdirectory of the search-form__button
                                       # element
        search-form__button.css
        search-form__button.js

    _theme/                            # Subdirectory of the search-form_theme
                                       # modifier
        search-form_theme_islands.css  # CSS implementation of the search-form block
                                       # that has the theme modifier with the value
                                       # islands
        search-form_theme_lite.css     # CSS implementation of the search-form block
                                       # that has the theme modifier with the value
                                       # lite

    search-form.css                    # CSS implementation of the search-form block
    search-form.js                     # JavaScript implementation of the
                                       # search-form block
```

이러한 파일 구조는 코드를 사용하기 쉽고 재사용성을 높여줍니다.
