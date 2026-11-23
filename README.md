# 소영권

친구들이 GitHub 주소로 들어와 **Google 로그인** 후 같은 방에서 함께 싸우는 3D 난투 격투 게임.
설치 없이 브라우저(PC·모바일)에서 바로 실행됩니다.

- 3D 렌더링: Three.js
- 로그인 + 실시간 멀티플레이: Firebase (Authentication + Realtime Database) — **무료 요금제로 충분**
- 호스팅: GitHub Pages (무료)

## 조작법

| 키 | 동작 |
|---|---|
| WASD / 방향키 | 이동 (가장 가까운 상대 자동 조준) |
| J | 약공격 — 연타하면 잽 → 스트레이트 → 킥 3단 콤보 |
| K | 강공격 — 느리지만 강력, **가드를 부숨** |
| L (누르고 있기) | 가드 (피해 85% 감소) |
| L (맞기 직전 타이밍) | **패링** — 상대 1초 무방비, 내 다음 공격 1.6배 |
| Space | 점프 (공중에서 J/K = 점프킥) |
| Shift | 회피 — 짧은 무적 대시 |
| Tab | 타겟 변경 |
| Esc | 메뉴 |

모바일은 화면 왼쪽 조이스틱 + 오른쪽 버튼으로 조작합니다.
링 밖으로 떨어지면 K.O.! 마지막으로 때린 사람이 킬을 가져갑니다. 3초 후 부활.

**상성:** 약공격 연타 → 가드에 막힘 / 강공격 → 가드를 부수지만 느려서 패링·회피당함 / 패링 → 타이밍이 어려움

---

## 친구들과 하기 — 설정 (약 10분, 한 번만)

### 1단계. GitHub에 올리기
1. https://github.com 에서 새 저장소(Repository) 생성 (예: `soyoungkwon`, **Public**)
2. 이 폴더의 파일 전부(`index.html`, `css/`, `js/`, `database.rules.json`, `README.md`)를 업로드
   (저장소 페이지 → **Add file → Upload files** 로 드래그해도 됩니다)
3. 저장소 **Settings → Pages** → Source: `Deploy from a branch`, Branch: `main` / `(root)` → **Save**
4. 1~2분 뒤 주소가 생깁니다: `https://<내아이디>.github.io/soyoungkwon/`

이 상태에서도 **연습 모드(봇 대전)** 는 바로 됩니다.

### 2단계. Firebase 프로젝트 만들기 (Google 로그인 + 멀티플레이)
1. https://console.firebase.google.com → **프로젝트 추가** (Google 애널리틱스는 꺼도 됨)
2. 프로젝트 개요 화면에서 **웹 앱 추가(</> 아이콘)** → 앱 이름 입력 → 등록
3. 화면에 나오는 `firebaseConfig` 값을 복사해서 `js/firebase-config.js` 에 붙여넣기
   (`databaseURL` 이 없으면 아래 4단계 후 **프로젝트 설정**에서 다시 복사하세요)

### 3단계. Google 로그인 켜기
1. 왼쪽 메뉴 **빌드 → Authentication → 시작하기**
2. **로그인 방법** 탭 → **Google** → 사용 설정 → 저장
3. **설정** 탭 → **승인된 도메인** → **도메인 추가** → `<내아이디>.github.io` 입력
   (이걸 안 하면 GitHub 주소에서 로그인 팝업이 실패합니다)

### 4단계. Realtime Database 만들기
1. 왼쪽 메뉴 **빌드 → Realtime Database → 데이터베이스 만들기**
   (위치는 아무거나, 예: `asia-southeast1`) → **잠금 모드**로 시작
2. **규칙** 탭 → 내용을 전부 지우고 `database.rules.json` 내용을 붙여넣기 → **게시**
3. 데이터 탭 위쪽의 주소(`https://...firebasedatabase.app` 또는 `...firebaseio.com`)가
   `firebase-config.js` 의 `databaseURL` 과 같은지 확인

### 5단계. 수정한 `js/firebase-config.js` 를 GitHub에 다시 올리기
1~2분 뒤 사이트를 새로고침하면 **Google로 로그인** 버튼이 활성화됩니다.

### 6단계. 친구 초대
- 로그인 → 방 코드 입력(예: `ABCD`) → 입장
- 게임 중 우측 상단 **초대 링크 복사** → 친구에게 전송
  (`https://<내아이디>.github.io/soyoungkwon/?room=ABCD`)
- 한 방에 최대 8명까지 함께 난투

> `firebase-config.js` 의 값(apiKey 등)은 원래 공개되는 값이라 GitHub에 올려도 괜찮습니다.
> 데이터 보호는 4단계의 데이터베이스 규칙이 담당합니다 (로그인한 사람만 읽기, 각자 자기 캐릭터만 쓰기).

## 한 파일 버전 (soyoungkwon.html)

`soyoungkwon.html` 은 위의 모든 파일(css/js)을 한 파일로 합친 버전입니다.
GitHub에 이 파일 하나만 올려도 됩니다. 이름을 `index.html` 로 바꿔서 올리면
주소가 `https://<내아이디>.github.io/soyoungkwon/` 으로 깔끔해집니다.
Firebase 설정값은 파일 안에서 `YOUR_API_KEY` 를 검색해 그 부분을 바꾸면 됩니다.

## 내 PC에서 테스트하기

모듈 스크립트라 파일을 더블클릭하면 안 열립니다. 폴더에서:

```
python -m http.server 8000
```

후 http://localhost:8000 접속. (Firebase 승인된 도메인에 `localhost` 는 기본 포함)

## 파일 구조

```
index.html              화면/UI
css/style.css           스타일
js/main.js              씬, 카메라, 입력, HUD, 게임 흐름
js/fighter.js           캐릭터 모델·애니메이션·전투(패링/가드/회피/콤보) 로직
js/bot.js               연습 모드 AI
js/net.js               Firebase 로그인 + 실시간 동기화
js/sfx.js               효과음 (Web Audio 합성)
js/firebase-config.js   ← 내 Firebase 값으로 수정
database.rules.json     ← Realtime Database 규칙에 붙여넣기
```

## 밸런스 조정

`js/fighter.js` 맨 위의 `MOVES`(공격별 발동/지속/후딜/데미지/넉백), `PARRY_WIN`(패링 유효 시간, 기본 0.18초),
`DODGE_*`(회피), `ARENA_R`(링 크기) 값을 바꾸면 됩니다.

## 네트워크 방식 (참고)

각자 자기 캐릭터를 직접 움직이고 초당 15번 위치를 공유합니다. 공격이 닿으면 **맞는 사람의 화면**에서
가드/패링/회피 여부를 판정하므로, 내가 제때 패링하면 내 화면 기준으로 반드시 성공합니다.
친구끼리 즐기기용 구조라 치트 방지 기능은 없습니다.
