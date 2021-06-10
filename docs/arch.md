# twomeat-system

[![hackmd-github-sync-badge](https://hackmd.io/9WMKQnaKQQObY1Gi5mbS6Q/badge)](https://hackmd.io/9WMKQnaKQQObY1Gi5mbS6Q)

### 要件定義

- 安定して且つ拡張可能な多機能systemの構築.

これが全て.

### 設計原理

- CArch(Clean Archtecture)を参考にし拡張可能且つ保守性の高いシステムの構築.
- システムは以下のように細分化される.
  - Frontend
  - Backend
  - Database
  - Auth
- 細分化されたシステムは原則として単体で動作するものとする.

### 詳細

- Frontend
  - http ([Next.js](https://github.com/vercel/next.js)) `-> Vercel`
  - Discord
    - Bot ([serenity](https://github.com/serenity-rs/serenity)) `-> GCE`
    - Webhook ([hhooking](https://github.com/Nanai10a/hhooking)) `-> GCF`
    - Slash Commands ([hhooking](https://github.com/Nanai10a/hhooking)) `-> GCF`
  - Twitter
    - REST ([egg-mode](https://github.com/egg-mode-rs/egg-mode)?) `-> GCE`
    - Webhook ( 独自lib? ) `-> `
- Backend `-> GCE`
  - http ([warp](https://github.com/seanmonstar/warp))
    - REST ([warp](https://github.com/seanmonstar/warp))
    - GraphQL ([juniper, juniper_warp](https://github.com/graphql-rust/juniper))
  - ws ([warp](https://github.com/seanmonstar/warp))
- Database
  - MongoDB ([mongodb](https://github.com/mongodb/mongo-rust-driver)) `-> MongoDB Atlas`
- Auth
  - ( 独自lib? ) `-> `

GCEにdeployされる小systemはdocker-composeによって統括管理され, 維持を行う.

### Arch

CArchの有名な図を以下に示す.

![](https://i.imgur.com/H1qkCGs.png)

![](https://i.imgur.com/bW7Ka78.png)



http/wsでrequestを受けてそれに返答をしないといけないため, 特にhttpは同期をとってPresenter/Viewの内容をresponseする必要がある.  
今回考案したのはrequest-handlerでrequestIdを振りControllerに渡し, Viewの中でrequestIdを処理しhandlerにchannelを通じてデータを送る, といったやり方.  
~~これがどう出るか~~

wsは最初にinitial responseとしてrequestIdを送り返して受諾を通知し, idと共にasync的に返答を返す, といったものを検討している.

ただ, requestIdは上位層には関係のない話なので`_`をprefixにしようかなと思っている(けどどうなんでしょうね).
