# Sketch Flow

[![Claude Code 지원](https://img.shields.io/badge/Claude_Code-D97757?style=flat-square)](#claude-code)
[![Codex 지원](https://img.shields.io/badge/Codex-14532D?style=flat-square)](#codex)
[![출력 형식 HTML + SVG](https://img.shields.io/badge/HTML_%2B_SVG-1864AB?style=flat-square)](assets/flow-template.html)

**시스템 구성과 처리 흐름을 손그림 스타일의 HTML로 그립니다.**

Claude Code와 Codex에서 함께 쓰는 스킬입니다. Rough.js + SVG로 그림을 만들며, 별도 빌드 없이 브라우저에서 결과를 확인하고 HTML을 수정할 수 있습니다.

[예시 보기](#예시) · [설치](#설치) · [사용법](#사용) · [파일 구성](#파일-구성) · [실행 환경](#실행-환경) · [외부 라이선스](#외부-라이선스)

| 표현 | 역할 |
| --- | --- |
| 한글 손글씨 · 빗금 채움 | 흰 바탕에 손으로 그린 듯한 질감 |
| 원통형 저장소 · 직각 화살표 | 데이터가 저장되는 곳과 처리 순서 구분 |
| 색상별 경로 · 흰색 라벨 외곽선 | 흐름을 구별하고 선 위의 글자를 읽기 쉽게 표시 |

<a id="예시"></a>

## 🎨 예시

[![손그림 스타일 주문 처리 흐름도: 주문 API, 작업 큐, 처리 워커, 저장소와 실패 재시도 경로](assets/flow-preview.png)](assets/flow-preview.png)

이미지를 클릭하면 크게 볼 수 있습니다. 직접 수정하려면 [HTML 예제·템플릿](assets/flow-template.html)을 내려받아 여세요.

<a id="설치"></a>

## 📦 설치

<a id="claude-code"></a>

### 🛠️ ![Claude 로고](https://img.shields.io/badge/-D97757?style=flat-square&logo=claude&logoColor=white) Claude Code

**개인 설치** · 모든 프로젝트에서 사용합니다.

```sh
git clone https://github.com/UjiinEatingTangerines/sketch-flow-skill.git ~/.claude/skills/sketch-flow
```

**프로젝트 설치** · 특정 프로젝트에서만 쓰려면 프로젝트 루트에서 실행하세요. 개인 설치와 프로젝트 설치 중 하나를 선택하면 됩니다.

```sh
git clone https://github.com/UjiinEatingTangerines/sketch-flow-skill.git .claude/skills/sketch-flow
```

<a id="codex"></a>

### 🛠️ ![OpenAI 로고](assets/codex-badge.svg) Codex

```sh
git clone https://github.com/UjiinEatingTangerines/sketch-flow-skill.git ~/.codex/skills/sketch-flow
```

`CODEX_HOME`을 따로 지정했다면 그 경로의 `skills/sketch-flow`에 설치하세요. 설치 후 새 세션에서 스킬을 불러옵니다.

> [!TIP]
> 이미 설치했다면 해당 스킬 저장소에서 `git pull --ff-only`로 업데이트하세요. 직접 수정한 파일이 있다면 변경 사항을 먼저 확인하세요.

<a id="사용"></a>

## ✍️ 사용

### 💬 Claude Code에서 요청하기

```text
/sketch-flow 주문 API → 작업 큐 → 워커 → 저장소 흐름을 그려주세요.
실패 재시도는 빨간 점선으로, 외부 시스템은 경계로 구분해주세요.
결과는 docs/order-flow.html에 저장해주세요.
```

### 💬 Codex에서 요청하기

```text
$sketch-flow로 주문 API → 작업 큐 → 워커 → 저장소 흐름을 그려주세요.
실패 재시도는 빨간 점선으로, 외부 시스템은 경계로 구분해주세요.
결과는 docs/order-flow.html에 저장해주세요.
```

Claude Code의 설치 위치와 `/sketch-flow` 호출 방식은 [공식 Skills 문서](https://code.claude.com/docs/en/skills)를 따릅니다.

<a id="파일-구성"></a>

## 🗂️ 파일 구성

| 파일 | 용도 |
| --- | --- |
| [SKILL.md](SKILL.md) | 두 도구가 함께 읽는 지침. 표준 `name`·`description` 필드만 사용합니다. |
| [flow-template.html](assets/flow-template.html) | 브라우저에서 열고 수정하는 예제 겸 템플릿 |
| [flow-preview.png](assets/flow-preview.png) | README에 표시하는 예제 이미지 |
| [openai.yaml](agents/openai.yaml) | Codex용 표시 메타데이터. Claude Code에서는 필요하지 않습니다. |

<a id="실행-환경"></a>

## ⚙️ 실행 환경

별도 MCP 서버나 특정 브라우저 플러그인은 필요하지 않습니다. 에이전트가 파일을 읽고 쓰는 기능으로 HTML을 만듭니다. 브라우저 도구가 있으면 렌더링까지 검증하고, 없으면 완성된 파일을 직접 열어 확인하도록 안내합니다.

> [!NOTE]
> 예제는 가상의 주문 처리 흐름입니다. Rough.js 4.6.6 CDN과 Google Fonts를 불러오므로 인터넷 연결이 필요합니다. 오프라인으로 배포하려면 라이브러리와 글꼴을 별도로 포함하세요. 자동 캡처 시에도 글꼴 로딩을 기다려야 합니다.

<a id="외부-라이선스"></a>

## 📄 외부 라이선스

HTML 템플릿에서 불러오는 라이브러리와 글꼴의 라이선스입니다. 배지를 클릭하면 원문을 확인할 수 있습니다.

| 구성요소 | 용도 | 라이선스 |
| --- | --- | --- |
| [Rough.js](https://github.com/rough-stuff/rough) | 손그림 스타일 SVG 렌더링 | [![Rough.js 라이선스: MIT](https://img.shields.io/badge/MIT-1864AB?style=flat-square)](https://github.com/rough-stuff/rough/blob/master/LICENSE) |
| [Gaegu](https://fonts.google.com/specimen/Gaegu) | 한글 손글씨 글꼴 | [![Gaegu 라이선스: SIL OFL 1.1](https://img.shields.io/badge/SIL_OFL_1.1-1864AB?style=flat-square)](https://github.com/google/fonts/blob/main/ofl/gaegu/OFL.txt) |

두 구성요소는 CDN과 Google Fonts에서 불러오며, 해당 라이브러리·글꼴 파일은 저장소에 포함하지 않습니다. 위 표는 외부 구성요소에 적용되는 라이선스를 안내합니다.
