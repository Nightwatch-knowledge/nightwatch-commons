# playbooks/ — AI 사용설명서 (CLAUDE.md)

> 이 저장소는 NightWatch 지식 커먼즈(공개 티어)다 — 시장구조 지식만 담는다. 게이트·교훈 심층·펀드 내부는 프로·내부 티어. 사람도 읽지만 1차 독자는 AI다.
> 구조: **raw(원자료) → wiki(이 폴더) → INDEX(목차) → 이 파일(사용법)**.
> 처음이면 이 파일 → [[INDEX]] → 해당 플레이북 README → gates 순서로 읽는다.

## 1. 이게 무엇인가

- **플레이북** = 한 시장(또는 한 엔진)에서 AI가 행동하는 데 필요한 지식의 완결 묶음. 폴더 하나 = 플레이북 하나.
- **파일 = 노드, `[[링크]]` = 엣지.** 이 폴더는 텍스트이면서 동시에 그래프다. Obsidian으로 열면 그래프 뷰가 나온다.
- **정본은 여기가 아니라 DB·원장이다.** 플레이북은 *검증된 구조 지식의 정리본*이고, 살아있는 값(시세·수수료·문 상태·잔고)은 각 README의 `live_endpoints`로 읽는다. 수치엔 반드시 `as_of`가 붙어 있다 — 날짜를 보고 신선도를 판단하라.

## 2. 폴더 규약

```
<playbook>/
  README.md      frontmatter(name·slug·version·epoch·tier·curators·coverage_grade·settlement_reality·live_endpoints·origin) + 읽는 순서
  facts/         검증된 사실. 인용·실측·출처. status: verified | unverified | curated
  rails/         (시장 플레이북) 입출금·API 접근 레일
  maps/          (레일 플레이북) 경로 맵 — 다이어그램 + 회랑 표 + 기계용 YAML
  atoms/<허브>/  원자 노트 — 1사실=1노트 (NN-slug.md). 허브 노드 끝 `## Atoms`에서 링크. 규약=[[ATOMIZATION_SPEC]]
  gates/         기계가 읽는 규칙. index.md + 게이트 파일들
  lessons/       what-generalises.md — 이 시장 밖에서도 통하는 교훈 (번호 목록)
  rooms/         open-questions.md — 열린 질문 = Hive 질문 노드 후보 = 기여 지점
  changelog.md   epoch 표기 변경 이력 (소급수정 금지)
```
펀드는 가족이다: `fund/README` → `fund/core`(엔진 무관) + `fund/<engine>/`. 엔진 플레이북은 `rails`·`hyperliquid` 게이트를 **상속**하고 복제하지 않는다.

## 3. Frontmatter 스키마

**노드(facts/rails/maps/lessons/rooms)**
```yaml
id: <playbook>.<kind>.<slug>     # 예: hl.facts.account-modes
title: ...
status: verified | unverified | curated | open
as_of: YYYY-MM-DD                # 사실 취득일. 없으면 신뢰하지 마라
freshness_note: ...              # (선택) 어떤 값이 빨리 낡는지
sources: [...]                   # 우리가 실제로 친 엔드포인트·문서·메모리. "기억"은 출처가 아니다
contributors: [house | <root sbt name>]
tags: [...]
tier_candidate: commons          # (선택) 공개 가능 후보
```
**게이트(gates/*)** — 행동 전에 로드하는 규칙. 이 다섯 필드는 기계가 읽는다.
```yaml
gate_id: <playbook>.gate.<slug>
severity: blocking | advisory
when: "언제 검사하는가"
check: "무엇을 확인하는가"
fail_action: "실패 시 무엇을 하는가"
source: "[[근거 노드]]"
as_of: YYYY-MM-DD
```

## 4. AI가 이 폴더를 쓰는 법

1. **행동 전 게이트 먼저.** 해당 플레이북 `gates/index.md`를 로드하고, 상속 게이트(fund→rails·hyperliquid)까지 포함해 `when`에 해당하는 것을 전부 검사한다. `blocking`은 통과 못 하면 행동하지 않는다.
2. **사실을 인용할 땐 노드 id와 as_of를 함께 말한다.** "hl.facts.account-modes(2026-07-31)에 따르면 …". `unverified`는 사실이 아니라 가설로 인용한다.
3. **숫자는 라이브로 다시 읽는다.** 플레이북의 수수료·시세는 스냅샷이다. `get_pair_gate`·`get_quartermaster`·`get_token_intel`·`nw_kg_facts`가 현재값이다.
4. **모르면 rooms에 있다.** 답이 없는 질문은 `rooms/open-questions.md`에 이미 열려 있을 가능성이 높다 — 거기 없으면 추가 후보다.
5. **교훈은 건너간다.** 어떤 시장에서 일하든 `lessons/what-generalises.md`는 전 플레이북 것을 읽어라. 다른 시장의 사고가 이 시장의 게이트다.

## 5. 기여하는 법 (쓰기)

- 새 사실 = 새 노드 파일 (또는 기존 노드에 날짜 붙은 항목 추가). **기존 숫자를 고치지 않는다** — 새 as_of 항목을 아래에 붙이고 changelog에 적는다.
- 노드는 **제출 → 검증 → 적재** 파이프를 탄다. 하우스 에이전트도 예외 없다. 검증 전 노드는 `status: unverified`.
- 게이트 추가는 근거 노드(`source`)가 먼저 있어야 한다. 사고 → 사실 노드 → 게이트 순서.
- 열린 질문을 닫으면 rooms에서 지우지 말고 "해소된 것" 절로 옮긴다.
- 형식: **바닐라 Markdown + `[[위키링크]]` + YAML frontmatter만.** Dataview·Canvas·플러그인 문법 금지 (Obsidian 밖에서 죽는다).
- **넣지 말 것**: 키·토큰·비밀번호·지갑 개인키·거래소 API 키·실잔고·개인 지갑 주소(공개 주소라도 운영 지갑은 Credentials Index로만 가리킨다).

## 8. 하지 말 것 (요약)

소급수정 · 지어낸 수치("부재를 측정으로 읽기") · 출처 없는 사실 · 게이트 우회 · 비밀값 · 플러그인 전용 문법 · 다른 플레이북 게이트 복제(링크로 상속).
