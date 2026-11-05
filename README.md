# Reviewed Feature Guide 1.0.0

기능을 설계하고 교차 검토한 뒤, 사용자가 요청할 때마다 개발 단위 하나씩 따라 할 내용을 안내하는 스킬입니다. **별도의 구현 요청 전에는 실제 소스·애셋·설정을 변경하지 않습니다.**

Windows·macOS·Linux에서 읽을 수 있는 UTF-8 문서 패키지입니다. 스킬 자체에는 실행 파일, 셸 스크립트, 설치 프로그램, 훅, MCP 서버, API 키 요구가 없습니다. 자동 호출·서브에이전트·로컬 파일 접근은 사용하는 앱의 기능과 권한에 따릅니다.

## 가장 간단한 설치

1. ZIP을 풉니다.
2. 안쪽의 **`skills/reviewed-feature-guide` 폴더 전체**를 아래 중 사용하는 앱의 스킬 폴더 한 곳에 복사합니다. `SKILL.md`만 복사하지 말고 `references`, `agents`, `LICENSE`도 함께 복사합니다.
3. 앱의 스킬 목록에서 `reviewed-feature-guide`를 확인합니다. 반영되지 않으면 해당 앱의 새 대화·스킬 다시 읽기 절차를 따릅니다.

| 환경 | 개인용: 모든 프로젝트에서 사용 | 프로젝트 공유용 |
| --- | --- | --- |
| Codex | `~/.agents/skills/reviewed-feature-guide/` | `.agents/skills/reviewed-feature-guide/` |
| Claude Code | `~/.claude/skills/reviewed-feature-guide/` | `.claude/skills/reviewed-feature-guide/` |
| Gemini CLI | `~/.gemini/skills/reviewed-feature-guide/` 또는 `~/.agents/skills/reviewed-feature-guide/` | `.gemini/skills/reviewed-feature-guide/` 또는 `.agents/skills/reviewed-feature-guide/` |
| 다른 Agent Skills 지원 앱 | 그 앱이 문서화한 개인 스킬 경로 | 그 앱이 문서화한 프로젝트 스킬 경로 |

`~`는 각 사용자의 홈 폴더입니다. Windows에서는 사용자 프로필 폴더 아래에 해당 디렉터리를 만들면 됩니다. 프로젝트 경로는 대상 저장소 기준입니다. 설치 위치 근거: [Codex](https://learn.chatgpt.com/docs/build-skills), [Claude Code](https://code.claude.com/docs/en/skills), [Gemini CLI](https://geminicli.com/docs/cli/skills/).

기존 Codex 환경에서 `~/.codex/skills` 등 다른 경로의 설치본이 이미 인식된다면 그 설치본을 갱신하세요. 같은 이름의 스킬을 여러 경로에 중복 설치하지 마세요. 개인용 설치가 웹·클라우드 세션에 자동 전파된다는 뜻은 아닙니다. 원격 환경에는 별도로 배포해야 합니다.

## 호출 예

Codex에서 스킬 호출을 지원하는 경우:

```text
$reviewed-feature-guide 인벤토리 장착 기능을 설계하고 검토해줘.
직접 구현하지 말고, 내가 다음 단계를 요청할 때 한 단위씩 설명해줘.
```

Claude Code에 일반 스킬로 설치했다면 `/reviewed-feature-guide`로 시작할 수 있습니다. 다른 앱에서는 스킬을 선택하거나 이름을 포함한 자연어 요청을 사용하세요. 호출 문법은 공통 표준이 아닙니다.

Claude Code 플러그인으로 설치했다면 `/reviewed-feature-guide:reviewed-feature-guide`로 호출합니다.

이후에는 다음처럼 요청합니다.

```text
다음 단계
```

이는 한 단계의 **설명 요청**입니다. 직접 구현을 원하면 `이번 단계만 구현해줘`처럼 범위를 지정합니다. 자동 목표 알림이나 시간 경과로 다음 단계를 진행하지 않습니다.

## 플러그인과 검토자 지원 차이

원본 검토는 **Superpowers 설계 → Ponytail Ultra 검토 → 설계 수정·재검토 → mattpocock 최종 검증**입니다. 같은 최신 설계 버전에서 필수 지적이 해소될 때까지 반복합니다.

연동할 때 실제로 읽을 외부 지침은 다음과 같습니다. 제공자별 배포 방식으로 별도 설치하며, 이 ZIP이 자동 설치하거나 복제해 포함하지 않습니다.

| 제공자 | 사용하는 지침 |
| --- | --- |
| [Superpowers](https://github.com/obra/superpowers) | `brainstorming`, `writing-plans` |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | `ponytail`의 Ultra 수준 |
| [mattpocock skills](https://github.com/mattpocock/skills) | `codebase-design` |

| 환경의 기능 | 가능한 진행 |
| --- | --- |
| 지정 스킬과 서브에이전트 사용 가능 | 원본 검토 |
| 지정 스킬이 없고 분리된 검토자 사용 가능 | 사용자 선택 후 자체 기본 기준으로 대체 독립 검토 |
| 자동 서브에이전트 없음 | 사용자 선택 후 새 대화나 별도 검토자에게 자료를 수동 전달 |
| 독립 검토 수단 없음 | 사용자가 독립 검토 없이 진행하기를 선택하면 단독 점검과 제한된 안내 |

대체 검토는 실제 외부 플러그인 검토가 아니며, 단독 점검은 독립 검토가 아닙니다. 결과에 수행한 방식과 미실행 검토가 표시됩니다. 사용자가 선택한 대체 방식은 같은 과제에서 반복 확인하지 않습니다. 원본 검토를 원한다면 필요한 기능을 갖춘 환경에서 진행하면 됩니다.

대체 방식을 바로 지정하는 예:

```text
reviewed-feature-guide의 대체 독립 검토로 진행해줘.
이 환경에 없는 플러그인을 실행했다고 표시하지 말고, 구현은 하지 마.
```

파일·스킬 설치 기능이 없는 대화 환경에서는 [SKILL.md](skills/reviewed-feature-guide/SKILL.md)와 [대체·수동 검토 안내](skills/reviewed-feature-guide/references/portable-review.md)를 함께 제공하고 적용을 요청합니다. 필요한 소스 자료도 사용자가 제공해야 합니다. 이 경우 자동 스킬 등록이나 로컬 저장소 접근이 생기는 것은 아닙니다. 수동 인계 양식은 두 번째 문서에 있습니다.

## 플러그인 패키지로 배포

일반 스킬 폴더 복사 대신 플러그인을 배포하려면 **압축을 푼 루트 전체**를 사용합니다.

- `plugin.json`: Agent Plugins 1.0.0 형식의 기본 진입점. 스킬은 `skills/` 아래에 있습니다.
- `.codex-plugin/plugin.json`: Codex 호환 형식을 사용하는 호스트용 메타데이터.
- `.claude-plugin/plugin.json`: Claude Code 플러그인용 메타데이터.

실제 등록은 해당 호스트가 제공하는 로컬 플러그인·마켓플레이스 절차를 따릅니다. 이 ZIP은 이미 게시된 마켓플레이스 항목이 아닙니다. 공개 저장소 주소나 게시자 정보가 정해지지 않아 가짜 주소·연락처를 넣지 않았습니다. 웹·모바일 배포는 호스트의 게시 및 권한 절차가 별도로 필요합니다. 형식 근거: [OpenAI 플러그인 패키징](https://developers.openai.com/plugins/build/plugins), [Claude 플러그인 manifest](https://code.claude.com/docs/en/plugins-reference).

```text
reviewed-feature-guide-1.0.0/
  README.md
  LICENSE
  SHA256SUMS
  plugin.json
  .codex-plugin/plugin.json
  .claude-plugin/plugin.json
  skills/reviewed-feature-guide/
    SKILL.md
    LICENSE
    agents/openai.yaml
    references/portable-review.md
```

스킬 본문은 [Agent Skills 표준](https://agentskills.io/specification)의 메타데이터와 Markdown을 사용합니다. `agents/openai.yaml`을 지원하지 않는 앱은 이 표시 정보를 사용하지 않아도 본문과 참조 문서를 읽을 수 있습니다.

## 공유·갱신·확인

- 공유할 파일은 버전 ZIP과 옆의 `.sha256` 파일입니다. 수신자는 ZIP의 SHA-256을 비교할 수 있습니다. ZIP 내부 `SHA256SUMS`는 자기 자신을 제외한 배포 파일 목록과 해시입니다.
- 갱신할 때 기존 설치본을 먼저 보관하고, 같은 이름의 폴더를 새 스킬 폴더로 교체하세요. 참조 문서까지 함께 갱신합니다. 앱의 같은 이름 스킬이 하나만 활성화되도록 확인하세요.
- 다른 프로젝트의 지침·대화·검토 기록은 배포물에 넣지 않습니다. 새 환경에서는 요구·현재 소스·단계 진행 상태를 새로 확인합니다.
- 첫 사용에서는 사용할 검토 방식과 실제 읽을 수 있는 자료를 먼저 확인하고, 설계가 준비된 뒤 `다음 단계`가 한 단위 설명만 제공하는지 확인하세요.

이 배포물은 MIT 라이선스로 공유·수정할 수 있습니다. [LICENSE](LICENSE)를 함께 유지하세요. 스킬 폴더를 단독 복사할 때도 그 안의 LICENSE가 따라갑니다. 외부 플러그인은 각 제공자의 라이선스와 배포 정책을 따릅니다.

## 검증 범위

배포 기준일: 2026-11-05. Windows 작업 환경에서 스킬 형식, 공개 Agent Plugins JSON Schema, 버전·라이선스 일치, UTF-8, 상대 링크의 존재·대소문자·범위, 배포 파일 목록, 개인 경로 제외를 검사했습니다. ZIP의 10개 파일, CRC, 내부 SHA-256 목록과 원본 일치를 확인했고 한글·공백이 있는 다른 경로에 추출한 사본도 같은 검사를 통과했습니다.

독립 모의 사용 5가지에서 파일 접근 없음, 검토 버전 불일치, 수동 새 대화 인계, 단독 점검 뒤 자동 알림, 다른 스킬 접두사·도구 이름을 확인했습니다. 이 결과는 실제 타 호스트 통합 실행과 구분합니다.

모든 운영체제와 앱에서 실제 설치·동작을 보증하는 패키지는 아닙니다. 원본 기능의 빌드·게임 실행, 타 호스트의 실설치·마켓플레이스 심사, 웹·모바일 등록은 이 배포 작업의 검증 범위 밖입니다.
