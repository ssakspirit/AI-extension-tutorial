# AI Extension Tutorial

인공지능 확장의 세 가지 핵심 기능(엔티티 감지, 블록 데이터 분석, 에이전트 인벤토리)을 소개하는 튜토리얼입니다.

## 튜토리얼 시작하기

```
https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial-examples
```

## 튜토리얼 시작 방법

### 방법 1: 웹 브라우저에서 시작 (마인크래프트와 연결되지 않음)

위 링크를 브라우저에서 열어주세요.

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
           "defaulturi": "https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial-examples"
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
   codebuilder navigate @p false https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial-examples
   ```
3. 커맨드 블록을 활성화하면 가장 가까운 플레이어에게 튜토리얼이 열립니다

### 방법 4: NPC 사용

1. 교육용 NPC를 배치합니다
2. NPC 설정에서 "고급설정"
3. 다음 명령어 입력:
   ```
   codebuilder navigate @initiator false https://minecraft.makecode.com/#tutorial:github:ssakspirit/AI-extension-tutorial/tutorial-examples
   ```
4. NPC와 상호작용하면 튜토리얼이 열립니다

---

## MakeCode에서 확장 직접 추가하기

튜토리얼 없이 일반 프로젝트에서 바로 사용하려면 MakeCode 편집기의 **확장(Extensions)** 버튼을 클릭한 후 검색창에 아래 URL을 입력하세요:

```
https://github.com/ssakspirit/AI-extension
```

확장이 추가되면 블록 카테고리에서 **인공지능** 명령 블록을 사용할 수 있습니다.

---

## AI Extension 소개

이 튜토리얼은 [AI Extension](https://github.com/ssakspirit/AI-extension)을 사용합니다.

---

## 라이선스

MIT License

이 확장과 튜토리얼은 스티브코딩이 제작 및 배포합니다.
