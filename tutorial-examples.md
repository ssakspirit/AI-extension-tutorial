# 인공지능 확장 예제 모음

## 소개 @unplugged

인공지능 확장으로 만들 수 있는 다양한 실용적인 예제를 배워봅시다!

몬스터 경보 시스템, 지형 분석기, 자동 인벤토리 관리 등 실제로 활용할 수 있는 프로그램을 만들어볼 거예요.

## 예제 1: 주변 몬스터 경보

"경보"라고 채팅하면 주변 5칸 안의 몬스터를 감지하고 경고 메시지를 보냅니다.

```blocks
player.onChat("경보", function () {
    let enemy = ai.scanNear(ai.ScanCenter.Agent, ai.ScanTarget.Monster, 5, 3)
    mobs.say(enemy, "위험! 에이전트가 감지했습니다!")
})
```

## 예제 2: 가장 가까운 플레이어 찾기

"찾기"라고 채팅하면 에이전트 주변 10칸 안의 플레이어를 찾아 인사합니다.

```blocks
player.onChat("찾기", function () {
    let found = ai.scanNear(ai.ScanCenter.Agent, ai.ScanTarget.Player, 10, 1)
    mobs.say(found, "안녕하세요! 에이전트가 당신을 발견했습니다!")
})
```

## 예제 3: 플레이어 기준 감지

"주변"이라고 채팅하면 플레이어 위치를 기준으로 주변의 모든 엔티티를 감지합니다.

```blocks
player.onChat("주변", function () {
    let nearby = ai.scanNear(ai.ScanCenter.Player, ai.ScanTarget.All, 4, 5)
    mobs.say(nearby, "플레이어 근처에 있습니다!")
})
```

## 예제 4: 잔디 땅 분석

"잔디분석"이라고 채팅하면 에이전트 앞 5칸의 잔디 블록을 분석합니다.

```blocks
player.onChat("잔디분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(GRASS)
    for (let i = 0; i < 5; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Forward)
    }
    player.say("잔디: " + ai.getBlockCount(GRASS) + " / 전체: " + ai.getTotalBroken())
})
```

## 예제 5: 흙과 잔디 비율 분석

"땅분석"이라고 채팅하면 에이전트 앞 10칸의 흙과 잔디 비율을 분석합니다.

```blocks
player.onChat("땅분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(GRASS)
    ai.addTrackedBlock(DIRT)
    for (let i = 0; i < 10; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Forward)
    }
    player.say("전체 부순 블록: " + ai.getTotalBroken())
    player.say("잔디: " + ai.getBlockCount(GRASS))
    player.say("흙: " + ai.getBlockCount(DIRT))
})
```

## 예제 6: 돌 채굴 분석

"채굴분석"이라고 채팅하면 에이전트 앞 8칸의 돌과 자갈을 분석합니다.

```blocks
player.onChat("채굴분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(STONE)
    ai.addTrackedBlock(GRAVEL)
    for (let i = 0; i < 8; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Forward)
    }
    player.say("전체: " + ai.getTotalBroken())
    player.say("돌: " + ai.getBlockCount(STONE))
    player.say("자갈: " + ai.getBlockCount(GRAVEL))
})
```

## 예제 7: 아래쪽 블록 분석

"아래분석"이라고 채팅하면 에이전트 아래 블록을 분석합니다.

```blocks
player.onChat("아래분석", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(GRASS)
    ai.addTrackedBlock(DIRT)
    ai.addTrackedBlock(STONE)
    for (let i = 0; i < 5; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Down)
    }
    player.say("전체: " + ai.getTotalBroken())
    player.say("잔디: " + ai.getBlockCount(GRASS))
    player.say("흙: " + ai.getBlockCount(DIRT))
    player.say("돌: " + ai.getBlockCount(STONE))
})
```

## 예제 8: 인벤토리 자동 정렬

"청소"라고 채팅하면 에이전트 인벤토리를 자동으로 정리합니다.

```blocks
player.onChat("청소", function () {
    ai.sortAgentInventory()
    player.say("인벤토리 정렬 완료!")
})
```

## 예제 9: 흙 버리기

"흙버리기"라고 채팅하면 에이전트가 가진 흙 블록을 앞에 모두 내려놓습니다.

```blocks
player.onChat("흙버리기", function () {
    ai.agentDropItem(ai.AgentDirection.Forward, DIRT)
    player.say("흙 내려놓기 완료!")
})
```

## 예제 10: 돌 버리기

"돌버리기"라고 채팅하면 에이전트가 가진 돌 블록을 뒤에 내려놓습니다.

```blocks
player.onChat("돌버리기", function () {
    ai.agentDropItem(ai.AgentDirection.Back, STONE)
    player.say("돌 내려놓기 완료!")
})
```

## 예제 11: 채굴 후 정리

"채굴정리"라고 채팅하면 분석 후 인벤토리를 자동 정렬합니다.

```blocks
player.onChat("채굴정리", function () {
    ai.resetAnalysis()
    ai.addTrackedBlock(STONE)
    ai.addTrackedBlock(DIRT)
    for (let i = 0; i < 6; i++) {
        ai.analyzeBlocks(ai.AgentDirection.Forward)
    }
    player.say("채굴 완료! 전체: " + ai.getTotalBroken())
    ai.sortAgentInventory()
    player.say("인벤토리 정렬 완료!")
})
```

## 예제 12: 몬스터 감지 후 경보 + 도망

"도망"이라고 채팅하면 몬스터를 감지하고 메시지를 보냅니다.

```blocks
player.onChat("도망", function () {
    let enemy = ai.scanNear(ai.ScanCenter.Player, ai.ScanTarget.Monster, 8, 1)
    mobs.say(enemy, "멈춰라! 에이전트가 발견했다!")
    player.say("몬스터 감지! 조심하세요!")
})
```

## 완료! @unplugged

축하합니다! 인공지능 확장의 다양한 활용 예제를 배웠습니다.

**배운 것:**
- 에이전트/플레이어 기준으로 엔티티 감지
- 여러 종류의 블록 동시 추적 분석
- 다양한 방향으로 블록 분석
- 인벤토리 자동 정렬 및 아이템 내려놓기
- 여러 기능을 조합한 복합 프로그램

**이제 해볼 것:**
- 감지 반경을 바꿔서 넓은 범위 탐지
- 다양한 블록 종류 추적해보기
- 채굴 + 분석 + 정렬을 하나의 명령으로 자동화
- 몬스터 감지 경보 시스템 만들기
