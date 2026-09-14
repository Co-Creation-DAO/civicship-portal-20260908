<a id="en"></a>

# Front-End Documentation

*English below · [日本語は下段へ](#ja)*


- Milestone 5 deliverable 1, describing the code at `df68a9a` (2026-09-07)
- A mutual-assistance application for residents, delivered as a **LINE mini app
  (LIFF)**
- Next.js 15 (App Router) and TypeScript, Tailwind CSS, Apollo Client against a
  GraphQL API, on Cloud Run behind an Edge middleware
- 206 Storybook stories document the components, published on every pull request
  through Chromatic
- GPL-3.0

---

## UI/UX design principles

Produced and submitted during Milestone 3, and approved there.

| | |
| --- | --- |
| Design principles, redesign requirements and action plan | https://hopin-inc.notion.site/What-s-Co-Creation-DAO-App-1c030b95d2b68016be45e448154a50ab |
| How interviewees were selected, the interview format, and how feedback was recorded and analysed | https://hopin-inc.notion.site/Additional-Document-M3-21130b95d2b68092aae4de53b3e5147d |
| UI design (Figma) | https://www.figma.com/design/TkZ3wAG6zj114b4N6ogJyf/Co-Creation-DAO-App-UI--Catalyst-M3- |
| Design walkthrough — participant side | https://youtube.com/playlist?list=PL0Jg6Cs8E9r3ynDqeweM-kWII2znYjr2v |
| Design walkthrough — host / admin side | https://youtube.com/playlist?list=PL0Jg6Cs8E9r1tfJ25FdtOguzyt6KWkiCV |

[From the Milestone 3 prototype to the application today](./design-traceability.md)
carries each of those values through to the screen that runs it.

The principle those documents apply here:

- The UX assumes a mobile browser inside LINE
- The residents it serves already use LINE daily
- Reaching the application requires no app installation and no Web3 wallet

---

## Integration processes

### With the backend

- The front end holds no business logic and no database access
- Everything goes through the GraphQL API in
  [`civicship-api`](https://github.com/Hopin-inc/civicship-api)
- That API's own technical documentation, submitted as Milestone 4:
  https://github.com/Hopin-inc/civicship-api/tree/master/docs/handbook

- **Transport:** Apollo Client. Server components and the Edge middleware call the
  same API over HTTP with the community's session cookie; the browser sends the
  session cookie plus an `X-Community-Id` header identifying the tenant.
- **Types:** the GraphQL schema is code-generated into TypeScript
  (`pnpm gql:generate` → `src/types/graphql.tsx`), so a schema change that breaks
  the front end fails at compile time rather than at runtime.
- **Tenancy:** every request carries the community id. The API resolves the tenant
  and the caller's identity from it, and applies row-level security accordingly.
- **Authorisation:** `src/lib/auth/core/access-policy.ts` decides which paths a
  role may reach in the interface.

### With LINE, and identity across communities

1. **LINE login** through LIFF produces an access token.
2. The API exchanges it for a **Firebase custom token** against the community's own
   Firebase tenant.
3. The portal exchanges that for an ID token and asks the API for a **session
   cookie scoped to the community** (`__session_{communityId}`).
4. **Phone-number verification** runs separately and acts as the common identity
   across communities — the same person joining two communities is recognised as
   one person.
5. A **DID** is issued against the verified phone number.

- Relevant source: `src/lib/auth/`, `src/middleware.ts`

---

## User instructions

- **NEO88 App Manual**, for experience providers:
  https://docs.google.com/presentation/d/1WypOpniKO8l7OXk1VBbkYNf7O_vYgkwDg8it4eJccxk/edit
- The [recordings for deliverable 3](./demo/) show the current flow

---
---

<a id="ja"></a>

# フロントエンド ドキュメント

*[English is above](#en)*

- Milestone 5 成果物1。`df68a9a`（2026-09-07）時点のコードについて記述している
- 住民同士の助け合いのためのアプリケーションで、**LINE ミニアプリ（LIFF）** として
  提供する
- Next.js 15（App Router）と TypeScript、Tailwind CSS、GraphQL API に対する Apollo
  Client、実行環境は Cloud Run で前段に Edge middleware
- コンポーネントは206個の Storybook ストーリーとして文書化されており、
  プルリクエストごとに Chromatic 経由で公開される
- GPL-3.0

---

## UI/UX 設計原則

Milestone 3 の期間中に作成・提出し、承認されたもの。

| | |
| --- | --- |
| 設計原則、再設計要件、アクションプラン | https://hopin-inc.notion.site/What-s-Co-Creation-DAO-App-1c030b95d2b68016be45e448154a50ab |
| インタビュー対象者の選定方法、インタビュー形式、フィードバックの記録・分析方法 | https://hopin-inc.notion.site/Additional-Document-M3-21130b95d2b68092aae4de53b3e5147d |
| UI デザイン（Figma） | https://www.figma.com/design/TkZ3wAG6zj114b4N6ogJyf/Co-Creation-DAO-App-UI--Catalyst-M3- |
| デザイン ウォークスルー — 参加者側 | https://youtube.com/playlist?list=PL0Jg6Cs8E9r3ynDqeweM-kWII2znYjr2v |
| デザイン ウォークスルー — ホスト / 管理者側 | https://youtube.com/playlist?list=PL0Jg6Cs8E9r1tfJ25FdtOguzyt6KWkiCV |

[M3 のプロトタイプから現在のアプリケーションまで](./design-traceability.md)に、
各価値が動作中の画面へ至るまでの対応を示している。

それらの資料が本実装に適用している原則：

- UX は LINE 内のモバイルブラウザを前提とする
- 対象となる住民は既に LINE を日常的に使っている
- 利用にあたってアプリのインストールも Web3 ウォレットの管理も必要としない

---

## 連携方式

### バックエンドとの連携

- フロントエンドは業務ロジックもデータベースアクセスも持たない
- すべては [`civicship-api`](https://github.com/Hopin-inc/civicship-api) の
  GraphQL API を経由する
- API 自体の技術ドキュメント（Milestone 4 として提出）：
  https://github.com/Hopin-inc/civicship-api/tree/master/docs/handbook

- **通信：** Apollo Client。サーバーコンポーネントと Edge middleware は同じ API を
  コミュニティのセッション cookie 付きで HTTP 呼び出しし、ブラウザはセッション cookie に
  加えてテナントを示す `X-Community-Id` ヘッダを送信する。
- **型：** GraphQL スキーマから TypeScript を自動生成しており
  （`pnpm gql:generate` → `src/types/graphql.tsx`）、フロントエンドを壊すスキーマ変更は
  実行時ではなくコンパイル時に失敗する。
- **テナンシー：** すべてのリクエストがコミュニティ ID を持つ。API はそこからテナントと
  呼び出し元のアイデンティティを解決し、行レベルセキュリティを適用する。
- **認可：** `src/lib/auth/core/access-policy.ts` が画面上でどのロールがどのパスに
  到達できるかを決める。

### LINE との連携と、コミュニティ横断のアイデンティティ

1. LIFF 経由の **LINE ログイン**でアクセストークンを取得する。
2. API がそれを、当該コミュニティ専用の Firebase テナントに対する
   **Firebase カスタムトークン**と交換する。
3. ポータルがそれを ID トークンと交換し、API に**コミュニティスコープのセッション
   cookie**（`__session_{communityId}`）を要求する。
4. **電話番号認証**を別途実施し、これがコミュニティ横断の共通 ID として機能する —
   同一人物が2つのコミュニティに参加した場合も1人として認識される。
5. 検証済みの電話番号に対して **DID** を発行する。

- 関連するソース：`src/lib/auth/`、`src/middleware.ts`

---

## 利用者向け手順書

- **NEO88 アプリマニュアル**（体験提供事業者向け）：
  https://docs.google.com/presentation/d/1WypOpniKO8l7OXk1VBbkYNf7O_vYgkwDg8it4eJccxk/edit
- 現在の操作フローは[成果物3の録画](./demo/)で示している
