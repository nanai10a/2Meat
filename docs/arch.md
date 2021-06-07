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
  - http (Next.js) `-> Vercel`
  - Discord (serenity, hhooking)
    - Bot `-> `
    - Webhook `-> `
    - Slash Commands `-> `
  - Twitter ( ? )
    - ( ? )
- Backend
  - http ( ? )
    - REST ( ? )
    - GraphQL ( ? )
  - ws ( ? )
- Database
  - MongoDB ( ? ) `-> MongoDB Atlas`
  - Redis ( ? ) `-> `
- Auth
  - ( ? ) `-> `
