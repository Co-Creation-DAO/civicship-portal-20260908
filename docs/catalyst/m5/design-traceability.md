<a id="en"></a>

# From the Milestone 3 Prototype to the Application Today

*English below · [日本語は下段へ](#ja)*


Project Catalyst F12, Project ID 1200088.

Milestone 3 gathered user feedback through interviews, distilled it into a set
of values, and expressed those values as a Figma prototype. This document carries
that chain one step further: from each value, to what the prototype made of it,
to the screen that runs it today.

Sources:

| | |
| --- | --- |
| The five values, with the interview evidence behind each | [What's Co-Creation DAO App](https://hopin-inc.notion.site/What-s-Co-Creation-DAO-App-1c030b95d2b68016be45e448154a50ab) |
| Value-to-Interface Mapping | [Additional Document M3](https://hopin-inc.notion.site/Additional-Document-M3-21130b95d2b68092aae4de53b3e5147d) |
| The prototype | [Figma](https://www.figma.com/design/TkZ3wAG6zj114b4N6ogJyf/Co-Creation-DAO-App-UI--Catalyst-M3-) |

Paths below are relative to **https://dev.civicship.app/community/neo88**.

## What Milestone 5 submitted against what Milestone 3 submitted

Milestone 3 submitted a design. Milestone 5 submitted the application that
design became.

| Milestone 3 | Milestone 5 |
| --- | --- |
| A UI/UX design prototype in Figma | The front end itself — [source](https://github.com/Co-Creation-DAO/civicship-portal-20260908), [documentation](./frontend-documentation.md), and a [running deployment](https://civicship.app/community/neo88) |
| Design walkthrough videos: the prototype, narrated, in two playlists | [Use-case recordings](./demo/): the running application, in the same two sets |
| Requirements for the redesign, and an action plan | This document — each value, and the screen that carries it |

The recordings keep the split visible. [`milestone3-use-cases/`](./demo/milestone3-use-cases/)
holds the eleven use cases Milestone 3 demonstrated, recorded again on the
current application. [`beyond-milestone3/`](./demo/beyond-milestone3/) holds ten
that go past it. This document reads the same way: sections 1 to 6 are what the
prototype set out, and the two sections after them are what was left for later
and what was built beyond it.

## 1. Visualising local people, activities and resources

| | |
| --- | --- |
| Prototype | A map showing region-based activity hubs and their status; a host-side My Page listing hosted activities and recruitment status; recruitment reachable directly from a map marker |
| Today | `/places`, `/places/[id]`, `/users/me`, `/users/[id]`, `/admin/places`, `/admin/places/new` |

The related approach in the Milestone 3 document — leaving a participant's
involvement as a portfolio — runs at `/users/me/portfolios`.

## 2. Exchange of value rather than money

| | |
| --- | --- |
| Prototype | An invitation-ticket interface, issued by a host to chosen participants after an activity; tokens as an expression of future intent rather than payment for work done |
| Today | `/tickets`, `/tickets/receive`, `/admin/tickets`, `/admin/tickets/utilities`, `/wallets/me`, `/wallets/donate`, `/transactions`, `/admin/wallet/issue`, `/admin/wallet/grant` |

## 3. Relationships built in stages

| | |
| --- | --- |
| Prototype | Two content types, kept distinct: Activity and Quest |
| Today | `/opportunities`, `/opportunities/search`, `/opportunities/[id]`, `/reservation/select-date`, `/reservation/confirm`, `/reservation/complete`, `/participations/[id]` |

The two types are a filter over one listing rather than two listings: `/activities`
and `/quests` redirect to `/opportunities/search?type=activity` and `?type=quest`,
matching the Value-to-Interface Mapping's "flexible filtering based on type,
location, and time".

## 4. An interface that carries atmosphere

| | |
| --- | --- |
| Stated approach | Interview articles placed alongside the activities; activity photographs uploaded by the people who took part; an interface led by photographs and a map rather than by text |
| Today | A host's interview appears on the opportunity they run — [`HostInfoSection.tsx`](../../../src/app/community/%5BcommunityId%5D/opportunities/%5Bid%5D/components/OpportunityContent/HostInfoSection.tsx) renders it beside the host's name — and a place carries its related articles at `/places/[id]`. Either opens at `/articles/[id]`. Activity photographs are uploaded by the people who took part, attached to a points transfer: `/wallets/donate` and `/admin/wallet/grant` both take them through [`TransferInputStep.tsx`](../../../src/app/community/%5BcommunityId%5D/admin/wallet/grant/components/TransferInputStep.tsx), and `/transactions/[id]` edits them afterwards. |

## 5. Experience that leads to further experience

| | |
| --- | --- |
| Stated approach | Examples rather than a design — a multi-person application through a shared invitation link, recommendation of nearby events held on the same day, "etc." |
| Today | A host issues an invitation for a set number of people and shares it from `/admin/tickets/[id]` as a QR code or a copied link; each person who opens it claims their own at `/tickets/receive`. One application covers several people: `/reservation/select-date` takes a party size and `/reservation/confirm` settles a ticket or a point allocation for each. Activities are searched and filtered at `/opportunities/search` and `/search/result`. |

## 6. Opportunities to apply skills and experience

| | |
| --- | --- |
| Prototype | A search interface to browse activities and quests by interest or need; skill-tagged recommendations noted as future scope |
| Today | A Quest is the form an opportunity takes when the participant contributes rather than receives. `/opportunities/search?type=quest` lists them, and a quest states the points the participant will earn where an activity states a fee, a point cost or a ticket — [`displayPointsOrFee.tsx`](../../../src/utils/opportunity/displayPointsOrFee.tsx) is where the two diverge. |

## Left for a later milestone

| Milestone 3 | Today |
| --- | --- |
| "(Future scope) Skill-tagged recommendations" | Not built. |

## Beyond Milestone 3

Resident-card NFTs were already present in Milestone 3's interview evidence — "Through NFT or token ownership, even remote individuals can participate in the local economy", recorded under the participants' second value — though not among the interfaces the prototype covered.

| Area | Screens |
| --- | --- |
| DAO voting | `/votes`, `/votes/[topicId]`, `/admin/votes` |
| Verifiable credentials | `/credentials/[id]`, `/admin/credentials`, `/admin/credentials/issue` |
| Resident-card NFTs | `/nfts/[id]`, `/admin/nfts` |
| Member bonuses | `/admin/bonuses`, `/admin/bonuses/signup` |
| Analytics | `/admin/analytics` |
| System administration | under `/sysAdmin` |

---
---

<a id="ja"></a>

# Milestone 3 のプロトタイプから、現在のアプリケーションまで

*[English is above](#en)*

Project Catalyst F12、Project ID 1200088。

Milestone 3 では、インタビューを通じて利用者のフィードバックを収集し、それを複数の
価値に整理したうえで、Figma プロトタイプとして表現した。本書はその連鎖をもう一段
先へ進める。すなわち、各価値が、プロトタイプで何になり、現在どの画面で動いているか
を示す。

出典：

| | |
| --- | --- |
| 5つの価値と、その根拠となるインタビュー | [What's Co-Creation DAO App](https://hopin-inc.notion.site/What-s-Co-Creation-DAO-App-1c030b95d2b68016be45e448154a50ab) |
| Value-to-Interface Mapping | [Additional Document M3](https://hopin-inc.notion.site/Additional-Document-M3-21130b95d2b68092aae4de53b3e5147d) |
| プロトタイプ | [Figma](https://www.figma.com/design/TkZ3wAG6zj114b4N6ogJyf/Co-Creation-DAO-App-UI--Catalyst-M3-) |

以下のパスは **https://dev.civicship.app/community/neo88** からの相対である。

## Milestone 3 の提出物と、Milestone 5 の提出物

Milestone 3 は設計を提出した。Milestone 5 は、その設計がなったアプリケーションを
提出した。

| Milestone 3 | Milestone 5 |
| --- | --- |
| Figma の UI/UX デザインプロトタイプ | フロントエンド本体 — [ソース](https://github.com/Co-Creation-DAO/civicship-portal-20260908)、[ドキュメント](./frontend-documentation.md)、[稼働中のデプロイ](https://civicship.app/community/neo88) |
| デザインウォークスルー動画：プロトタイプの解説、2プレイリスト | [ユースケース録画](./demo/)：稼働中のアプリケーション、同じ2セット |
| 再設計の要件とアクションプラン | 本書 — 各価値と、それを担う画面 |

録画はこの区分を保っている。[`milestone3-use-cases/`](./demo/milestone3-use-cases/)
は Milestone 3 でデモンストレーションした11件を現在のアプリケーションで撮り直した
もの、[`beyond-milestone3/`](./demo/beyond-milestone3/) はそれを超える10件である。
本書も同じ読み方をする。1〜6節がプロトタイプで定めたもの、その後の2節が後の
マイルストーンに送ったものと、それを超えて構築したものである。

## 1. 地域の人・活動・資源の可視化

| | |
| --- | --- |
| プロトタイプ | 地域ごとの活動拠点とその状況を示すマップ／ホスト視点のマイページ（開催中の活動と募集状況）／マップのマーカーから募集へ直接到達 |
| 現在 | `/places`、`/places/[id]`、`/users/me`、`/users/[id]`、`/admin/places`、`/admin/places/new` |

Milestone 3 の文書にある関連アプローチ「関わりをポートフォリオのように残す」は
`/users/me/portfolios` で動作している。

## 2. 金銭ではない価値の交換

| | |
| --- | --- |
| プロトタイプ | 招待チケットのインターフェース（活動後にホストが選んだ参加者へ発行）／トークンは労働の対価ではなく、今後の意思表示として扱う |
| 現在 | `/tickets`、`/tickets/receive`、`/admin/tickets`、`/admin/tickets/utilities`、`/wallets/me`、`/wallets/donate`、`/transactions`、`/admin/wallet/issue`、`/admin/wallet/grant` |

## 3. 段階的に築く関係

| | |
| --- | --- |
| プロトタイプ | コンテンツ種別を Activity と Quest の2つに分ける |
| 現在 | `/opportunities`、`/opportunities/search`、`/opportunities/[id]`、`/reservation/select-date`、`/reservation/confirm`、`/reservation/complete`、`/participations/[id]` |

2つの種別は、別々の一覧ではなく1つの一覧に対するフィルタとして実装している。
`/activities` と `/quests` はそれぞれ `/opportunities/search?type=activity`、
`?type=quest` へリダイレクトする。Value-to-Interface Mapping にある
"flexible filtering based on type, location, and time" に対応する。

## 4. 空気感を伝えるインターフェース

| | |
| --- | --- |
| 記載されたアプローチ | インタビュー記事を活動と並べて配置する／活動の写真は参加した本人がアップロードする／テキストではなく写真とマップを主体としたインターフェース |
| 現在 | 案内人のインタビューは、その人が主催する募集の詳細に表示される（[`HostInfoSection.tsx`](../../../src/app/community/%5BcommunityId%5D/opportunities/%5Bid%5D/components/OpportunityContent/HostInfoSection.tsx) が案内人の名前の横に描画する）。拠点は関連記事を `/places/[id]` に持つ。いずれも `/articles/[id]` で開く。活動の写真は、参加した本人がポイント送付に添えてアップロードする。`/wallets/donate` と `/admin/wallet/grant` はいずれも [`TransferInputStep.tsx`](../../../src/app/community/%5BcommunityId%5D/admin/wallet/grant/components/TransferInputStep.tsx) を通して受け取り、`/transactions/[id]` で後から編集できる。 |

## 5. 次の体験につながる体験

| | |
| --- | --- |
| 記載されたアプローチ | 設計ではなく例示 — 招待リンクの共有による複数人での申込、同日開催の周辺イベントのレコメンド、「等」 |
| 現在 | 案内人は枚数を指定して招待を発行し、`/admin/tickets/[id]` から QR コードまたはコピーしたリンクで共有する。受け取った人はそれぞれ `/tickets/receive` で自分のぶんを受け取る。申込は複数人ぶんをまとめて行える。`/reservation/select-date` で人数を選び、`/reservation/confirm` で人数ぶんのチケットまたはポイントを充当する。募集の検索と絞り込みは `/opportunities/search` と `/search/result`。 |

## 6. スキルと経験を活かせる機会

| | |
| --- | --- |
| プロトタイプ | 関心や必要に応じて Activity と Quest を探せる検索インターフェース。スキルタグによるレコメンドは将来対応と記載 |
| 現在 | Quest は、参加者が受け取る側ではなく貢献する側に立つときの募集の形である。`/opportunities/search?type=quest` が一覧を出し、Activity が参加費・ポイント消費・チケット利用を示すのに対し、Quest は参加者が獲得するポイント数を示す。分岐は [`displayPointsOrFee.tsx`](../../../src/utils/opportunity/displayPointsOrFee.tsx) にある。 |

## 後のマイルストーンに送ったもの

| Milestone 3 の記載 | 現在 |
| --- | --- |
| "(Future scope) Skill-tagged recommendations" | 未実装。 |

## Milestone 3 を超えて構築したもの

住民証 NFT は、Milestone 3 のインタビュー記録には既に現れている。参加者の価値2に "Through NFT or token ownership, even remote individuals can participate in the local economy" として記録されているが、プロトタイプが扱ったインターフェースには含まれていなかった。

| 領域 | 画面 |
| --- | --- |
| DAO 投票 | `/votes`、`/votes/[topicId]`、`/admin/votes` |
| 参加証明（VC） | `/credentials/[id]`、`/admin/credentials`、`/admin/credentials/issue` |
| 住民証 NFT | `/nfts/[id]`、`/admin/nfts` |
| 特典 | `/admin/bonuses`、`/admin/bonuses/signup` |
| 分析 | `/admin/analytics` |
| システム管理 | `/sysAdmin` 以下 |
