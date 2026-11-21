# Red Alert Protocol

## Table of Contents <!-- omit in toc -->

- [Concept](#concept)
- [公開ロビー向け](#公開ロビー向け)
- [What's New v3](#whats-new-v3)
- [想定敵数](#想定敵数)
- [Hazard 5との平均パラメータ比較](#hazard-5との平均パラメータ比較)
- [Changes](#changes)
  - [難易度全般](#難易度全般)
  - [イベント](#イベント)
  - [Stationary Enemy Changes](#stationary-enemy-changes)
  - [Elite \& Custom Enemies](#elite--custom-enemies)
  - [ミッション個別調整](#ミッション個別調整)
  - [その他](#その他)
- [Experimental Features](#experimental-features)
- [Future Plans](#future-plans)

## Concept

Hazard 5のゲームテンポと基本的なプレイ感をベースに、  
バニラの体験を大きく崩さない範囲で調整した、野良ロビー向けの難易度。

基本的に難易度はT1を想定しているが、  
ミッション、イベント、洞窟構成、併用するMODなどの条件によっては、T2相当の難易度になる場合がある。  
(例：SabotageでのStationary Enemy追加やCustom Cave Layout)

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

## What's New v3

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

## 想定敵数

- ME0 : Haz5   x 1.5 程度
- ME1 : Haz6   x 1.5 程度
- ME2 : Haz5.5 x 2   程度

敵数は各Hazard 5+ Modifierレベル向けに調整されており、  
難易度の主な変化要因はModifier側となるよう設計されています。

## Hazard 5との平均パラメータ比較

- Enemy Count Modifier         : 1.113 -> 1.58 (ME1: 1.89 / ME2: 2.36)
- Encounter Difficulty         :   337 -> 190
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

### 難易度全般

- ME0 / ME1 / ME2 個別に調整されたEnemyCountスケーリングとなるよう調整
- Haz5x2のような敵の密度をSwarmにフォーカスした難易度となるよう調整
- Swarm以外の敵の数と間隔を下方修正 (Encounter、Stationary、Enemy Normal Wave)
- EnemyCountスケーリングによって想定以上に影響を受ける敵のスポーン数を再調整
  - Crawler、Pit Jaw、Scrab

### イベント

- Gold Riskシステムを追加
  - 一定量のゴールドを採掘するとイベントが発生 (Compressed Goldは対象外)
  - 進捗50%、75%、90%で警告メッセージを表示
  - イベント発生時に最終警告を表示
  - 進捗75%到達後、Elite Ebonite Glyphid GruntによるMini Waveが定期的に発生
  - 進捗100%到達時、Elite Glyphid Crassus Detonatorが出現
- RED ALERTシステムを追加
  - Alert Swarmは低確率でRED ALERTへ昇格する
  - RED ALERTの基本発生率は10%
  - 通常Swarmが発生するたびに発生率が5%上昇し、最大20%まで増加
  - RED ALERT発生時、発生率は10%にリセットされる
  - RED ALERT発生時は専用警告メッセージが表示される
  - RED ALERT中は通常のSwarmとは別に、元のSwarm規模の約25%に相当する追加Spawn Waveが発生する
    - 試験的なRED ALERTバリエーション：Grunt、Mactera、Ranged、Exploder増援

### Stationary Enemy Changes

- Stationary Difficultyで空ロールを廃止  
  (Enemy Count補正込みの総難度は概ねHazard 5相当を維持しつつ、  
  平均難度を158→168へ増加)
- StationaryEnemyDiversityを 2–4 から 3–5 に増加
- Elite Cave Leechを追加  
  (触手速度40%低下、実HP25%増加、P4で約173EHP、無音)
- Brood Nexusの調整
  - Brood NexusからGlyphid Spawn以外のクリーチャーも出現するように変更  
    (放置されがちなため)
  - 生成間隔を10秒から30秒に変更
  - 死亡時のSpawn数を15から10に変更

### Elite & Custom Enemies

- SentinelをEnemy PoolにPraetorianと同程度の出現率で追加
- Acid QueenをSpecial PoolにMenaceと同程度の出現率で追加  
  (DamageMultiplier 5.5、実体力は545)
- エリートのダメージ抵抗のスケーリングを修正
- カスタムEnemyグループ (LST、HVT、Special、Disruptive) を追加
  - 敵の出現頻度を制御するため、グループ毎のクールダウンを設定
  - クールダウン毎に各グループから1体のみVeteranへ昇進可能
- Elite Septic Spreader を Ranged Special Enemy Group に追加  
  (Red Sepsisの代わりに雪玉を発射、P4で480EHP、温度閾値2倍)
- Elite Stingtail を HVT Disruptive Enemy Group に追加  
  (掴みクールダウン短縮、恐怖無効、P4で480EHP、温度閾値1.5倍)
- Elite Warden を LST Disruptive Enemy Group に追加  
  (バフ範囲1.5倍、スタン・恐怖無効、P4で1200EHP、温度閾値1.5倍)
- Mactera Fire Bomber を LST Disruptive Enemy Group に追加  
  (Mactera Goo Bomberからのみ昇進)

### ミッション個別調整

- ミッション全般
  - Extractionフェーズ中の敵数を増加 (Point Extractionの脱出カウントダウン中も含む)
- On-site Refining
  - Refineryでパイプが壊れた際の敵の数を減少
- Salvage Operation
  - Mini Muleの足スキャン時間を2秒から1秒に変更
  - 修理の秒数をByPlayerCountに応じて10秒から10 / 20 / 30 / 40 秒に変更
  - 修理に必要な足の数を2-5のランダムに設定
  - MiniMule/Uplink/Refuelの協力インタラクト倍率をx5に設定
  - SalvageのExtraction中、時間経過で敵数が増加
    - Drop Pod起動時から敵数が増加し始める
    - Drop Podのドアが開く頃には敵数がおよそ2倍になる
    - 脱出完了まで敵数は増加し続ける
- Point Extraction
  - Point Extractionの敵の数を減少
- Escort Duty
  - Dorettaの大ダメージ判定のしきい値を削除
  - Dorettaの大ダメージ耐性を0.5から0.75に減少

### その他

- ダウン時のサウンドを追加 (ランダム)
- Acid Queenのスポーングローバルサウンドを追加
- この難易度向けのSpace Rig Tipsを追加
  - カスタム要素、敵、ゲームプレイ変更点に関する情報を表示
- QoL: 回収作戦中、防衛エリアのプレイヤーがいない場合のミッションコントロールのメッセージを無効
- QoL: 回収作戦中、ソロの場合、防衛エリアのプレイヤーがいない場合のペナルティを調整
- CD2専用: 独自エリートの名称を変更
- CD2専用: 一部の独自エリートの色を変更

## Experimental Features

- 難易度全般
  - MinPoolSizeを8から10に増加  
    (Enemy Poolへの敵追加後も敵の多様性を維持するため)
  - StationaryEnemyCountを4から5に増加  
    (Elite Cave Leech追加後も固定敵の種類を維持するため)
- Gold Riskシステム
  - Elite Ebonite Gruntの挙動を変更
    - Gold Risk進捗75%到達後に出現する仕様はそのまま
    - 衝突判定を追加し、踏みつけで倒せるように変更 (クリボー風)
    - 倒すとGold Risk進捗1%分に相当するGoldをドロップするように変更
  - Elite Crassus Detonatorを調整
    - 常時アウトラインを追加
- Stationary Enemy Changes
  - Elite Cave LeechのEHPをP4で240へ増加
  - Cave LeechのMaxDropPlayerDurationを2から10に増加
- Elite & Custom Enemies
  - CrawlerをEnemy PoolにTri-Jawと同程度の出現率で追加  
    (Spreaderと同じ温度閾値：発火35、凍結-50)
  - Elite Trawler を Melee Special Enemy group に追加  
    (P4で480EHP、温度閾値2倍、よりアグレッシブな行動)
  - Elite Youngling を Melee Special Enemy group に追加  
    (P4で300EHP、温度閾値1.5倍、転がり攻撃を優先)
  - Elite Patrol Bot を HVT Disruptive Elite Group に追加  
    (P4で324EHP、炎温度閾値0.5倍・氷温度閾値0.4倍、  
     通常弾を高速連射、体当たり攻撃なし、ハッキング不可)
  - Acid QueenのEHPを545から600に増加し、Poison Damage耐性を80%に変更  
    (自身の範囲攻撃でHPが半分以下になりにくくなるよう調整)
  - Acid Queenの出現方法を変更 (Special Enemy Poolの多様性を維持するため)
    - Special Poolから削除
    - Acid Spitterから10%の確率で昇進するよう変更
    - Ranged Special Enemy Groupに追加
  - Elite Wardenのバフ範囲と最大バフ対象数を2倍に増加
- 敵バランス
  - SwarmerのMaxSpawnCountを100に制限
  - ShredderのMaxSpawnCountを20に制限
  - Egg SpiderのSpawn数を1に制限
  - Swarmerの凍結耐性を低下 (FreezeTemperature 20 -> 8) (from VEA)
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
- ミッション個別調整
  - Dread Helperを追加
    - Dreadnought戦中に追加の脅威として出現することがあるカスタムBulk Detonator
    - ミッション開始時にDread Helperの対象となるDreadnoughtタイプの組み合わせを抽選
    - 結果として戦闘あたり平均約46%の確率でDread Helperが出現
  - Egg Hunt
    - Swarmが発生しないEgg Ambushの敵数を増加  
      (プレイヤー人数に応じて x2.0 / x2.0 / x2.5 / x3.0)
  - Salvage Operation
    - Uplink / Refuelの防衛フェーズ中にSentinel増援を追加 (過度に防御的な地形利用への対策)
  - Sabotage
    - Hack-C防衛フェーズ中にPhase Bombが定期的に発生するよう変更
    - Note: Sabotageで通常Stationary Enemyを出現させる場合、ハードコーディングされた挙動のため別MODを推奨
- その他
  - ミッション固有のゲームプレイ通知を追加
    - 対象ミッション開始時に重要なゲームプレイ変更を表示
  - CD2専用: SentinelやCrawlerなどの名称を変更し、イベント湧きと区別

## Future Plans

- ゴールド採掘システムの調整
  - イベント内容、バランスの調整
  - 鉱物をテーマとした特殊エンカウントの追加
  - Gold RiskのCrassus DetonatorからElite属性を削除
    - Goldの見た目を維持し、Directによる設定を適用しやすくするため
    - 死亡時のCarve直径を通常のBulk Detonatorと同じ値に変更
    - 死亡時のMeatballを削除
- RED ALERTシステムの拡張
  - RED ALERT専用の敵や特殊エンカウントの追加
    - e.g. Enemy Mutations, more Elites, etc.
  - イベント内容、バランスの調整
- ミッション固有のギミック・調整
  - Escortの固定と特殊枠の制限 (Fire Bomber、Scalebrambleとか)
  - Drillevator中の敵設定を調整
  - Egg Hunt、Elimination、Sabotageのバランス調整
  - Elimination、SabotageのWaveを実装
- 新たなエリートの追加と出現率の調整
  - バニラに存在しないエリートの追加
  - 脅威度の高いEliteバリエーションを追加
  - 高Courage、LST、HVTへの対処の重要性を高める
- 固定敵の種類数と出現数を増加
- 温度閾値の調整
  - Dreadnoughtの炎上温度を調整
- 恐怖のバランス調整
- Enemy Count ModifierおよびMore Enemies(ME)の影響を受ける一部の敵のスポーン数を調整
  - 例: Scrab、Turret、Patrol Bot、Nemesis
- QoL要素の追加
  - Salvageのバルクの地形破壊無効
- 補給可能時の通知メッセージ追加 (将来的なNitraコスト変更への対応)
