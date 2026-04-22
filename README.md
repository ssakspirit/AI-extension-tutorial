# AI Extension Tutorial

인공지능 확장 명령블록 사용법을 배우는 단계별 튜토리얼입니다.

## 튜토리얼 목록

### 기본 튜토리얼 (tutorial.md)
- 엔티티 감지 — 에이전트/플레이어 기준, 대상 종류 선택
- 블록 데이터 분석 — 초기화, 추적 블록 등록, 반복 분석, 결과 확인
- 에이전트 인벤토리 — 자동 정렬, 아이템 내려놓기

**시작하기:**
```
https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial
```

### 예제 모음 (tutorial-examples.md)
- 주변 몬스터 경보 시스템
- 플레이어/에이전트 기준 엔티티 탐지
- 잔디·흙·돌 지형 구성 분석
- 다양한 방향 블록 분석 (앞, 아래)
- 인벤토리 자동 정렬 및 아이템 내려놓기
- 채굴 + 분석 + 정렬 복합 자동화

**시작하기:**
```
https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial-examples
```

## 튜토리얼 시작 방법

### 방법 1: 웹 브라우저에서 시작 (마인크래프트와 연결되지 않음)

브라우저에서 원하는 튜토리얼 링크를 열어주세요:
- 기본: `https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial`
- 예제: `https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial-examples`

### 방법 2: education.json 파일 사용 (권장)

월드가 시작될 때 자동으로 Code Builder에서 튜토리얼을 열도록 설정할 수 있습니다.

1. 마인크래프트 Education Edition 월드 폴더로 이동:
   ```
   설치 파일로 설치한 경우
   C:\Users\사용자이름\AppData\Roaming\Minecraft Education Edition\games\com.mojang\minecraftWorlds

   스토어 경유해서 설치한 경우
   C:\Users\사용자이름\AppData\Local\Packages\Microsoft.MinecraftEducationEdition_8wekyb3d8bbwe\LocalState\games\com.mojang\minecraftWorlds
   ```

2. 월드 폴더 안에 `education.json` 파일을 생성하거나 수정:
   ```json
   {
       "codebuilder": {
           "canResize": true,
           "defaulturi": "https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial"
       },
       "commands": {
           "hiddenFromPlayer": [""]
       }
   }
   ```

3. 월드에 접속하면 자동으로 튜토리얼이 열립니다!

### 방법 3: 커맨드 블록 사용

1. 크리에이티브 모드에서 커맨드 블록을 설치합니다
2. 커맨드 블록에 다음 명령어를 입력:
   ```
   codebuilder navigate @p false https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial
   ```
3. 커맨드 블록을 활성화하면 가장 가까운 플레이어에게 튜토리얼이 열립니다

### 방법 4: NPC 사용

1. 교육용 NPC를 배치합니다
2. NPC 설정에서 "고급설정"
3. 다음 명령어 입력:
   ```
   codebuilder navigate @initiator false https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial
   ```
4. NPC와 상호작용하면 튜토리얼이 열립니다

---

## AI Extension 소개

이 튜토리얼은 [AI Extension](https://github.com/ssakspirit/AI-extension)을 사용합니다.

### 주요 기능

**엔티티 감지**
- `scanNear`: 기준 위치(에이전트/플레이어), 대상 종류(전체/플레이어/몬스터/몹), 반경, 최대 개수 설정
- 감지된 엔티티에게 메시지 전송 등 다양한 명령 실행 가능

**블록 데이터 분석**
- `resetAnalysis`: 이전 분석 데이터 초기화
- `addTrackedBlock`: 추적할 블록 종류 등록
- `analyzeBlocks`: 지정 방향 블록 분석 및 파괴
- `getTotalBroken` / `getBlockCount`: 전체 및 개별 블록 집계

**에이전트 인벤토리**
- `sortAgentInventory`: 같은 아이템끼리 모아 슬롯 1번부터 정렬
- `agentDropItem`: 특정 아이템만 골라서 지정 방향으로 내려놓기

### MakeCode에서 확장 추가하기

튜토리얼이 아닌 일반 프로젝트에서 AI Extension을 사용하려면:

1. MakeCode 편집기에서 **확장(Extensions)** 버튼을 클릭합니다
2. 검색창에 다음 GitHub 저장소 URL을 입력합니다:
   ```
   https://github.com/ssakspirit/AI-extension
   ```
3. 검색 결과에서 AI Extension을 선택합니다
4. 확장이 추가되면 블록 카테고리에서 **인공지능** 명령 블록을 사용할 수 있습니다

---

## 문제 해결

### 튜토리얼이 열리지 않는 경우
- 인터넷 연결을 확인하세요
- 브라우저에서 먼저 테스트해보세요
- URL이 정확한지 확인하세요

### 인공지능 블록이 보이지 않는 경우
- 튜토리얼을 완전히 닫고 다시 열어보세요
- 브라우저 캐시를 지우고 다시 시도하세요
- 특정 커밋 버전으로 불러오려면 `https://github.com/ssakspirit/AI-extension#{커밋해시}` 형식 사용

### 블록 분석 카운트가 누적되지 않는 경우
- `resetAnalysis` 블록을 for 루프 **바깥**에 배치했는지 확인하세요
- `addTrackedBlock`으로 추적할 블록을 등록했는지 확인하세요

---

## 라이선스

MIT License

이 확장과 튜토리얼은 스티브코딩이 제작 및 배포합니다.
