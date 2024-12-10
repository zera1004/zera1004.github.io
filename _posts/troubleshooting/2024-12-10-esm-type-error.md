---
title:  "[Troubleshooting] 변수 가져올 때 typeError"
excerpt: "[Troubleshooting] 변수 가져올 때 typeError"

categories:
  - Troubleshooting
tags:
  - [Troubleshooting]

toc: true
toc_sticky: true
 
date: 2024-12-10 20:15:10 +0900
last_modified_at: 2024-12-10 20:16:10 +0900
---

## Basic 간단한 CRUD 과제 중 트러블 슈팅

<br>

### 배경

Basic 과제인 mvc패턴으로 express와 인메모리 방식을 이용해 간단한 축구선수 CRUD를 구현하던 중

<br>

### 발단

app.js에 만들어놨던 변수를 playerController.js에서 불러와 재할당해서 실행 시켰는데 오류가 발생했다.

```js
// app.js
export let player = [];
```

```js
// playerController.js
import * as playerModel from "../models/playerModel.js";
import { player } from "../app.js";

// 선수 업데이트
export const updateUser = async (req, res) => {
  try {
    const { name, speed, shouting } = req.body;

    if (!name || !speed || !shouting)
      return res
        .status(400)
        .json({ error: "name, speed, shouting을 전부 입력해 주세요" });
    if (!player[0] || !player.filter((i) => i.name === name)[0])
      return res.status(400).json({ error: "존재하지 않는 선수입니다." });
    let value = { name, speed, shouting };
    player = await playerModel.updateUser(player, value);
    return res
      .status(201)
      .json({ message: "성공적으로 선수가 업데이트 되었습니다." });
  } catch (err) {
    console.log(err);
    return res.status(500).json({ error: "서버 오류가 발생하였습니다." });
  }
};
```

```
TypeError: Assignment to constant variable.
```

<br>

### 전개

insomnia로 테스트 하는데 catch문으로 가서 '서버 오류가 발생하였습니다.'가 응답으로 돌아와서,  
문제가 될만한 부분에 console.log를 찍어 출력이 안되는 부분을 찾았다.

```js
player = await playerModel.updateUser(player, value);
```

그 결과 위의 문장에서 오류가 발생함을 알게 되었다.

분명 내가 기억하기로는 let은 재할당이 되고, const로 선언할 경우 재할당이 안되는 걸로 알아서  
값을 할당하고 import하면 오류 생기는 건가라는 생각으로 ```let player```까지만 작성해서 import도 해봤지만 되지않았다.

<br>

### 위기

그리고 그렇다면 playerModel부분이 문제일까라고도 생각을 했다.

```js
// playerModel.js
export const updateUser = async (playerData, value) => {
  return playerData.map((i) => {
    if (i.name === value.name) return value;
    return i;
  });
};
```

그런데 간단한 코드라 잘못될 이유가 전혀 없어 보였다.

그래서 CRUD의 delete인 선수 삭제 부분도 insomnia로 실행해 봤는데, 역시 똑같은 오류가 생겼다.

```js
// playerController.js
import * as playerModel from "../models/playerModel.js";
import { player } from "../app.js";
// 선수 삭제
export const deleteUser = async (req, res) => {
  try {
    const { name } = req.body;
    if (!player[0] || !player.filter((i) => i.name === name)[0])
      return res.status(400).json({ error: "존재하지 않는 선수입니다." });

    player = await playerModel.deleteUser(player, name);
    return res
      .status(200)
      .json({ message: "성공적으로 선수가 삭제되었습니다." });
  } catch (err) {
    console.log(err);
    return res.status(500).json({ error: "서버 오류가 발생하였습니다." });
  }
};
```

```js
// playerModel.js
export const deleteUser = async (playerData, value) => {
  return playerData.filter(i => i.name !== value)
};
```

그래서 내가 모르는 어떤 규칙이 있을꺼라고 생각이 들어,  
구글에 "let import 수정 typeerror: assignment to constant variable."라고 검색해 봤다.

<br>

### 절정

블로그에 들어가서 봤더니, ESM은 임포트된 모듈이 익스포트된 값에 대해 읽기 전용 라이브 바인딩된다고 했다.

쉽게말해, ESM에서는 import해온 변수를 직접 변경할 수 없는 것이었다.

하지만 함수를 이용해서 변경이 가능하다는 것을 보았다.

```js
// app.js
import express from "express";
import PlayerRouter from "./routers/player.js";

const app = express();
const PORT = 3030;

export let player = [];
export function setPlayer(data) {
  player = data;
}

app.use(express.json());

app.use("/player", PlayerRouter);

app.listen(PORT, () => {
  console.log(PORT, "포트로 서버 열림");
});
```

```js
// playerController.js
import * as playerModel from "../models/playerModel.js";
import { player, setPlayer } from "../app.js";
// 선수 업데이트
export const updateUser = async (req, res) => {
  try {
    const { name, speed, shouting } = req.body;

    if (!name || !speed || !shouting)
      return res
        .status(400)
        .json({ error: "name, speed, shouting을 전부 입력해 주세요" });
    if (!player[0] || !player.filter((i) => i.name === name)[0])
      return res.status(400).json({ error: "존재하지 않는 선수입니다." });
    let value = { name, speed, shouting };
    setPlayer(await playerModel.updateUser(player, value));
    return res
      .status(201)
      .json({ message: "성공적으로 선수가 업데이트 되었습니다." });
  } catch (err) {
    console.log(err);
    return res.status(500).json({ error: "서버 오류가 발생하였습니다." });
  }
};
```

이렇게 app.js에 player값을 바꿔주는 함수를 만들어 playerController파일에 적용해 주었더니 원하던 대로 선수 업데이트, 삭제 전부 잘 되었다.

<br>

### 결말

이제 변수를 가져와서 변경시킬 때 함수도 같이 만들어 import하면 원하는대로 변경할 수 있다는 것을 알게 되었다.

<br>

### p.s.

```js
    if (!player[0] || !player.filter((i) => i.name === name)[0])
      return res.status(400).json({ error: "존재하지 않는 선수입니다." });
```

```find```가 기억이 안나서 생각나는대로 ```filter```로 했는데 확실히 코드가 별로인 것 같다.  
기본적인 내장함수를 확실하게 익혀야겠다.

그리고 사실 player선언을 playerController에 가져와서 해도 되긴했는데,  
왜 안되지 하는 호기심 때문에 계속 시도하고 찾아봐서 시간은 많이 걸렸지만 ESM 특징에 대해 배울 수 있어서 가치가 있었던 것 같다.