# Sketch Flow

Claude Code와 Codex에서 Rough.js + SVG로 손그림 느낌의 시스템 구성도와 처리 흐름도를 만드는 공용 스킬입니다.

흰 바탕에 한글 손글씨, 빗금 채움, 원통형 저장소, 직각 화살표, 색상별 경로와 흰색 라벨 외곽선을 사용합니다. 별도 빌드 없이 HTML로 결과를 확인하고 수정할 수 있습니다.

## 예시

[![손그림 스타일 주문 처리 흐름도: 주문 API, 작업 큐, 처리 워커, 저장소와 실패 재시도 경로](assets/flow-preview.png)](assets/flow-preview.png)

이미지를 클릭하면 크게 볼 수 있습니다. [HTML 예제·템플릿](assets/flow-template.html)을 내려받아 직접 열고 수정할 수 있습니다.

## 설치

### Claude Code

모든 프로젝트에서 사용하려면 개인 스킬 경로에 설치합니다.

```sh
git clone https://github.com/UjiinEatingTangerines/sketch-flow-skill.git ~/.claude/skills/sketch-flow
```

특정 프로젝트에서만 사용하려면 해당 프로젝트 루트에서 다음 명령을 실행합니다. 두 방식 중 하나를 선택하세요.

```sh
git clone https://github.com/UjiinEatingTangerines/sketch-flow-skill.git .claude/skills/sketch-flow
```

### Codex

```sh
git clone https://github.com/UjiinEatingTangerines/sketch-flow-skill.git ~/.codex/skills/sketch-flow
```

`CODEX_HOME`을 따로 지정했다면 그 경로의 `skills/sketch-flow`에 설치하세요. 설치 후 새 세션에서 스킬을 불러옵니다.

설치 경로가 이미 있으면 다시 복제하지 말고 해당 스킬 저장소에서 `git pull --ff-only`로 업데이트하세요. 직접 수정한 파일이 있다면 변경 사항을 먼저 확인하세요.

## 사용

Claude Code:

```text
/sketch-flow 주문 API → 작업 큐 → 워커 → 저장소 흐름을 그려주세요.
실패 재시도는 빨간 점선으로, 외부 시스템은 경계로 구분해주세요.
결과는 docs/order-flow.html에 저장해주세요.
```

Codex:

```text
$sketch-flow로 주문 API → 작업 큐 → 워커 → 저장소 흐름을 그려주세요.
실패 재시도는 빨간 점선으로, 외부 시스템은 경계로 구분해주세요.
결과는 docs/order-flow.html에 저장해주세요.
```

Claude Code의 설치 위치와 `/sketch-flow` 호출 방식은 [공식 Skills 문서](https://code.claude.com/docs/en/skills)를 따릅니다.

## 구성과 요구사항

- `SKILL.md`: 두 도구에서 사용하는 공통 지침. 표준 `name`·`description` 필드만 사용합니다.
- `assets/flow-template.html`: 그대로 열거나 수정할 수 있는 예제 겸 템플릿.
- `assets/flow-preview.png`: README 미리보기.
- `agents/openai.yaml`: Codex용 표시 메타데이터. Claude Code 사용에는 필요하지 않습니다.

별도 MCP 서버나 특정 브라우저 플러그인을 설치할 필요는 없습니다. 에이전트의 파일 읽기·쓰기 기능으로 HTML을 만들며, 브라우저 도구가 있으면 실제 렌더링도 검증합니다. 없으면 파일을 직접 열어 확인하도록 안내합니다.

- [스킬 지침](SKILL.md)
- [실행 가능한 HTML 예제·템플릿](assets/flow-template.html): 내려받아 브라우저에서 여세요.

예제는 가상의 주문 처리 흐름입니다. Rough.js 4.6.6 CDN과 Google Fonts를 사용하므로 인터넷 연결이 필요합니다. 오프라인 배포는 의존성을 별도로 포함해야 합니다. 자동 캡처 시에도 글꼴 로딩을 기다리세요.

Rough.js는 MIT, Gaegu는 SIL Open Font License로 배포되는 외부 의존성입니다. 이 저장소에는 해당 라이브러리·글꼴 파일을 포함하지 않습니다.
