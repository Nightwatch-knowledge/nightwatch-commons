# 원자화 규약 (Atomization Spec) — 1사실 = 1노트

> 목적: 압축 노트(한 파일에 사실 10~25개)를 **원자 노트**로 분해해 그래프가 지식 구조를 드러내게 한다.
> 원자 = 외부 Obsidian 사용자가 보는 지식의 최소 단위이자, 기여자 지분·출처가 붙는 단위.

## 절대 규칙
1. **지어내지 않는다.** 원자의 모든 문장은 허브 노트(기존 facts/rails/maps 파일)에 있는 문장·숫자·인용에서만 온다. 요약·해석·추론 추가 금지. 숫자는 한 자리도 바꾸지 않는다.
2. **허브 노트는 삭제·이동하지 않는다.** 기존 링크가 깨진다. 허브 파일 끝에 `## Atoms` 절을 추가해 원자들로 링크만 건다.
3. **원자 하나 = 검증 가능한 주장 하나** (+ 그 근거·출처). "A이고 B이다"는 두 원자.
4. **원자에 `unverified`가 붙은 주장은 `status: unverified`** 로 그대로 승계.
5. 비밀값(키·잔고·개인 지갑 주소) 금지 — 허브에 없으면 원자에도 없다.

## 위치와 이름
```
<playbook>/atoms/<허브slug>/NN-<영문-slug>.md      NN = 01부터, 허브 안 등장 순서
```
예: `hyperliquid/atoms/account-modes/03-unified-account-shares-margin.md`

## 원자 파일 형식
```markdown
---
id: <playbook>.atom.<허브slug>.NN
title: <한 문장 주장 — 한국어, 40자 내외>
status: verified | unverified
as_of: <허브의 as_of 또는 해당 항목의 실측일>
hub: "[[../../facts/<허브slug>]]"            # 상대경로. rails/maps면 그 경로
source: "<허브의 sources 중 이 주장의 근거 1개, 또는 인용 원문>"
tags: [<허브 tags 중 관련 것 1~3개>]
contributors: [house]
---

# <title과 동일>

<주장 1~3문장 — 허브 원문 그대로 또는 최소 편집. 인용은 > 블록 유지.>

**근거**: <실측값·인용·표 행 — 원문 그대로>

관련: [[<이 사실을 쓰는 게이트 파일 상대경로>]] · [[<원자료 파일명>]] · [[<메모리 파일명>]]
```

## 링크 규칙 (그래프 밀도의 핵심)
- **게이트로**: 허브의 `source`에 이 허브가 적힌 게이트, 또는 허브 본문에서 `→ [[../gates/...]]`로 가리킨 게이트 → 원자의 `관련:`에 상대경로로.
- **원자료로**: 허브 `sources`/`origin`에 적힌 문서를 **파일명만으로** 링크 (`[[HL_FACT_MAP]]`, `[[PATH_INTELLIGENCE]]`, `[[2026-09-07-multix-round-l]]`). playbooks 단독 vault에선 미해결 링크(숨김), wiki vault에선 해결됨.
- **메모리로**: 허브 sources에 메모리 이름이 있으면 파일명으로 (`[[project_transfer_intelligence]]`).
- **원자 간**: 같은 허브의 앞뒤 원자, 다른 허브의 직접 관련 원자 → `[[../<허브slug>/NN-...]]`. 억지로 잇지 않는다 — 본문이 서로를 참조할 때만.
- 게이트 파일은 손대지 않는다 (단방향: 원자 → 게이트). 단, `gates/index.md`는 그대로.

## 허브 노트 갱신 (유일한 수정)
허브 파일 **맨 끝**에 추가:
```markdown

## Atoms
- [[../atoms/<허브slug>/01-...]] — <title>
- ...
```
(`maps/`·`rails/` 허브면 경로 깊이에 맞게)

## 크기 기대치
| 플레이북 | 허브 수 | 예상 원자 |
|---|---|---|
| hyperliquid | facts 9 + rails 2 | 100~120 |
| rails | facts 5 + maps 1 | 80~100 |
| fund | core facts 3 + arb facts 3 + carry facts 1 + dated README 본문 | 90~120 |

## 완료 기준
- 모든 허브에 `## Atoms` 절, 모든 원자에 frontmatter 8필드
- 링크 무결성: playbooks 내부 상대 링크 전부 해결 (원자료·메모리 파일명 링크는 예외)
- 원자 본문에 허브에 없는 숫자·주장 0건 (검수: 임의 원자 10개 대조)
