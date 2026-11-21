# Red Alert Protocol

> This doc is based on Red Alert Protocol v5.6.

## Table of Contents <!-- omit in toc -->

- [Concept](#concept)
- [公開ロビー向け](#公開ロビー向け)
- [What's New](#whats-new)
  - [v5 - Encounter Overhaul](#v5---encounter-overhaul)
  - [v4 - Combat Expansion](#v4---combat-expansion)
  - [v3 - Gameplay Expansion](#v3---gameplay-expansion)
  - [v2 - Events](#v2---events)
  - [v1 - Core Difficulty](#v1---core-difficulty)
- [想定敵数](#想定敵数)
- [Hazard 5との平均パラメータ比較](#hazard-5との平均パラメータ比較)
- [Changes](#changes)
  - [General Difficulty](#general-difficulty)
  - [Mission Events](#mission-events)
  - [Stationary Enemy Changes](#stationary-enemy-changes)
  - [Elite \& Custom Enemies](#elite--custom-enemies)
  - [Enemy Balance](#enemy-balance)
  - [Mission-specific Changes](#mission-specific-changes)
  - [Miscellaneous](#miscellaneous)
- [Current Changes](#current-changes)
- [Future Plans](#future-plans)

## Concept

Hazard 5のゲームテンポと基本的なプレイ感をベースに、  
バニラの体験を大きく崩さない範囲で調整した、野良ロビー向けの難易度。

基本的に難易度はT1を想定しているが、  
ミッション、イベント、洞窟構成、併用するMODなどの条件によっては、T2相当の難易度になる場合がある。  
(例: SabotageでのStationary Enemy追加やCustom Cave Layout)

Hazard 5+ More Enemiesで敵数を段階的に調整できるよう設計され、  
ME2ではHaz5.5x2ライクな敵密度を想定。

難易度のピークをAlert Swarmに集中させ、  
それ以外の時間帯は概ねバニラと同程度の圧力に抑えている。

敵数の増加に加え、敵の優先処理、状況判断、Nitra管理を重視。  
独自の敵、Eliteバリエーション、イベント、およびミッション固有のゲームプレイ調整を追加。

## 公開ロビー向け

- 公開ロビー向けにバランス調整
- クライアント側のMOD導入不要
- Alert Swarmが主な脅威
- 優先ターゲットの排除が重要
- ナイトラ80設定

## What's New

### v5 - Encounter Overhaul

- Egg Huntの調整  
  Swarmを伴わないEgg Ambushの敵数を、発生回数に応じて段階的に増加するよう調整
- RED ALERTのバリエーション拡張  
  Heavy Wave (マルチプレイ限定) とSwarmer Waveを追加し、遭遇パターンの多様性を向上
- RED ALERTの発生対象を拡張  
  Point ExtractionのSwarm、SalvageのUplink / Refuel防衛フェーズ、On-site Refiningの精製フェーズをRED ALERTの発生対象に追加
- Elite Halloween Skullが登場するハロウィーンイベントを追加

### v4 - Combat Expansion

- Stationary Enemyの拡張  
  新たなStationary Enemy VariantとしてElite BreederとSproutを追加。
- 新たなElite Enemy Variant  
  新たなElite Variantを追加し、昇進仕様を拡張。
- 敵バランスの改善  
  恐怖耐性を調整し、Dreadnoughtに対する炎構成の有効性を改善。
- Dreadnought戦の調整  
  Dread Helperの体力を減少し、Dreadnought戦のバランスを調整。
- ミッション個別調整  
  Industrial Sabotage、Salvage Extraction、Point Extraction、Deep Scanを調整。

### v3 - Gameplay Expansion

- 新たな敵を追加  
  Crawler、Elite Trawler、Elite Youngling、Elite Patrol Botを追加。
- Enemy Groupシステムの拡張  
  Melee Specialグループを追加し、新しいEliteに対応するためHVT Disruptiveグループを拡張。
- Enemy Poolの拡張  
  新たな敵の追加後も遭遇の多様性を維持するため、Enemy PoolとStationary Poolのサイズを拡張。
- ミッションイベントの改善  
  Dreadnought戦にBulk Detonatorイベント、Egg Waveにプレイヤー人数スケーリング、Hack-C中にPhase Bombを追加。
- 敵バランスの調整  
  Eliteや独自バリエーションを含む複数の敵を再調整し、スポーン数や温度設定を調整。

### v2 - Events

- RED ALERTとGold Riskイベントを導入。

### v1 - Core Difficulty

- Red Alert Protocolの基本難易度と敵数スケーリングを構築。

## 想定敵数

- ME0 : Haz5   x 1.5 程度
- ME1 : Haz6   x 1.5 程度
- ME2 : Haz5.5 x 2   程度

敵数は各Hazard 5+ Modifierレベル向けに調整されており、  
難易度の主な変化要因はModifier側となるよう設計されています。

## Hazard 5との平均パラメータ比較

- Enemy Count Modifier         : 1.113 -> 1.58 (ME1: 1.89 / ME2: 2.36)
- Encounter Difficulty         :   337 -> 240
- Stationary Difficulty        :   158 -> 168  *1
- Enemy Wave Interval (Alert)  :  240s -> 241s
- Enemy Normal Wave Interval   :  161s -> 211s *2
- Enemy Normal Wave Difficulty :   400 -> 270  *2

*1 Stationary Enemyはより安定して出現するよう調整。  
   敵が配置されない抽選結果を廃止し、Enemy Count補正を考慮した  
   総合的な難易度はHazard 5に近い水準を維持。

*2 通常Waveは平均的に大幅削減されているため、  
   戦闘の主な難所はAlert Swarmとなる。

ただし稀に強力な通常Waveが発生する:

- 10%で約105秒間隔
- 5%でDifficulty約600

Note:  
Aggressive Enemiesと組み合わせた場合、  
敵の速度補正がHazard 7相当を超える場合があります。

敵が極めて攻撃的になり、バランスを超えた挙動を見せる場合があります。

## Changes

### General Difficulty

- ME0 / ME1 / ME2のEnemyCountスケーリングを個別に調整 (Haz5x1.5 / Haz6x1.5 / Haz5.5x2相当)
- Swarm以外の敵の数と間隔を下方修正 (Encounter、Stationary、Enemy Normal Wave)
- MinPoolSizeを8から10に増加  
  (Enemy Poolへの敵追加後も敵の多様性を維持するため)
- Eliteのダメージ抵抗率をプレイヤー人数に応じて1.3 / 1.3 / 1.5 / 1.65に調整

### Mission Events

- Gold Riskシステムを追加
  - 一定量のゴールドを採掘するとイベントが発生 (Compressed Goldは対象外)
  - 進捗50%、75%、90%で警告メッセージを表示
  - イベント発生時に最終警告を表示
  - 進捗75%到達後、Elite Ebonite Glyphid GruntによるMini Waveが定期的に発生
    - 衝突判定を追加し、踏みつけで倒せるように変更 (クリボー風)
    - 倒すとGold Risk進捗1%分に相当するGoldをドロップ
  - 進捗100%到達時、Elite Glyphid Crassus Detonatorが出現
    - 常時アウトラインを追加
- RED ALERTシステムを追加
  - Alert Swarmは低確率でRED ALERTへ昇格する
  - RED ALERTの基本発生率は15%
  - 通常Swarmが発生するたびに発生率が5%上昇し、最大25%まで増加
  - RED ALERT発生時、発生率は0%にリセットされる
  - RED ALERT発生時は専用警告メッセージが表示される
  - RED ALERT中は通常のSwarmとは別に、元のSwarm規模の約50%に相当する追加Spawn Waveが発生する
    - RED ALERTバリエーション: Grunt、Mactera、Ranged、Exploder増援
  - RED ALERT発生時にSEを追加

### Stationary Enemy Changes

- Stationary Difficultyで空ロールを廃止  
  (Enemy Count補正込みの総難度は概ねHazard 5相当を維持しつつ、  
  平均難度を158→168へ増加)
- StationaryEnemyCountを4から5に増加 (Sproutが出現可能な場合は6)
- StationaryEnemyDiversityを 2–4 から 3–5 に増加 (Sproutが出現可能な場合は4–6)
- Elite Cave Leechを追加  
  (触手速度40%低下、実HP25%増加、P4で240EHP、無音)
- Brood Nexusの調整
  - Brood NexusからGlyphid Spawn以外のクリーチャーも出現するように変更  
    (放置されがちなため)
  - 生成間隔を10秒から30秒に変更
  - 死亡時のSpawn数を15から10に変更
- Cave LeechのMaxDropPlayerDurationを2から10に増加
- SproutをBarrage Infectorと同程度の出現率でStationary Poolに追加  
  (Projectileの弾速を上昇、威力は通常のSproutと同等)
- Elite Breederを追加
  - 昇格率33%、Enemy Groupには所属しない
  - 移動速度5倍、P4で実体力2,250
  - Eggから通常のHatchlingの代わりに4体の敵が出現
  - ダウン中のドワーフ数に応じてEgg数とEggごとの出現敵数が減少
  - 死亡時にHatchlingが出現

### Elite & Custom Enemies

- SentinelをEnemy PoolにPraetorianと同程度の出現率で追加
- CrawlerをEnemy PoolにTri-Jawと同程度の出現率で追加
  - 温度閾値: Spreaderと同じ (発火35、凍結-50)
  - MaxSpawnCount: 2/2/3/4 (プレイヤー人数別)
- カスタムEnemyグループ (LST Disruptive、HVT Disruptive、Melee Special、Ranged Special) を追加
  - 敵の出現頻度を制御するため、グループ毎のクールダウンを設定
- Acid Queenを Ranged Special Enemy Group に追加
  - DamageMultiplier 5、実体力は600
  - Poison Damage耐性を80%に変更  
    (自身の範囲攻撃でHPが半分以下になりにくくなるよう調整)
  - Acid Spitterから10%の確率で昇進するよう変更
- Elite Snowball Spreader を Ranged Special Enemy Group に追加  
  (Red Sepsisの代わりに雪玉を発射、P4で480EHP、温度閾値2倍)
- Elite Stingtail を HVT Disruptive Enemy Group に追加  
  (掴みクールダウン短縮、恐怖無効、P4で480EHP、温度閾値1.5倍)
- Elite Warden を LST Disruptive Enemy Group に追加  
  (バフ範囲・バフ対象数2倍、スタン・恐怖無効、P4で1200EHP、温度閾値1.5倍)
- Mactera Fire Bomberを追加  
  (Mactera Goo Bomberからのみ昇進)
- Elite Trawler を Melee Special Enemy Group に追加  
  (P4で480EHP、温度閾値2倍、よりアグレッシブな行動)
- Elite Youngling を Melee Special Enemy Group に追加  
  (P4で300EHP、温度閾値1.5倍、転がり攻撃を優先)
- Elite Patrol Bot を HVT Disruptive Enemy Group に追加  
  (P4で324EHP、炎温度閾値0.5倍・氷温度閾値0.4倍、  
   通常弾を高速連射、体当たり攻撃なし、ハッキング不可)
- Elite Frost BomberをLST Disruptive Enemy Groupに追加
  - Mactera Goo Bomberから昇進 (Magma Coreを除く)
  - P4で1200 EHP、Burn Temperature 52.5、Douse Temperature 7.5、Freeze Temperature 375、Warming Rate 60
  - Snowballを射撃
- Elite Fire BomberをLST Disruptive Enemy Groupに追加
  - Mactera Goo Bomberから昇進 (Glacial Strataを除く)
  - P4で1200 EHP、Burn Temperature 52.5、Douse Temperature 7.5、Freeze Temperature 250、Warming Rate 40
  - HiveguardのFire Mortarを射撃 (各弾はSprout相当のダメージ)
- Elite SwarmerをMelee Special Enemy Groupに追加
  - P4で実体力108、移動速度5倍、攻撃力2倍
  - Fear無効、IgniteまたはFreezeで即死しない
  - Burn Temperature 6、Douse Temperature 2、Freeze Temperature -6、Unfreeze Temperature 0、Cooling Rate 6、Warming Rate 6
- Elite ExploderをMelee Special Enemy Groupに追加
  - P4で実体力108、移動速度2倍、爆発範囲40%増加
  - 恐怖とスタン無効、Exploder Infestation Variantからは昇進しない
  - Burn Temperature 999、Douse Temperature 0、Freeze Temperature -999、Unfreeze Temperature 0、Cooling Rate 100、Warming Rate 100
- Elite StalkerをHVT Disruptive Enemy Groupに追加
  - P4で実体力432、移動速度1.5倍、攻撃力0.75倍
  - 恐怖無効、スタン時間x1、再スタン耐性2秒
  - Damage Thresholdを通常種の80から40に減少
  - Burn Temperature 45、Freeze Temperature -75
- Elite Fireball SpreaderをRanged Special Enemy Groupに追加
  - Magma CoreでのみSeptic Spreaderから昇進
  - P4で実体力480、移動速度2倍、攻撃力0.6倍
  - HiveguardのFire Mortarを射撃
  - Burn Temperature 70、Douse Temperature 10、Freeze Temperature -100、Unfreeze Temperature 0、Cooling Rate 6、Warming Rate 12

### Enemy Balance

- バニライベント用Crawlerのスポーン数を調整 (MinSpawnCount 1 -> 0、MaxSpawnCount 9999 -> 1)
- Scrabのスポーン数を調整 (MinSpawnCount 4 -> 1、MaxSpawnCount 9999 -> 20、SpawnAmountModifier 1 -> 0.5)
- Pit Jawのスポーン数を調整 (MinSpawnCount 1 -> 0、MaxSpawnCount 9999 -> 1、SpawnAmountModifier 1 -> 0.5)
- SwarmerのMaxSpawnCountを100に制限
- ShredderのMaxSpawnCountを20に制限
- Egg SpiderのSpawn数を1に制限
- Goo Bomberの凍結耐性を低下 (FreezeTemperature 320 -> 250、WarmingRate 50 -> 40)
- Fire Bomberの凍結耐性を低下 (FreezeTemperature 320 -> 250、WarmingRate 50 -> 40)
- Frost Bomberの凍結耐性を低下 (FreezeTemperature 560 -> 375、WarmingRate 75 -> 60)
- Younglingの温度閾値を25%低下 (FreezeTemperature 90、BurnTemperature 75)
- Menaceの凍結耐性を増加 (FreezeTemperature 50 -> 100、UnfreezeTemperature 0 -> 50、WarmingRate 6 -> 10)
- Patrol Botの凍結耐性を低下 (FreezeTemperature 375 -> 150、UnfreezeTemperature 10)
- Shredderの凍結耐性を低下 (FreezeTemperature 1250 -> 75、WarmingRate 20 -> 30)
- Nemesisの凍結耐性を低下 (FreezeTemperature 300、UnfreezeTemperature 150、WarmingRate 75 -> 30)
- Hiveguard戦のSentinelのSpawnSpreadを1500から500に減少
- Brood NexusのOnFireHeatRangeを150から250に増加 (from VEA)
- Praetorian (Frost含む)とOppressorのPiercing耐性を削除 (from VEA)
- Swarmer系のバランス調整 (Dreadnought Pheromone Swarmerを除く)
  - 実体力を1/3に減少
  - Freeze Temperatureを8に変更 (Ice Glyphid Swarmerを除く)
- Stalker: 攻撃力x0.75、スタン時間x1、再スタン耐性2秒
- 恐怖のバランス調整
  - Grunt系のCourageを0.5から0.6に引き上げ
  - Praetorian系のCourageを0.5から0.6に引き上げ
  - Mactera Spawn、Tri-Jaw、BrundleのCourageを0から0.3に引き上げ
  - 特殊敵 (Spreader、Stalker、Stingtail、Warden、Grabber、Bomber系) のCourageを0.6に変更
  - Note: 250%以上の恐怖効果には影響しない (例: Coil Gun、Aggressive Venting)
- Dreadnoughtの温度・炎耐性調整
  - Burn Temperatureを1000から100、Douse Temperatureを100から25、Cooling Rateを30から20に変更
  - バニラの炎耐性を基準に、受ける炎ダメージを30%増加

### Mission-specific Changes

- ミッション全般
  - Extractionフェーズ中の敵数を増加 (Point Extractionの脱出カウントダウン中も含む)
- Egg Hunt
  - Swarmが発生しないEgg Ambushの敵数を増加  
    (プレイヤー人数に応じて x2.0 / x2.0 / x2.5 / x3.0)
- On-site Refining
  - Refineryでパイプが壊れた際の敵の数を減少
- Salvage Operation
  - Mini Muleの足スキャン時間を2秒から1秒に変更
  - 修理の秒数をByPlayerCountに応じて10秒から10 / 20 / 30 / 40 秒に変更
  - 修理に必要な足の数を2-5のランダムに設定
  - MiniMule/Uplink/Refuelの協力インタラクト倍率をx5に設定
  - SalvageのExtraction中、時間経過で敵数が増加
    - Enemy Count Modifierが2/3から時間経過で増加し、Drop Podのドアが開く頃に約2倍へ到達
    - 脱出完了まで敵数は増加し続ける
  - Uplink / Refuelの防衛フェーズ中にSentinel増援を追加 (過度に防御的な地形利用への対策)
- Point Extraction
  - Enemy Count Modifierのバニラ相当への軽減を序盤のみに変更
    - 最初の2分間は2/3を維持し、その後徐々に増加して約7分で1.0倍に戻る
- Escort Duty
  - Dorettaの大ダメージ判定のしきい値を削除
  - Dorettaの大ダメージ耐性を0.5から0.75に減少
- Elimination
  - Dread Helperを追加
    - Dreadnought戦中に追加の脅威として出現することがあるカスタムBulk Detonator
    - ミッション開始時にDread Helperの対象となるDreadnoughtタイプの組み合わせを抽選
    - 特殊湧きのDreadnoughtもDread Helperの対象
    - 結果として戦闘あたり平均約46%の確率でDread Helperが出現
    - Dread Helperの体力を11/12に減少 (P4で5500HP)
- Industrial Sabotage
  - Industrial SabotageのTurret出現数を2/3に削減
  - Hack-C防衛フェーズ中にPhase Bombが定期的に発生するよう変更
  - Note: Sabotageで通常Stationary Enemyを出現させる場合、ハードコーディングされた挙動のため別MODを推奨
- Deep Scan
  - Drillevator中の敵数を20%増加

### Miscellaneous

- ダウン時のサウンドを追加 (ランダム)
- Acid Queenのスポーングローバルサウンドを追加
- この難易度向けのSpace Rig Tipsを追加
  - カスタム要素、敵、ゲームプレイ変更点に関する情報を表示
- ミッション固有のゲームプレイ通知を追加
  - 対象ミッション開始時に重要なゲームプレイ変更を表示
- QoL: 回収作戦中、防衛エリアのプレイヤーがいない場合のミッションコントロールのメッセージを無効
- QoL: 回収作戦中、ソロの場合、防衛エリアのプレイヤーがいない場合のペナルティを調整
- CD2専用: 独自エリートの名称を変更
- CD2専用: 一部の独自エリートの色を変更
- CD2専用: SentinelやCrawlerなどの名称を変更し、イベント湧きと区別
- CD2専用: Custom Elite名では冗長な敵種族名を省略 (例: "Glyphid")

## Current Changes

- General Difficulty
  - P4のEnemy Count Modifier (Haz5比x1.4) を基準に、ミッション固有の補正を調整
    - Point Extraction、Salvage Extraction、RefiningStalled、Sabotage DuringEncounters
  - Encounter Difficultyの平均値を190から240に引き上げ
    - 極端な難度の抽選を減らし、Encounterの難度を安定化
  - Swarmの発生間隔を調整
    - 短間隔・長間隔での発生を抑え、標準的な間隔で発生しやすく変更
    - 平均間隔は約241秒を維持
- Mission Events
  - Gold Risk
    - SalvageのGOLD RISK最大取得Gold量をMini-Muleの数に応じて調整
      - Mini-Mule 2体: 300 Gold / 3体: 350 Gold
  - RED ALERT
    - Occurrence & Triggers (発生率・発生対象)
      - RED ALERTの発生率を調整
        - 初期20%、通常Swarmごとに+5% (最大30%)
        - 初回RED ALERT発生後は20%で固定
      - Point ExtractionのSwarmをRED ALERTの発生対象に追加
        - 通常のRED ALERTと異なり、バニラの仕様上、予備通知なし・準備猶予時間が短い
      - SalvageのUplink / Refuel防衛フェーズをRED ALERTの発生対象に追加
      - On-site Refiningの精製フェーズをRED ALERTの発生対象に追加
      - Escort DutyのオモランフェーズをRED ALERTの発生対象に追加
    - Variants & Wave Composition (種類・Wave構成)
      - RED ALERTの種類判定処理を再構築
      - 全RED ALERTバリエーションの抽選Weightを均等化
      - Heavy Waveを追加 (Praetorian、Sentinel、マルチプレイ限定)
      - Swarmer Waveを追加 (Swarmer、Shocker)
      - Mactera Waveの敵構成にGoo BomberとGrabberを追加
      - Mactera / Ranged Waveの抽選Weightをバニラの敵Rarityに近づくよう調整
    - Spawn Patterns (出現パターン)
      - Rangedの出現パターンをConstant Pressure型に変更
    - Notifications & Fixes (通知・修正)
      - 通知タイミングをそれぞれ2秒早めるよう調整
      - 再トリガー時に発生タイミングがずれる問題を修正
  - Halloween Event
    - Elite Halloween Skullを追加
      - 移動速度をx1.5に設定（体力は変更なし）
      - 死亡時にInstant Waveを発生
      - 出現時に通知メッセージを表示
- Elite & Custom Enemies
  - Elite Stalkerの移動速度をx1.5からx2.0に増加
- Mission-specific Changes
  - Egg Hunt
    - Swarmが発生しないEgg Ambushの敵数を増加
      - 基本倍率: x2.0、Ambush発生回数に応じてx0.8～x1.2で段階的に補正
      - 最終倍率: x1.6 / x1.8 / x2.0 / x2.2 / x2.4
  - Salvage Operation
    - Uplink / Refuel防衛フェーズ中のSentinel増援が意図した数で出現していなかった問題を修正
    - Extraction中のEnemy Count Modifierの最大倍率をx2.0に制限
  - Industrial Sabotage
    - Encounter Difficultyをx1.4に変更し、Enemy Count Modifierとの相殺補正を調整

## Future Plans

- General Difficulty
  - Difficultyバランスを見直し
- Mission Events
  - ゴールド採掘システムの調整
    - イベント内容、バランスの調整
    - 鉱物をテーマとした特殊エンカウントの追加
    - Gold RiskのCrassus DetonatorからElite属性を削除
      - Goldの見た目を維持し、Directによる設定を適用しやすくするため
      - 死亡時のCarve直径を通常のBulk Detonatorと同じ値に変更
      - 死亡時のMeatballを削除
  - RED ALERTシステムの拡張
    - On-site Refining、Salvage Operation、Escort DutyのイベントフェーズをRED ALERTの発生対象に追加
    - 追加WaveのパターンおよびDifficulty配分を見直し
    - 1ミッション2 Swarmを基準に、約2.5ミッションに1回程度を目標として発生率を再調整
    - 追加Waveパターンを検証
      - Peak: Swarm本来のSpawn曲線を維持するパターン
      - Sustain: Swarm後半のSpawn量の減少を補完し、Swarm全体を通して一定のSpawn圧を維持するパターン
      - Constant Pressure: Swarm本来のConstant Pressureを強化するパターン
      - Offset Pressure: Swarm本来のSpawnからタイミングをずらしてConstant湧きするパターン
    - RED ALERT専用の敵や特殊エンカウントの追加
      - e.g. Enemy Mutations, more Elites, etc.
    - RED ALERT全体のイベント内容およびバランスを継続的に調整
- Elite & Custom Enemies
  - CD2専用: 通常のEnemy Poolから出現するSentinelとCrawlerの外見を変更
  - Elite Spreaderの雪玉を調整
- Mission-specific Changes
  - Escortの固定と特殊枠の制限 (Fire Bomber、Scalebrambleとか)
  - Egg Hunt、Elimination、Sabotageのバランス調整
  - SabotageのWaveを実装
  - Elimination
    - DreadnoughtのHealth Gateを調整
    - Dread Helperを見直し、追加Waveを実装
    - Dread Helperを知らないプレイヤーにも、その意図が伝わりやすいよう改善
- 新たなエリートの追加と出現率の調整
  - バニラに存在しないエリートの追加
  - Rockpox派生Eliteの追加
  - 脅威度の高いEliteバリエーションを追加
  - 高Courage、LST、HVTへの対処の重要性を高める
- 固定敵の種類数と出現数を増加
- Enemy Balance
  - 温度閾値の調整
  - 恐怖のバランス調整
  - Enemy Count ModifierおよびMore Enemies(ME)の影響を受ける一部の敵のスポーン数を調整
    - 例: Scrab、Patrol Bot、Nemesis
- Miscellaneous
  - QoL要素の追加
    - Salvageのバルクの地形破壊無効
    - Acid Queenなど、出現・HP・撃破状況が重要な敵の状態を把握できるよう改善
  - 補給可能時の通知メッセージ追加 (将来的なNitraコスト変更への対応)
