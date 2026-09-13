<a id="en"></a>

# From the Milestone 3 Prototype to the Application Today

*English below · [日本語は下段へ](#ja)*


Project Catalyst F12, Project ID 1200088.

Milestone 3 gathered user feedback through interviews, distilled it into five
values, and expressed those values as a Figma prototype. This document carries
that chain one step further: from each value, to what the prototype made of it,
to the screen that runs it today.

Sources:

| | |
| --- | --- |
| The five values, with the interview evidence behind each | [What's Co-Creation DAO App](https://hopin-inc.notion.site/What-s-Co-Creation-DAO-App-1c030b95d2b68016be45e448154a50ab) |
| Value-to-Interface Mapping | [Additional Document M3](https://hopin-inc.notion.site/Additional-Document-M3-21130b95d2b68092aae4de53b3e5147d) |
| The prototype | [Figma](https://www.figma.com/design/TkZ3wAG6zj114b4N6ogJyf/Co-Creation-DAO-App-UI--Catalyst-M3-) |

Paths below are relative to **https://dev.civicship.app/community/neo88**, the
development deployment, which signs a visitor in automatically with an owner
membership — no LINE account, no personal information, and every administrative
screen reachable.

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

Not part of the Value-to-Interface Mapping; the approach is stated in the
Milestone 3 document itself.

| | |
| --- | --- |
| Stated approach | Interview articles placed alongside the activities; activity photographs uploaded by the people who took part; an interface led by photographs and a map rather than by text |
| Today | A host's interview appears on the opportunity they run — [`HostInfoSection.tsx`](../../../src/app/community/%5BcommunityId%5D/opportunities/%5Bid%5D/components/OpportunityContent/HostInfoSection.tsx) renders it beside the host's name — and a place carries its related articles at `/places/[id]`. Either opens at `/articles/[id]`. |

The article index at `/articles` exists but carries no navigation entry, so an
article is reached through the activity or place it belongs to rather than from a
list.

## 5. Experience that leads to further experience

| | |
| --- | --- |
| Stated approach | Group application through a shared invitation link; recommendation of nearby events held on the same day |
| Today | Partly. An invitation is received at `/tickets/receive`, and activities are searched and filtered at `/opportunities/search` and `/search/result` |

**Not built:** group application through a shared invitation link, and
same-day nearby-event recommendation.

## 6. Opportunities to apply skills and experience

This value appears in the Value-to-Interface Mapping under *Participant*. It does
not fold into the five above, which follow the main document's framing.

| | |
| --- | --- |
| Prototype | A search interface to browse activities and quests by interest or need; skill-tagged recommendations noted as future scope |
| Today | A Quest is the form an opportunity takes when the participant contributes rather than receives. `/opportunities/search?type=quest` lists them, and a quest states the points the participant will earn where an activity states a fee, a point cost or a ticket — [`displayPointsOrFee.tsx`](../../../src/utils/opportunity/displayPointsOrFee.tsx) is where the two diverge. |

## Carried forward from Milestone 3

| Milestone 3 | Today |
| --- | --- |
| "(Future scope) Skill-tagged recommendations" | Not built. Article recommendations exist, but they recommend articles rather than matching activities to a participant's skills. |

## Built since, beyond the mapping

Areas of the application that postdate the Value-to-Interface Mapping.

| Area | Screens |
| --- | --- |
| DAO voting | `/votes`, `/votes/[topicId]`, `/admin/votes` |
| Verifiable credentials | `/credentials/[id]`, `/admin/credentials`, `/admin/credentials/issue` |
| Resident-card NFTs | `/nfts/[id]`, `/admin/nfts` |
| Member bonuses | `/admin/bonuses`, `/admin/bonuses/signup` |
| Analytics | `/admin/analytics` |
| System administration | under `/sysAdmin` |

The application has 79 pages in total. Screen recordings of twenty-one use cases
are in [`demo/`](./demo/).

---
---

<a id="ja"></a>

# Milestone 3 のプロトタイプから、現在のアプリケーションまで

*[English is above](#en)*

Project Catalyst F12、Project ID 1200088。

Milestone 3 では、インタビューを通じて利用者のフィードバックを収集し、それを5つの
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
開発環境は訪問者をオーナー権限で自動的にサインインさせるため、LINE アカウントも
個人情報も要らず、管理画面にもすべて到達できる。

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

Value-to-Interface Mapping には含まれない。アプローチは Milestone 3 の文書本文に
記載されている。

| | |
| --- | --- |
| 記載されたアプローチ | インタビュー記事を活動と並べて配置する／活動の写真は参加した本人がアップロードする／テキストではなく写真とマップを主体としたインターフェース |
| 現在 | 案内人のインタビューは、その人が主催する募集の詳細に表示される（[`HostInfoSection.tsx`](../../../src/app/community/%5BcommunityId%5D/opportunities/%5Bid%5D/components/OpportunityContent/HostInfoSection.tsx) が案内人の名前の横に描画する）。拠点は関連記事を `/places/[id]` に持つ。いずれも `/articles/[id]` で開く。 |

記事の一覧 `/articles` は存在するが、ナビゲーションからの導線を持たない。記事は
一覧からではなく、その記事が属する活動や拠点から到達する。

## 5. 次の体験につながる体験

| | |
| --- | --- |
| 記載されたアプローチ | 招待リンクの共有による複数人での申込／同日開催の周辺イベントのレコメンド |
| 現在 | 部分的。招待の受け取りは `/tickets/receive`、募集の検索と絞り込みは `/opportunities/search` と `/search/result` |

**未実装：** 招待リンクの共有による複数人での申込、および同日開催イベントの
レコメンド。

## 6. スキルと経験を活かせる機会

この価値は Value-to-Interface Mapping の *Participant* 側にある。上の5つは本体文書の
枠組みに沿っており、この価値はそこに畳み込めない。

| | |
| --- | --- |
| プロトタイプ | 関心や必要に応じて Activity と Quest を探せる検索インターフェース。スキルタグによるレコメンドは将来対応と記載 |
| 現在 | Quest は、参加者が受け取る側ではなく貢献する側に立つときの募集の形である。`/opportunities/search?type=quest` が一覧を出し、Activity が参加費・ポイント消費・チケット利用を示すのに対し、Quest は参加者が獲得するポイント数を示す。分岐は [`displayPointsOrFee.tsx`](../../../src/utils/opportunity/displayPointsOrFee.tsx) にある。 |

## Milestone 3 で将来対応としたもの

| Milestone 3 の記載 | 現在 |
| --- | --- |
| "(Future scope) Skill-tagged recommendations" | 未実装。記事のレコメンドは存在するが、参加者のスキルに募集を合わせるものではない。 |

## Mapping 以降に構築したもの

Value-to-Interface Mapping より後に追加された領域。

| 領域 | 画面 |
| --- | --- |
| DAO 投票 | `/votes`、`/votes/[topicId]`、`/admin/votes` |
| 参加証明（VC） | `/credentials/[id]`、`/admin/credentials`、`/admin/credentials/issue` |
| 住民証 NFT | `/nfts/[id]`、`/admin/nfts` |
| 特典 | `/admin/bonuses`、`/admin/bonuses/signup` |
| 分析 | `/admin/analytics` |
| システム管理 | `/sysAdmin` 以下 |

アプリケーションの総ページ数は 79。21件のユースケースの画面録画は
[`demo/`](./demo/) にある。
