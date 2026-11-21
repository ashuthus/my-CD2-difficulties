# Red Alert Protocol Manual

> This manual is based on Red Alert Protocol v4.4.

独自仕様が増えすぎたので、自分用にもマニュアルを作成。  
とりあえずAIに丸投げしたので、細かい所はそのうち修正予定。

このマニュアルは、作者がRed Alert Protocol (以下RAP)を使用して公開ロビーをホストする際の環境と仕様をまとめたものです。  
RAP本体の設定に加え、ホスト側で併用しているMODによる変更も含まれます。  
そのため、記載内容のすべてがRAP単体の仕様とは限りません。

また、単純な仕様の確認だけでなく、Changelogでは残しにくい各変更の実装理由や設計意図、調整時のメモなども必要に応じて記載しています。

- [Overview](#overview)
  - [想定難易度](#想定難易度)
- [General Gameplay](#general-gameplay)
  - [Alert Swarms](#alert-swarms)
  - [Normal Waves](#normal-waves)
  - [Enemy Pools](#enemy-pools)
  - [Stationary Enemy Pools](#stationary-enemy-pools)
  - [Extraction](#extraction)
- [Events](#events)
  - [RED ALERT](#red-alert)
    - [RED ALERT Variants](#red-alert-variants)
  - [Gold Risk](#gold-risk)
    - [Gold Threshold](#gold-threshold)
    - [Progress](#progress)
    - [100% Event](#100-event)
- [Enemies](#enemies)
  - [Enemy Pool](#enemy-pool)
  - [Stationary Enemies](#stationary-enemies)
  - [Custom Enemies](#custom-enemies)
  - [Enemy Promotion](#enemy-promotion)
  - [Enemy Groups](#enemy-groups)
  - [Enemy List](#enemy-list)
  - [Enemy Balance Adjustments](#enemy-balance-adjustments)
    - [Spawn Count](#spawn-count)
    - [Temperature](#temperature)
    - [Fear / Courage](#fear--courage)
    - [Other Adjustments](#other-adjustments)
- [Missions](#missions)
  - [ミッション共通](#ミッション共通)
    - [脱出フェーズ](#脱出フェーズ)
  - [Mining Expedition](#mining-expedition)
  - [Egg Hunt](#egg-hunt)
    - [Non-Swarm Egg Ambush](#non-swarm-egg-ambush)
  - [On-site Refining](#on-site-refining)
  - [Salvage Operation](#salvage-operation)
    - [Mini-Mules](#mini-mules)
    - [Uplink / Refuel](#uplink--refuel)
    - [Salvage Extraction](#salvage-extraction)
  - [Point Extraction](#point-extraction)
  - [Escort Duty](#escort-duty)
  - [Elimination](#elimination)
    - [Dread Helper](#dread-helper)
    - [Dreadnoughts](#dreadnoughts)
  - [Industrial Sabotage](#industrial-sabotage)
    - [Sabotage Stationary Enemies](#sabotage-stationary-enemies)
  - [Deep Scan](#deep-scan)
  - [Heavy Extraction](#heavy-extraction)
- [Miscellaneous](#miscellaneous)
  - [Space Rig Tips](#space-rig-tips)
  - [Mission Start Notifications](#mission-start-notifications)
  - [Sound Cues](#sound-cues)
- [Appendix](#appendix)
  - [Modifiers](#modifiers)
  - [Host Mods](#host-mods)
  - [Recommended Client Mods](#recommended-client-mods)
  - [Afterword](#afterword)

## Overview

Red Alert Protocolは、Hazard 5のゲームテンポと基本的なプレイ感をベースに、  
バニラの体験を大きく崩さない範囲で調整したカスタム難易度です。

単純に常時大量の敵を出現させるのではなく、  
Alert Swarmを中心に明確な難所を作り、  
それ以外の時間帯では探索やミッション進行の余裕を確保するよう調整されています。

敵数の増加だけでなく、独自の敵やEliteバリエーション、  
RED ALERTやGold Riskなどのイベント、  
ミッション固有のゲームプレイ変更が追加されています。

敵集団の中には通常より大きな影響を与える敵が混ざるため、  
単純な殲滅力だけでなく、敵の優先処理、状況判断、Nitra管理が重要になります。

### 想定難易度

基本的にはT1相当 (Haz5x2, Haz6, etc.)の難易度を想定していますが、  
ミッション、イベント、洞窟構成、併用するMODなどによっては  
T2相当 (Haz5a, Haz6x2, etc.)の難易度になる場合があります。

洞窟生成パターンによっては、同じミッションでも難易度が大きく変動します。

Hazard 5+のMore Enemiesによって敵数を段階的に変更できるよう調整されており、  
各Modifier Levelのおおよその敵数目標は以下の通りです。

| More Enemies | Enemy Count Target |
| ------------ | ------------------ |
| ME0          | Haz5 x1.5程度      |
| ME1          | Haz6 x1.5程度      |
| ME2          | Haz5.5 x2程度      |

ME0 / ME1 / ME2では単純に同じ設定へ倍率を掛けるのではなく、  
各Modifier Levelに合わせてEnemy Countが調整されています。

そのため、More Enemiesを変更することで、  
RAPの基本的なゲームデザインを維持しながら敵数を調整できます。

その他Modifierについては [Modifiers](#modifiers) 参照。

___

## General Gameplay

RAPでは、戦闘の難易度を常に一定にするのではなく、  
Alert Swarmを中心に戦闘強度の高低が生まれるよう調整されています。

通常時の敵圧を抑える一方、  
Alert SwarmやExtractionなど特定のタイミングでは敵圧が上昇します。

比較的余裕のある時間帯に探索、採掘、補給、移動を進め、  
大規模な戦闘に備えることが基本的なゲーム展開となります。

### Alert Swarms

Alert SwarmはRAPにおける主要な難所です。

Swarmの平均発生間隔はHazard 5と大きく変えず、  
敵数の増加によってSwarm中の戦闘強度を高めています。

また、Alert Swarmは低確率でRED ALERTへ昇格し、  
通常のSwarmに追加の増援が加わる場合があります。

そのため、Swarmの警告が発生したら、  
現在の弾薬、地形、味方の位置などを確認し、  
できるだけ早く戦闘準備を整えることが重要です。

RAPではAlert Swarmを主な難所としているため、  
Swarm以外の時間帯をどのように使うかも重要になります。

### Normal Waves

Alert Swarm以外に発生する通常Waveは、  
Hazard 5と比較して平均的な発生頻度と規模が抑えられています。

| Parameter                    | Hazard 5 |  RAP |
| ---------------------------- | -------: | ---: |
| Enemy Normal Wave Interval   |     161s | 211s |
| Enemy Normal Wave Difficulty |      400 |  270 |

これにより、Alert Swarm以外の時間帯では  
常に高い敵圧を受け続けるのではなく、  
探索やミッション進行を行うための時間が作られています。

ただし、Normal Waveには振れ幅があり、  
稀に短い間隔や大規模なWaveが発生する場合があります。

- 約10%で105秒前後の短い間隔  
- 約5%でDifficulty 600前後の大規模Wave

そのため、Alert Swarm以外が常に安全というわけではありません。

### Enemy Pools

RAPではEnemy Poolが拡張され、  
バニラとは異なる敵構成が出現します。

通常のEnemy PoolにはSentinelやCrawlerなどが追加され、  
さらに既存の敵から独自のEliteやCustom Enemyへ昇進する仕組みが導入されています。

敵の追加後も既存の敵の多様性を維持するため、  
Enemy Poolのサイズも拡張されています。

独自Eliteの多くは役割ごとのEnemy Groupによって出現頻度が制御されており、  
強力な敵が無制限に連続して出現するのではなく、  
通常の敵集団の中へ高優先度のターゲットが混ざるよう調整されています。

そのため、敵数だけを見るのではなく、  
現在どのような敵が出現しているかを確認して  
処理する敵の優先順位を判断することが重要です。

### Stationary Enemy Pools

洞窟生成時に配置されるStationary Enemyも調整されています。

RAPではStationary Difficultyの空ロールが廃止され、  
Stationary Enemy DiversityはHaz5標準の2–4から3–5へ増加し、  
Sproutが追加される場合はさらに4–6へ増加します。

平均DifficultyはEnemy Countの増加を考慮して調整されているため、  
単純にStationary Enemyを大量に増やすことを目的とした変更ではありません。

一方で、何も配置されない抽選結果がなくなり、  
一度に選ばれる敵の種類も増えているため、  
Stationary Enemyとの遭遇はバニラより安定して発生します。

Stationary Poolには、バニラには存在しない追加の敵やEliteも含まれています。

新しい洞窟へ進入する際は、  
後から出現する敵だけでなく、  
すでに洞窟内に配置されている敵を確認してから進むことが重要です。

### Extraction

メイン目標達成後のExtractionでは敵数が増加します。

通常のミッションではExtraction中のEnemy Countが増加するため、  
メイン目標を達成した後も戦闘強度が高くなります。

Point Extractionでは通常のExtractionとは異なる条件で、  
脱出カウントダウン中に専用のEnemy Count増加が適用されます。

また、Salvage Operationではさらに独自のExtractionスケーリングがあり、  
Drop Pod起動後から時間経過とともに敵数が増加します。  
Drop Podのドアが開く頃にはおよそ2倍となり、  
脱出が完了するまで増加し続けます。

そのため、メイン目標の完了をミッション終了と考えず、  
Drop Podへ帰還するための弾薬やNitraを残しておくことが重要です。

___

## Events

RAPでは、通常のミッション進行中に独自のイベントが発生することがあります。

イベントは単純に敵数を増加させるだけではなく、  
Swarmや資源採掘など、プレイヤーの行動やミッション進行に応じて発生します。

現在、以下の主要イベントが存在します。

- `RED ALERT`
- `Gold Risk`

### RED ALERT

Alert Swarmが発生した際、低確率で通常より危険な  
「RED ALERT」へ昇格することがあります。

RED ALERTの基本発生率は10%です。

通常のSwarmが発生するたびに次回の発生率が5%ずつ上昇し、  
最大20%まで増加します。

RED ALERTが発生すると、発生率は10%へリセットされます。

| 状態                       | 次回RED ALERT発生率 |
| -------------------------- | ------------------: |
| 初期状態 / RED ALERT発生後 |                 10% |
| 通常Swarm 1回後            |                 15% |
| 通常Swarm 2回以上後        |                 20% |

以下、想定確率や期待値など。

| Swarm数 / Mission | 1回以上遭遇する確率 | RED ALERT期待値 |  期待値ベースの頻度 |
| ----------------: | ------------------: | --------------: | ------------------: |
|          2 Swarms |               23.5% |         0.245回 | 約4.08 Missionに1回 |
|          3 Swarms |               38.8% |         0.426回 | 約2.35 Missionに1回 |

RED ALERTが発生すると専用の警告が表示され、  
通常のSwarmに加えて追加の敵が出現します。

追加Waveの規模は、元のSwarmのおよそ25%を目安としています。  
ソロでのSwarm処理に70-80%程度の弾薬消費を基準とし、  
追加Waveで必要な補給回数が増えない程度の数を意図。

#### RED ALERT Variants

RED ALERTには複数のバリエーションがあり、
発生した種類によって追加される敵の構成が変化します。

| Variant  | 内容                               |
| -------- | ---------------------------------- |
| Grunt    | Gruntを中心とした増援              |
| Mactera  | Macteraを中心とした増援            |
| Ranged   | 遠距離攻撃を行う敵を中心とした増援 |
| Exploder | Exploderを中心とした増援           |

通常のSwarmにこれらの増援が追加されるため、  
元のSwarm構成との組み合わせによって脅威が大きく変化します。

RED ALERTはRAPにおける主要な難所のひとつです。  
Swarm終了まで対応できる弾薬やNitraを確保し、  
追加の敵に対応できるよう準備しておくことが重要です。

> **Note:** 現在のRED ALERT Variantsは初期に試験的に実装された構成を継続して使用しています。  
> 今後、バリエーションの内容や構成を再設計する予定です。

### Gold Risk

Gold Riskは、ミッション中のGold採掘量に応じて進行するイベントです。

通常のGoldを採掘すると進捗が増加し、  
一定量に到達すると警告や追加の敵が発生します。

Compressed GoldはGold Riskの進行対象には含まれません。

> **Note:** 本来MODDED環境でのGold採掘はキック対象となるレベルの行為であるため、  
> その名残のペナルティ要素としてイベント実装。  
> 割とボーナスと認識しているプレイヤーが増えてきているため、テコ入れが必要かもしれません。

#### Gold Threshold

100%到達に必要なGold量はミッションによって異なります。

| Mission           | Gold | Note                          |
| ----------------- | ---: | ----------------------------- |
| Default           |  200 |                               |
| Salvage Operation |  300 | Mini Mule修理ボーナス分を含む |
| On-site Refining  |  350 | Loot Bug密集分を含む          |

#### Progress

Gold Riskの進捗に応じて、以下のイベントが発生します。

| Progress | Event                                          |
| -------: | ---------------------------------------------- |
|      50% | 警告メッセージ                                 |
|      75% | 警告メッセージ / Elite Ebonite Gruntの出現開始 |
|      90% | 警告メッセージ                                 |
|     100% | 最終イベント発生                               |

75%に到達すると、  
Elite Ebonite Gruntが定期的に出現するようになります。

この敵は通常のEbonite Gruntとは異なり、  
つるはし2回、またはプレイヤーが踏みつけることで倒すことができます。

Elite Ebonite Gruntを倒すと、Gold Risk進捗1%分に相当するGoldをドロップします。

#### 100% Event

Gold Riskが100%に到達すると最終イベントが発生し、  
Elite Glyphid Crassus Detonatorが出現します。

そのためGold Riskは、  
Goldを採掘するほど追加の脅威が増加していく仕組みとなっています。

また、100%に到達するとElite Ebonite Gruntは出現しなくなります。

Goldをどこまで採掘するかはプレイヤー側で選択できます。  
弾薬、Nitra、現在のミッション状況などを考慮し、  
イベントを進行させるか判断してください。

___

## Enemies

RAPではバニラの敵構成をベースに、独自の敵やEliteバリエーションを追加しています。

これらの敵は単純に耐久力が高いだけではなく、  
攻撃方法や行動、状態異常への耐性などが変更されている場合があります。

特に危険な敵は放置すると戦闘を大きく不利にするため、  
敵数だけでなく敵の構成を確認し、脅威度の高い敵から優先して対処してください。

独自Eliteの出現はグループごとのクールダウンによって制御されているため、  
常に大量の特殊敵が出現するのではなく、通常の敵集団に強敵が混ざる形を基本としています。

### Enemy Pool

通常のEnemy Poolには、バニラでは通常の敵構成に含まれない敵も追加されています。

RAPでは以下の敵が通常のEnemy Poolに追加されています。

- `Sentinel`
- `Crawler`

CD2上ではイベント由来の個体と区別するため、  
それぞれ `O-Sentinel`、`SARU` の名前で表示されます。

これらはイベント専用の敵ではなく、  
通常の敵構成の一部としてEncounterやWaveなどで出現する場合があります。

敵の追加によって既存の敵が極端に出現しにくくならないよう、  
Enemy Pool自体の最小サイズは8から10へ拡張されています。  
Disruptive Enemyはミッションごとに3種類が選択されます。

### Stationary Enemies

RAPでは、通常のStationary Enemyに加えて独自の敵やEliteバリエーションが追加されています。

- `Elite Cave Leech`
- `Sprout`
- `Elite Breeder` (Breederから昇進)

Stationary Poolには独自の敵やEliteも追加されており、  
通常とは異なるStationary Enemyが出現する場合があります。

Stationary Enemyの詳細については[Enemy List](#enemy-list)を参照してください。

### Custom Enemies

RAPでは、バニラには存在しない独自の敵やEliteバリエーションが追加されています。

独自敵は単純なステータス強化だけではなく、  
攻撃方法、行動、状態異常への耐性などが変更されている場合があります。

これらの多くは、通常の敵と区別しやすくするためEliteとして実装されています。  
敵の色を変更することも可能ですが、HOST側にしか反映されないため、  
Client側からも独自敵であることを判別できるEliteの外見を利用しています。

同じベースの敵に見えてもバニラとは対処方法が異なる場合があるため、  
敵の特徴を把握しておくことを推奨します。

> **Note:** Custom EnemyやEliteは、新しい遭遇や戦闘の変化を継続的に追加するため、段階的に実装しています。
> 特に強力なEliteについては、既存の敵構成や難易度への影響を確認しながら、追加するタイミングを検討しています。

### Enemy Promotion

RAPの独自Eliteの多くは、  
独立した敵として直接Enemy Poolから抽選されるのではなく、  
対応する通常敵から昇進することで出現します。

例えば、通常の敵として出現する対象が  
一定の条件を満たした場合に独自Eliteへ置き換えられます。

この仕組みにより、  
通常の敵構成を維持しながら、その中に低頻度で強力な敵が混ざるようになっています。

※一部の昇進はEnemy Groupによる制御を受けません。  
　例えばElite BreederはBreederから33%で昇進しますが、Enemy Groupには所属していません。

### Enemy Groups

独自Eliteの出現頻度を制御するため、  
RAPでは敵を役割ごとのグループに分けています。

主なグループは以下の通りです。

- `LST Disruptive`
  - 比較的大型で、存在しているだけで戦闘へ大きな影響を与える敵を扱うグループです。
- `HVT Disruptive`
  - プレイヤーの行動を直接妨害したり、短時間で大きな脅威となる敵を扱うグループです。
- `Melee Special`
  - 近距離で特殊な行動を行う敵を扱うグループです。
- `Ranged Special`
  - 遠距離から継続的に戦闘へ影響を与える敵を扱うグループです。

各グループには個別のクールダウンが設定されています。

独自Eliteが出現すると対応するグループのクールダウンが開始され、  
クールダウン中は同じグループから新しい独自Eliteが昇進しません。

クールダウンが利用可能になった際も、  
同じグループから昇進できる敵の数も制限されています。

これにより、複数の強力な敵が短時間に大量出現することを抑えつつ、  
敵集団の中へ継続的に高優先度ターゲットが混ざるよう調整されています。

以下は、各Enemy Groupの昇進条件が利用可能な場合の昇進確率です。  
実際の出現頻度はEnemy GroupのCooldownや同グループの敵の存在によって制限されます。

| Group          | Base Enemy        | Promotion             | Chance | Max Active |
| -------------- | ----------------- | --------------------- | -----: | ---------: |
| -              | Breeder           | Elite Breeder         |  33.0% |          1 |
| Ranged Special | Acid Spitter      | Acid Queen            |  10.0% |          1 |
| Ranged Special | Septic Spreader   | Elite Septic Spreader |  50.0% |          1 |
| HVT Disruptive | Stingtail         | Elite Stingtail       |  50.0% |          1 |
| HVT Disruptive | Stalker           | Elite Stalker         |  50.0% |          1 |
| HVT Disruptive | Patrol Bot        | Elite Patrol Bot      |  25.0% |          1 |
| LST Disruptive | Warden            | Elite Warden          |  50.0% |          1 |
| LST Disruptive | Goo Bomber        | Elite Frost Bomber    |  12.5% |          1 |
| LST Disruptive | Goo Bomber        | Elite Fire Bomber     |  12.5% |          1 |
| -              | Goo Bomber        | Mactera Fire Bomber   |  25.0% |          - |
| Melee Special  | Exploder          | Elite Exploder        |  10.0% |          2 |
| Melee Special  | Nayaka Trawler    | Elite Trawler         |  25.0% |          2 |
| Melee Special  | Q'ronar Youngling | Elite Youngling       |  25.0% |          2 |

※ Bomber系はBiomeによって昇進候補が変化するため、実際の昇進確率が表記と異なる場合があります。

### Enemy List

| Enemy                   | Category       | EHP (P4) | MS   | 主な特徴                                                               |
| ----------------------- | -------------- | -------: | :--- | ---------------------------------------------------------------------- |
| Elite Cave Leech        | Stationary     |      240 |      | 長射程、触手速度 -40%、無音                                            |
| Brood Nexus             | Stationary     |     2700 |      | DefaultはExploder・EscortはGruntを生成、Spawn間隔・死亡時Spawn数を調整 |
| Sprout                  | Stationary     |      800 |      | 高速Projectileを使用                                                   |
| Elite Breeder           | Stationary     |     2250 | x5   | Eggから複数の敵を生成 (ダウン人数に応じて減少)、死亡時Hatchlingを生成  |
| Sentinel                | Enemy Pool     |      675 |      | 通常Enemy Poolに追加、Praetorianと同程度の出現率                       |
| Crawler                 | Enemy Pool     |      336 |      | Spreaderと同じ温度閾値、Tri-Jawと同程度の出現率                        |
| Acid Queen              | Ranged Special |      600 |      | Poison耐性80%、出現時クモの巣の音                                      |
| Elite Septic Spreader   | Ranged Special |      480 | x2   | Snowballを発射、温度閾値 x2                                            |
| Elite Stingtail         | HVT Disruptive |      480 | x1.5 | 掴みCD短縮、Fear無効、温度閾値 x1.5                                    |
| Elite Stalker           | HVT Disruptive |      432 | x1.5 | 攻撃力 x0.75、Fear無効、Damage Threshold 40                            |
| Elite Patrol Bot        | HVT Disruptive |      324 |      | 通常弾を高速連射、体当たりなし、Hack不可、Caretaker戦では出現しない    |
| Elite Warden            | LST Disruptive |     1200 |      | バフ範囲・最大バフ対象数 x2、Stun/Fear無効、温度閾値 x1.5              |
| Mactera Fire Bomber     | -              |     1200 |      | Goo Bomberから昇進                                                     |
| Elite Frost Bomber      | LST Disruptive |     1200 |      | Goo Bomberから昇進 (Magma Coreを除く)、Snowballを射撃                  |
| Elite Fire Bomber       | LST Disruptive |     1200 |      | Goo Bomberから昇進 (Glacial Strataを除く)、Hiveguard Fire Mortarを射撃 |
| Elite Exploder          | Melee Special  |      108 | x2   | 爆発範囲 +40%、Stun/Fear無効、Exploder Infestationでは昇進しない       |
| Elite Trawler           | Melee Special  |      480 |      | より攻撃的、温度閾値 x2                                                |
| Elite Youngling         | Melee Special  |      300 |      | 転がり攻撃を優先、温度閾値 x1.5                                        |
| Elite Ebonite Grunt     | Gold Risk      |       77 |      | つるはし2回または踏みつけで撃破、Goldをドロップ                        |
| Elite Crassus Detonator | Gold Risk      |     6600 | x2   | 腐食・電気無効                                                         |
| Dread Helper            | -              |     5500 |      | Dreadnought戦で追加出現するBulk Detonator                              |

温度閾値や状態異常など。

| Enemy                 |  Burn | Douse | Cooling | Freeze | Unfreeze | Warming | Stun | Fear |
| --------------------- | ----: | ----: | ------: | -----: | -------: | ------: | ---- | ---- |
| Elite Septic Spreader |  70.0 |  10.0 |       6 |    100 |        0 |      12 | -    | -    |
| Elite Stingtail       | 112.5 |  60.0 |       7 |    150 |       45 |      10 | -    | 無効 |
| Elite Stalker         |  45.0 |   6.0 |       6 |    -75 |        0 |       6 | -    | 無効 |
| Elite Warden          |  75.0 |  37.5 |       6 |    105 |       45 |      12 | 無効 | 無効 |
| Elite Exploder        | 999.0 |   0.0 |     100 |   -999 |        0 |     100 | 無効 | 無効 |
| Elite Trawler         |  90.0 |   0.0 |      10 |    100 |        0 |      20 | -    | -    |
| Elite Youngling       | 150.0 | 105.0 |      10 |    180 |      135 |      15 | -    | -    |
| Elite Patrol Bot      | 125.0 |     - |      20 |    150 |       10 |      40 | -    | -    |
| Elite Frost Bomber    |  52.5 |   7.5 |      10 |    375 |        - |      60 | -    | -    |
| Elite Fire Bomber     |  52.5 |   7.5 |      10 |    250 |        - |      40 | -    | -    |
| Dreadnoughts          | 100.0 |  25.0 |      20 |      - |        - |       - | -    | -    |

Enemy Notes(オマケ):

- Elite Cave Leech
  - 目立つが鋭い角度から無音で捉えようとし、意外と死角や僅かな隙間から伸びてくる
  - 目立つため足元お留守になりがちでPitJawが脅威になることも
- Sprout
  - MOD環境の核を撃つSpitballerの代わりに起こしてはいけない枠として追加
- Brood Nexus
  - MOD環境では完全にいないものとして扱われるため、放置しないで欲しい枠としてExploderを沸かせている
- Acid Queen
  - シンプルな優先処理枠として追加
- Elite Septic Spreader
  - 防衛系のトラブルの起点枠として追加
  - Fire Bomberとの連携で稀に即死を決めている
- Elite Exploder
  - ドリラーのCCでついでに倒されるため、近づかれる前に意識的に処理してほしい枠として追加
- Elite Patrol Bot / Trawler / Youngling
  - ミッション/バイオーム/ミューテーション固有の不遇枠なので早めに実装した
  - 対処は簡単、放置するとそれなりに厄介
- Elite Frost / Fire Bomber
  - バイオームによる確率増減の味変も入れてみたかったので実装
  - Frostに関しては野良プレイヤーから唯一悪質であるとの評価を得た
- Elite Stalker
  - エリートのエフェクトがあるので多少早く動いても問題無いよね？という枠
  - 5倍の速度は完全に足止め/仕留めるための注意力が必要となるため1.5倍に留めた

### Enemy Balance Adjustments

独自敵の追加とは別に、Enemy Count補正や状態異常との相互作用を調整するため、  
一部の既存敵にもSpawn数、温度、耐性などの変更が適用されています。

#### Spawn Count

| Enemy      | 変更内容                                                              |
| ---------- | --------------------------------------------------------------------- |
| Swarmer    | `MaxSpawnCount`を100に制限                                            |
| Shredder   | `MaxSpawnCount`を20に制限                                             |
| Egg Spider | 1回のSpawn数を1体に固定                                               |
| Crawler    | 最大1体 (Coreから生成される個体)                                      |
| Crawler    | `MaxSpawnCount`をプレイヤー数に応じて2 / 2 / 3 / 4に変更 (通常湧個体) |
| Pit Jaw    | 最大1体、`SpawnAmountModifier`を0.5に変更                             |
| Scrab      | 1～20体、`SpawnAmountModifier`を0.5に変更                             |

これらは、Enemy Count ModifierやMore Enemiesによって  
特定の敵だけが想定以上に増加することを抑えるための調整です。

#### Temperature

以下は、現行の設定で変更されている通常敵の温度関連パラメータです。  
内部倍率が適用された後のゲーム内での実効値を表記しています。

| Enemy           | Freeze | Unfreeze | Warming | Burn | Douse | Cooling | 主な変更                                                                    |
| --------------- | -----: | -------: | ------: | ---: | ----: | ------: | --------------------------------------------------------------------------- |
| Swarmer系       |      8 |        - |       - |    - |       |         | 凍結しやすく変更 (Ice Glyphid Swarmer、Dreadnought Pheromone Swarmerを除く) |
| Goo Bomber      |    250 |        - |      40 |    - |       |         | 凍結しやすく、解凍を遅く変更                                                |
| Fire Bomber     |    250 |        - |      40 |    - |       |         | 凍結しやすく、解凍を遅く変更                                                |
| Frost Bomber    |    375 |        - |      60 |    - |       |         | 凍結しやすく、解凍を遅く変更                                                |
| Mactera Grabber |    150 |        - |       - |    - |       |         | 凍結しやすく変更                                                            |
| Menace          |    100 |       50 |      10 |    - |       |         | 凍結耐性を強化                                                              |
| Youngling       |     90 |       45 |     7.5 |   75 |    35 |     7.5 | 通常個体の温度閾値を25%低下                                                 |
| Patrol Bot      |    150 |       10 |       - |    - |       |         | 通常個体とCaretaker個体を凍結可能                                           |
| Shredder        |     75 |        - |      30 |    - |       |         | 凍結可能、自然解凍しない                                                    |
| Nemesis         |    300 |      150 |      30 |    - |       |         | 凍結しやすく変更                                                            |

独自Eliteの温度設定については、[Enemy List](#enemy-list)を参照。

#### Fear / Courage

一部の敵はFearによって過度に戦線から離脱しないよう、Courageを調整しています。

| Enemy Type                              | Vanilla | RAP |
| --------------------------------------- | ------: | --: |
| Grunt-type                              |     0.5 | 0.6 |
| Praetorian-type                         |     0.5 | 0.6 |
| Mactera Spawn / Tri-Jaw / Brundle       |     0.0 | 0.3 |
| Spreader / Stalker / Stingtail / Warden |     0.5 | 0.6 |
| Grabber / Bomber-type                   |     0.0 | 0.6 |

主に低～中程度のFear効果によって敵が頻繁に戦線離脱することを抑えるための調整です。

250%以上のFear Chanceを持つ強力なFear効果  
(Coil Gun、Aggressive Ventingなど) には基本的に影響しません。

#### Other Adjustments

- Brood Nexusが燃焼中に周囲へ与えるHeatの範囲を150から250へ増加
- Cave Leechの`MaxDropPlayerDuration`を2から10へ増加
- Hiveguard戦で出現するSentinelの`SpawnSpread`を1500から500へ減少
- Praetorian、Frost Praetorian、OppressorのPiercing耐性を削除
- Swarmer系の実体力を1/3に変更 (Dreadnought Pheromone Swarmerを除く)
- StalkerのAttack Damageをx0.75、Stagger Durationをx1、Stagger Immunityを2秒に変更

___

## Missions

ミッション固有の変更点など。

### ミッション共通

RAPでは、ミッションタイプや進行フェーズに応じて敵の出現やゲームプレイが変化します。

一部のミッションでは、バニラとは異なる固有の調整や追加イベントが適用されます。  
重要な変更があるミッションでは、ミッション開始時にチャットで簡単な通知が表示されます。

#### 脱出フェーズ

メイン目標達成後の脱出フェーズでは、通常より敵の数が増加します。

脱出中も戦闘が激しくなりやすいため、  
弾薬やNitraを使い切らず、帰還に必要な戦力を残しておくことを推奨します。

Point Extractionでは、脱出カウントダウン中に専用の調整が適用されます。

### Mining Expedition

Nothing, any ideas?

### Egg Hunt

#### Non-Swarm Egg Ambush

Swarmが発生しないEgg Ambushの敵数が増加します。  
増加量はプレイヤー人数に応じて変化します。

| Players | Enemy Count | ME0時の体感Grunt数 | ME1 | ME2 |
| ------: | ----------: | -----------------: | --: | --: |
|       1 |        x2.0 |                 30 |  36 |  45 |
|       2 |        x2.0 |                 32 |  38 |  48 |
|       3 |        x2.5 |                 54 |  65 |  81 |
|       4 |        x3.0 |                 79 |  95 | 118 |

通常のSwarmを発生させる卵には、この強化は適用されません。

### On-site Refining

破損したPipelineを修理している間の敵圧が軽減されています。 (バニラHaz5と同等程度)

### Salvage Operation

#### Mini-Mules

Mini-Muleの修理に必要なLegの数が、ミッションごとに2～5本からランダムに決定されます。  
Legのスキャン時間は2秒から1秒に短縮されています。  
Mini-Muleの修理時間はプレイヤー数によって変化します。

| Players | Repair Time |
| ------: | ----------: |
|       1 |         10s |
|       2 |         20s |
|       3 |         30s |
|       4 |         40s |

複数人で同時に修理すると大幅に高速化されます。

> **Note:** 毎回決まって3本のLegを集めるより、必要な数が変わった方が面白いと思ったのでランダム化しました。
>
> 必要数+1本だけ配置する案もありましたが、それでは配置数から必要数が分かってしまううえ、  
> すべて探す手間も増えるため、必要数に関係なく常に6本配置しています。

#### Uplink / Refuel

UplinkとFuel Cellは複数人で同時に操作することで、起動を高速化できます。  
防衛エリアから全員が離れた際のMission Controlの警告は無効化されています。

防衛フェーズ開始時にSentinel増援が出現し、  
防衛が継続している間は60秒間隔で再び出現します。  
これは過度に防御的な地形利用へ圧力を掛けるための追加要素です。

#### Salvage Extraction

防衛終了後のExtractionでは、Enemy Count Modifierが2/3から開始し、時間経過とともに増加します。  
Drop Podのドアが開く頃には約2倍となり、その後も脱出が完了するまで増加し続けます。  
Extraction開始直後の敵圧を抑える代わりに、脱出に時間を掛けるほど敵数が増加する仕組みとなっています。

### Point Extraction

ミッション序盤の敵圧が通常より抑えられています。  

Enemy Countは最初の2分間は通常の約2/3に抑えられ、  
その後徐々に増加し、約7分で通常のEnemy Countへ戻ります。

そのため序盤は探索やAquarq回収を進めやすくなっていますが、  
長時間滞在した場合は通常と同程度のEnemy Countへ戻ります。

脱出カウントダウン開始後は、他のミッションと同様にExtraction時の敵数増加が適用されます。

### Escort Duty

Drilldozerが大きな単発ダメージを受けた際のダメージ処理が変更されています。  
Drilldozerへの大ダメージ軽減の閾値を撤廃し、全てのダメージ軽減倍率を0.5から0.75へ変更しています。(75%ダメージ軽減)  
これはクライオ構成以外で回避が難しい、Stationary等からの即壊を防ぐことを目的としている。

### Elimination

#### Dread Helper

Dreadnoughtとの戦闘中、追加でDread HelperとしてBulk Detonatorが出現する場合があります。  
ミッション開始時に、Dread Helperの対象となるDreadnoughtの種類または組み合わせが選択されます。  
対象はDreadnought、Hiveguard、Twinsのいずれか1種類が選ばれやすく、  
2種類の組み合わせや全種類が選ばれる場合もあります。

| 対象となるDreadnoughtタイプ | 組み合わせ数 | 合計Weight | 抽選率 |
| --------------------------- | -----------: | ---------: | -----: |
| 1種類                       |            3 |         27 |  69.2% |
| 2種類                       |            3 |          9 |  23.1% |
| 全3種類                     |            1 |          3 |   7.7% |

対象となった戦闘ではDread Helperが1体まで出現します。  
Dread Helperの体力はP4で5500 HPです。  
倒された場合もDreadnought戦が続いていれば継続して再出現します。  
設定上の平均では、1戦あたり約46%の確率で対象となります。

2体構成のミッションでは、抽選された対象タイプが実際のDreadnought構成に含まれず、  
どちらの戦闘でもDread Helperが出現しない場合があります。(約23%)

それでも最も退屈なミッションであることに変わりありません。

#### Dreadnoughts

DreadnoughtはFire系ビルドでも状態異常を利用できるよう、温度とFire Resistanceを調整しています。

- Burn Temperature: 1000 → 100
- Douse Temperature: 100 → 25
- Cooling Rate: 30 → 20
- Vanillaと比較してFire Damageを30%多く受けるよう調整

これにより、Dreadnought戦でもIgniteを利用したFire系ビルドが機能しやすくなっています。

### Industrial Sabotage

Turretの出現数を通常の2/3に減らしています。

Hack-C防衛フェーズ中にPhase Bombが45秒間隔で発生します。

Sadly, its hard coded :(

#### Sabotage Stationary Enemies

HOSTのMODにより、Stationary Enemyがミッション中に出現する場合があります。

### Deep Scan

Drillevator進行中、プレイヤーが2人以上の場合は敵の移動速度が約30%増加します。  
Soloではこの移動速度増加は適用されません。

### Heavy Extraction

洞窟生成MODによって部屋の形状が変化しています。  
部屋の端や天井付近にレジナイトが生成されることがあるため、探索時は注意してください。

Sad to say, its untouchable :(

___

## Miscellaneous

難易度そのもののバランス調整以外にも、  
独自仕様を把握しやすくするための通知、サウンドなどを追加しています。

### Space Rig Tips

Space Rigでは、RAP専用のTipsが表示されます。

Tipsには独自イベント、敵、ミッション変更など、  
RAPをプレイする上で知っておきたい情報が含まれています。

すべての仕様を詳細に説明するものではなく、  
プレイ中に重要な仕様やヒントを簡単に確認するための補助情報として使用しています。

### Mission Start Notifications

一部のミッションでは、ミッション開始時にRAP固有の変更点がチャットへ表示されます。

バニラと同じ進め方では見落としやすい変更を、  
ミッション開始時に簡単に知らせることを目的としています。

| Mission             | Notification                                                                   |
| ------------------- | ------------------------------------------------------------------------------ |
| Egg Hunt            | Non-Swarm EggのAmbushが強化されていることを通知                                |
| Elimination         | Dreadnought戦で追加の脅威が出現する可能性を通知                                |
| Industrial Sabotage | Stationary Enemyが出現する可能性、Hack-C防衛中にPhase Bombが発生することを通知 |
| Salvage Operation   | Mini-Muleの必要Leg数と協力修理について通知                                     |

詳細な仕様については各Missionの項目を参照。

### Sound Cues

一部の状況や独自敵には追加のサウンドを設定しています。

- プレイヤーダウン時
- Acid Queen出現時
- Gold Risk 100%到達時
- Dread Helper出現時

___

## Appendix

### Modifiers

RAPはHazard 5+のModifiersに対応していますが、基本的にはMore Enemies (ME)による難易度調整を想定しています。

| Modifier                  | RAPでの扱い     | Note                                                                |
| ------------------------- | --------------- | ------------------------------------------------------------------- |
| More Enemies (ME)         | Primary         | ME0 / ME1 / ME2に応じてEnemy Countを調整                            |
| Aggressive Enemies (AE)   | Optional        | Haz5のEnemy Movement Speedを基準とし、Haz5+と同様に任意で使用可能   |
| Player Vulnerability (PV) | Not Recommended | 被ダメージ倍率が高く、多くの攻撃で一撃ダウンが発生しやすい          |
| Tough Enemies (TE)        | Not Recommended | Gruntなど通常HPスケールの敵にも適用され、Breakpointが大きく変化する |

RAPはHazard 5のEnemy Movement Speedを基準としており、標準では追加の速度補正を行っていません。

高難易度のMODDED環境では、敵数が多く湧き間隔も短いため、それに合わせた速いペース配分が必要になります。  
RAPではそのようなプレイをPublic Lobbyの標準として要求せず、Hazard 5に近い移動感覚を維持しています。

また、ベースの移動速度をHazard 5のまま維持することで、  
Hazard 5+に慣れているプレイヤーは普段使用しているModifier構成のままプレイできます。

そのため、Aggressive EnemiesはRAPでもOptional Modifierとして利用できる扱いとしています。

AEによるEnemy Movement Speedは一般的なMODDED難易度よりも速くなりますが、  
RAPではNitraの制約やミッション全体を通した速いペース配分を同じようには要求していません。

その分、接敵時には敵から距離を取り続けることが難しく、都度の戦闘を強く要求されます。  
常に速いペースで行動する難易度ではなく、通常時と戦闘時の強度差を大きくするModifierとして機能します。

PVとTEは基本的に推奨していませんが、利用できないわけではありません。  
PVは被ダメージ倍率が高く、多くの攻撃で一撃ダウンが発生しやすくなります。

TEによるHP増加はSpecialなどの高耐久敵に対しては問題ありませんが、Gruntなどの通常敵にも適用されます。  
RAPでは通常敵について標準のHPスケールを維持することを想定しているため、  
TEを使用すると通常敵に対する武器やOverclockのBreakpointが大きく変化します。

これらはRAPの標準的なバランスからは外れますが、  
MODDED環境のような速いペース配分を要求するのではなく、  
バニラに近いゲームテンポのまま、  
よりピーキーな難易度でプレイしたい場合の選択肢として利用できます。

### Host Mods

RAP本体の実行には、ホスト側でCustom Difficulty v2 Update 18以降が必要です。  
また、Stationary EnemyにSproutを使用しているため、現在の設定ではMEVも必要です。  
Sproutを使用しない場合は、該当Descriptorを設定から除外することでMEVなしでも利用できます。

基本的に参加者側は、CD2およびその他MODの導入は必要ありません。

RAP本体とは別に、公開ロビーでのゲームプレイや利便性を調整するため、  
HOST側でいくつかのMODを導入しています。

これらはRAPの設定そのものには含まれませんが、  
一部はミッション構成やゲームプレイに影響します。

以下、HOSTの参考例。

- Required
  - custom-difficulty2-udpate-18
  - MEVv5_4 (Sproutを使用しない場合は不要)
- Gameplay
  - Chat Command: /resup (クライアント側がMODを入れずにカスタムコストの補給を呼び出せる、RAPでは不要)
  - Revert Resupply Stacking (補給重ね置き)
  - No Swarmer Swarms (特殊Swarmから難易度を下げがちなSwarmerを除外)
  - Iron Will Launch Override (鉄の意志を無視してDrop Podが出発する)
- Mission
  - Von's Cavegen Expansion (more cave layouts)
  - SabotagewithStationaries (Sabotageに通常のStationaryを追加)
- Weapon
  - Auto Build Sentry (Sentry自動組立、EM Discharge等のOCのQoL用)
- QoL
  - Client Impact Axe Fix (クライアント側も地面に刺さるようになる)
  - CheckResup (補給可否通知)
  - Anti-Carve (Exploding Plants, Exploder, Bulk, Resinite, Drillvatorなどによる地形破壊防止・抑制)
  - Additional chat notifications (MOTD, DownStats, Chat Command)
  - etc

### Recommended Client Mods

RAPをプレイするために、クライアント側MODを導入する必要はありません。

ただし、Custom Difficulty環境での情報表示を補助するものなど、  
導入しておくと便利なMODがあります。

以下のMODはすべて任意です。

- [Boss Health Bar](https://mod.io/g/drg/m/boss-health-bar)
  - Queen、Fire Bomberなど、RAPで追加される一部の敵のHPバーをClient側でも表示したい時に
  - Promoteによる湧きのため、MOD側の判定時のHPバー生成判定処理を飛ばしており、ホスト時でも2重に表示されることは無い (マップ生成時を除く)
- [Damage Meter / Friendlyfire Meter](https://mod.io/g/drg/m/damage-meter-friendlyfire-meter)
  - HostとClientの両方が導入している場合、同期されたデータを利用してClient側でもリアルタイムにダメージ状況を確認できる
- [New terrain scanner "MK4c"](https://mod.io/g/drg/m/mk4c)
  - Approvedではあるが、Rogue Coreから戻るとスキャナーの画質に耐えられないので推奨する

### Afterword

RAPは、普段からMODDED難易度を遊んでいた作者が、  
アジア圏のMODDEDホストやプレイヤーが減少してきたことをきっかけに、  
自分で遊ぶための難易度として作り始めました。  
特にRogue Coreの発売によって、  
今後さらにプレイヤーが減るかもしれないと考えたことが直接のきっかけの一つです。

固定メンバーではなくPublic Lobbyで遊ぶことを前提としており、  
バニラの中級プレイヤーからHazard 5+でAll Modifiersを有効にして遊ぶプレイヤーまで、  
幅広く参加できる難易度を目標としています。

また、普段はバニラを遊んでいるプレイヤーにも、  
敵数の増加やEnemy Poolの拡張、独自の敵やイベントといった  
MODDED環境ならではのゲームプレイを体験してもらうことも、この難易度の目的の一つです。

そのため、バニラからMODDEDへ移行しても極端に異なるゲームにならないよう、  
Hazard 5の基本的なゲーム感覚を残すことを重視しています。

常に大量の敵を出し続けるのではなく、  
平時はHazard 5に近いペースを維持し、  
Swarmやイベント時に敵数と脅威が大きく増加する設計にしています。  
戦闘の合間に探索や採掘ができるDRG特有のチルい時間帯を残しつつ、  
戦闘が始まればMODDEDらしい規模のSwarmを楽しめることを意図しています。

また、難易度を上げるために、単純に敵の性能を高くすることも避けています。  
特にEliteは耐久力を上げすぎると有効なOverclockやBuildが限られてしまうため、  
基本的にベースとなる通常個体のバニラ相当～2倍程度の範囲に収めています。

一方で、敵数やEnemy Poolを増やすだけではバニラとは異なる問題も発生します。  
MODDED環境ではCryoを中心とした構成が相対的に扱いづらく、  
Disruptive Enemyを単純に増やすだけでも弾薬消費が大きくなります。  
そのため、敵の追加や出現数だけでなく、  
一部の敵ではTemperatureにも調整を加えています。

FearやPheromoneのような強力なCrowd Controlについては、  
使用しない環境にできれば調整は容易ですが、  
Public LobbyでプレイヤーのBuildを完全に制限することは現実的ではありません。  
そのため使用自体を禁止するのではなく、  
一部の敵の耐性を少し強化することで対応しています。
