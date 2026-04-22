# 인공지능 확장 튜토리얼

## 소개 @unplugged

**인공지능(AI) 확장**을 사용하여 마인크래프트 에이전트가 주변을 감지하고, 블록을 분석하고, 인벤토리를 스스로 관리하도록 만들어봅시다!

이 튜토리얼에서는 3가지 AI 기능을 배웁니다:
- **엔티티 감지**: 에이전트 주변의 몹이나 플레이어 찾기
- **블록 데이터 분석**: 에이전트 앞 블록의 종류 파악하기
- **에이전트 인벤토리**: 아이템 자동 정렬 및 내려놓기

## 단계 1

먼저 플레이어가 "감지"라고 채팅하면 실행되도록 해봅시다.

``||player:채팅 명령어||`` 블록을 작업 공간에 추가하세요.

```blocks
player.onChat("감지", function () {

})
```

## 단계 2

이제 에이전트 주변의 엔티티를 감지해봅시다.

``||인공지능:에이전트 주변 반경 감지||`` 블록을 추가하여 반경 3칸 안의 모든 엔티티를 최대 1개 감지합니다.

```blocks
player.onChat("감지", function () {
    let target = ai.scanNear(ai.ScanCenter.Agent, ai.ScanTarget.All, 3, 1)
})
```

## 단계 3 @unplugged

**감지 기준**을 선택할 수 있습니다:
- **에이전트**: 에이전트 위치를 기준으로 주변 감지
- **플레이어**: 플레이어 위치를 기준으로 주변 감지

**감지 대상**도 선택할 수 있습니다:
- **전체**: 모든 엔티티
- **플레이어**: 플레이어만
- **몬스터**: 몬스터만
- **몹**: 동물 등 일반 몹만

## 단계 4

감지된 엔티티에게 메시지를 보내봅시다.

``||몹:~에게 말하기||`` 블록을 연결하면 감지된 엔티티에게 메시지가 표시됩니다.

```blocks
player.onChat("감지", function () {
    let target = ai.scanNear(ai.ScanCenter.Agent, ai.ScanTarget.All, 3, 1)
    mobs.say(target, "AI가 당신을 감지했습니다!")
})
```

## 단계 5

이번에는 몬스터만 감지하도록 바꿔봅시다.

감지 대상을 **몬스터**로 변경하세요.

```blocks
player.onChat("감지", function () {
    let target = ai.scanNear(ai.ScanCenter.Agent, ai.ScanTarget.Monster, 3, 1)
    mobs.say(target, "위험! 몬스터 발견!")
})
```

## 단계 6 @unplugged

잘 했습니다! 이제 **블록 데이터 분석**을 배워봅시다.

에이전트가 앞으로 나아가면서 블록을 부수고, 어떤 종류의 블록이 얼마나 있는지 분석합니다.

분석 순서:
1. **블록 분석 초기화** — 이전 데이터를 지웁니다
2. **추적 블록 추가** — 어떤 블록을 셀지 등록합니다
3. **블록 분석** — 에이전트가 한 칸 부수고 기록합니다
4. **결과 확인** — 몇 개인지 출력합니다

## 단계 7

"분석"이라고 채팅하면 실행되는 새 명령을 만들고, 블록 분석을 준비해봅시다.

``||인공지능:블록 분석 초기화||``와 ``||인공지능:추적 블록 추가||`` 블록을 추가하세요.

```blocks
player.onChat("분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(GRASS)
    ai.addTrackedBlock(DIRT)
})
```

## 단계 8

반복 블록 안에서 에이전트가 10번 블록을 분석하도록 해봅시다.

``||loops:반복||`` 블록과 ``||인공지능:에이전트 방향 블록 분석||`` 블록을 추가하세요.

```blocks
player.onChat("분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(GRASS)
    ai.addTrackedBlock(DIRT)
    for (let i = 0; i < 10; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Forward)
    }
})
```

## 단계 9 @unplugged

**블록 분석** 동작 방식:
- 에이전트 앞 블록이 공기면 건너뜁니다
- 블록이 있으면 종류를 확인하고, 추적 목록에 있으면 카운트합니다
- 그리고 블록을 부수고 다음으로 넘어갑니다

이렇게 하면 에이전트가 지나간 땅의 블록 구성을 파악할 수 있습니다!

## 단계 10

분석이 끝나면 결과를 채팅으로 출력해봅시다.

``||인공지능:전체 추적 개수||``와 ``||인공지능:블록 추적 개수||`` 블록으로 결과를 확인합니다.

```blocks
player.onChat("분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(GRASS)
    ai.addTrackedBlock(DIRT)
    for (let i = 0; i < 10; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Forward)
    }
    player.say("전체: " + ai.getTotalBroken())
    player.say("잔디: " + ai.getBlockCount(GRASS))
    player.say("흙: " + ai.getBlockCount(DIRT))
})
```

## 단계 11 @unplugged

훌륭합니다! 마지막으로 **에이전트 인벤토리** 관리를 배워봅시다.

에이전트는 블록을 부수면서 아이템을 인벤토리에 모읍니다. 시간이 지나면 인벤토리가 섞여 지저분해질 수 있습니다. 인공지능 확장으로 자동 정리할 수 있습니다!

## 단계 12

"정렬"이라고 채팅하면 에이전트 인벤토리를 자동 정렬하도록 해봅시다.

``||인공지능:에이전트 인벤토리 정렬||`` 블록을 추가하세요.

```blocks
player.onChat("정렬", function () {
    ai.sortAgentInventory()
})
```

## 단계 13

"버리기"라고 채팅하면 에이전트가 가진 흙을 앞에 내려놓도록 해봅시다.

``||인공지능:에이전트가 방향으로 내려놓기||`` 블록을 추가하세요.

```blocks
player.onChat("버리기", function () {
    ai.agentDropItem(ai.AgentDirection.Forward, DIRT)
})
```

## 완료! @unplugged

축하합니다! 인공지능 확장의 3가지 핵심 기능을 모두 배웠습니다!

**핵심 정리:**

🔍 **엔티티 감지**
- `scanNear`: 기준 위치, 대상 종류, 반경, 최대 개수 설정
- 감지된 엔티티에게 명령 실행 가능

🧱 **블록 데이터 분석**
- 초기화 → 추적 블록 등록 → 반복 분석 → 결과 확인
- 에이전트가 실제로 블록을 부수며 종류를 기록

📦 **에이전트 인벤토리**
- `sortAgentInventory`: 같은 아이템끼리 모아 정렬
- `agentDropItem`: 특정 아이템만 골라서 내려놓기

**활용 아이디어:**
- 몬스터 감지 경보 시스템
- 지형 구성 분석기
- 자동 인벤토리 정리 도우미
