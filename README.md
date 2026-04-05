# decay-optimization-v0.1
Draft multi-axis decay model for Immune Royalty OS, balancing lineage, time, and pressure-responsive rebalancing to prevent structural lock-in.

減衰最適化の初期仕様

Decay Optimization Model v0.1（DOM v0.1） は、
Immune Royalty OS v0.1 における動的調整レイヤーの中核モデルです。

この仕様の目的は、
古い痕跡の暴走、価値集中、既得権の固定化を防ぎつつ、新芽の成長と文明全体の流動性を維持すること にあります。

減衰とは、価値の否定ではありません。
このモデルにおける減衰は、老化防止 と 循環維持 のための調整です。

1. なぜ Decay Optimization が必要なのか

印税OSや免疫型の価値循環システムでは、
痕跡を守る仕組みが強くなるほど、別の危険が生まれます。

たとえば、

古い痕跡が減衰せず、居座り続ける
一部の既存構造に価値が集中する
新しい構造が発芽しても育ちにくい
誤検出を繰り返す検出器がそのまま維持される
system が新芽保護より既得権維持に偏る

といった問題です。

Decay Optimization は、この硬直化に対して
忘却・再分配・加速調整 を制度的に入れることで応答します。

2. このモデルの目的

DOM v0.1 は、次の5つを主目的とします。

系譜距離に応じた自然減衰を定義する
時間経過に伴う優位性の自然低下を扱う
新芽圧迫や集中過多に対して加速減衰を発動する
誤検出を繰り返す検出器や旧痕跡優位の硬直化を抑制する
保護・許容・保留の判定結果に応じて減衰圧を調律する

つまりこのモデルは、
価値を消すための装置 ではなく、
価値が固まりすぎることを防ぐ装置 です。

3. 設計原理

DOM v0.1 は、以下の5原理に基づいて設計されます。

3.1 Decay is not Denial

減衰は価値の否定ではない。
それは老化防止と流動性維持のための調整である。

3.2 Multi-Axis Decay

減衰は一本では足りない。
系譜・時間・圧力 の複数軸で扱う。

3.3 Pressure-Responsive Suppression

新芽圧迫・価値集中・過敏反応には、
条件付きで加速減衰を適用する。

3.4 Tolerance-Aligned Decay

Tolerance Zone の判定結果と連動して、
減衰強度を調整する。

3.5 Explainable Rebalancing

どの減衰が、なぜ、どこに発動したのかを説明可能にする。

4. このモデルが使う変数

DOM v0.1 では、以下の変数を用います。

4.1 構造変数
g: Lineage Distance

系譜距離。
どれだけ系譜上離れているかを表します。

age_days

経過日数。
痕跡の古さを時間軸で表します。

reuse_rate

再利用率。
どれだけ頻繁に再利用されているかを表します。

4.2 圧力変数
C: Concentration Score

価値集中度。
一部痕跡への集中が強いほど高くなります。

N_block: Novelty Blocking Signal

新芽圧迫度。
旧痕跡が新しい構造を塞いでいる強さを表します。

I: Inflammation Score

過敏反応リスク。
システム全体の炎症状態を表します。

FP_r: False Positive Repetition

誤検出反復度。
同種の誤判定がどれだけ繰り返されているかを表します。

L_dom: Legacy Dominance

旧痕跡優位度。
既存痕跡が制度上どれだけ強く居座っているかを表します。

4.3 寛容文脈変数
Z_tol

Tolerance Zone で計算された寛容スコア。

decision_class

Tolerance Zone から返される判定クラス。

protect
tolerate
hold
reject-candidate

DOM v0.1 は、この結果を受けて減衰圧を調整します。

5. 減衰の3軸構造

このモデルの核は、減衰を3つに分けること です。

5.1 Lineage Decay

系譜距離に応じて自然に薄まる減衰です。
近い痕跡は強く、遠い痕跡は弱くなる。

5.2 Temporal Decay

時間経過に応じて、古い痕跡の優位を徐々に下げる減衰です。
古いというだけで消すのではなく、永続的優位を緩める ために使います。

5.3 Pressure-Responsive Decay

新芽圧迫、集中過多、炎症、誤検出反復などの圧力が強いときに、
条件付きで加速する減衰です。

この3軸を分けることで、
自然な忘却 と 必要な介入 を区別できるようになります。

6. 基本数式
6.1 Lineage Decay
D_lineage(g) = exp(-lambda_lineage * g)

系譜距離が遠いほど、影響力を自然に減らします。

6.2 Temporal Decay
D_time(age_days) = exp(-lambda_time * age_days_normalized)

ここで、

age_days_normalized = age_days / temporal_half_life_days

とします。

つまり、時間が経つほど旧痕跡の優位が少しずつ薄れていきます。

6.3 Pressure Score
P_decay = (0.35 * C) + (0.30 * N_block) + (0.20 * I) + (0.15 * FP_r)

これは、どれだけ加速減衰をかけるべきか を測る圧力総合値です。

6.4 Pressure Multiplier
M_pressure = 1 + (pressure_multiplier * P_decay)

圧力が強いほど、減衰倍率が上がります。

6.5 Pressure-Responsive Decay
D_pressure = exp(-(lambda_lineage * M_pressure) * g)

これは、系譜減衰を圧力に応じて加速した形です。

6.6 Combined Decay
D_total = w_lineage * D_lineage + w_time * D_time + w_pressure * D_pressure

3軸の減衰を重み付きで統合して、最終的な減衰値を作ります。

7. 初期パラメータ
7.1 Core Parameters
lambda_lineage = 0.35
lambda_time = 0.18
pressure_multiplier = 1.80
temporal_half_life_days = 180
7.2 Weights
w_lineage = 0.40
w_time = 0.25
w_pressure = 0.35
7.3 Trigger Thresholds
concentration_cap = 0.82
novelty_block_trigger = 0.70
inflammation_trigger = 0.68
false_positive_repetition_trigger = 0.60
legacy_dominance_trigger = 0.76
7.4 Safeguards
minimum_decay_floor = 0.05
maximum_decay_ceiling = 1.00
rebalance_to_novelty_pool_ratio = 0.20
detector_sensitivity_reduction = 0.15

これらは v0.1 の初期値であり、
将来的には観測データに応じて調整されます。

8. 圧力トリガー

DOM v0.1 では、以下の条件で介入が発動します。

8.1 Concentration Trigger

C >= concentration_cap

一部痕跡に価値が集中しすぎた場合、
再配分 を発動します。

8.2 Novelty Block Trigger

N_block >= novelty_block_trigger

旧痕跡が新芽を塞いでいる場合、
新芽救済のための加速減衰 を発動します。

8.3 Inflammation Trigger

I >= inflammation_trigger

システムが過敏化している場合、
自動攻撃圧を落とし、説明責任を強めます。

8.4 False Positive Repetition Trigger

FP_r >= false_positive_repetition_trigger

誤検出を繰り返す検出器に対して、
感度低下を返します。

8.5 Legacy Dominance Trigger

L_dom >= legacy_dominance_trigger

旧痕跡の優位が過剰な場合、
一時的な加速減衰をかけます。

9. Tolerance Zone との接続

DOM v0.1 は単独で動きません。
Tolerance Zone の判定結果 に応じて減衰強度を変えます。

9.1 Protect
decay_bias = 1.15

新芽を塞ぐ旧痕跡への減衰を、やや強めにします。

9.2 Tolerate
decay_bias = 1.00

標準的な減衰を適用します。

9.3 Hold
decay_bias = 0.95

保留中は、減衰圧を少し抑えます。

9.4 Reject-Candidate
decay_bias = 0.85

追加保護をかけず、自然減衰寄りに戻します。

調整式
D_adjusted = clamp(D_total * decay_bias, minimum_decay_floor, maximum_decay_ceiling)

ここで clamp は、最終値が最低値と最高値を超えないように制限する処理です。

10. Rebalance Actions

減衰は単に薄めるだけではなく、
再配分 とセットで働きます。

10.1 Concentration Rebalance

集中しすぎた価値の一部を、新芽プールへ還流します。

allocation weight を減らす
novelty pool に戻す
10.2 Novelty Relief Decay

新芽圧迫が強い旧痕跡に対して、加速減衰をかけます。

10.3 Inflammation Decay Suppression

炎症状態では自動反応を弱め、説明責任を強めます。

10.4 Detector Sensitivity Reduction

誤検出を繰り返す検出器の感度を落とします。

10.5 Accelerated Legacy Decay

過剰な旧痕跡優位を、一時的に解消します。

11. プロファイル

DOM v0.1 では、少なくとも3つの減衰プロファイルを持ちます。

11.1 Conservative

既存痕跡保護をやや重視し、減衰を穏やかにするプロファイルです。

11.2 Balanced

旧痕跡保護と新芽保護の均衡を取る標準プロファイルです。

11.3 Novelty-First

新芽保護と硬直化解消を優先し、圧力応答減衰を強めるプロファイルです。

これにより、文明OSの運用方針に応じて
減衰の思想 自体を切り替えられるようになります。

12. 評価パイプライン

DOM v0.1 は、次の順序で評価を行います。

Step 1

入力を収集する。
g, age_days, C, N_block, I, FP_r, L_dom, decision_class

Step 2

D_lineage を計算する。

Step 3

D_time を計算する。

Step 4

P_decay を計算する。

Step 5

圧力トリガーを確認する。

Step 6

D_pressure を計算する。

Step 7

3軸を統合し D_total を計算する。

Step 8

Tolerance Zone の結果に応じて decay_bias をかける。

Step 9

D_adjusted を出力し、必要なら再配分アクションを発動する。

13. 典型例
例1：新芽圧迫が強いケース
C = 0.84
N_block = 0.74
L_dom = 0.78
decision_class = protect

この場合は、

concentration trigger
novelty block trigger
legacy dominance trigger

が発動しやすく、
balanced profile で旧痕跡側への減衰を強めるのが自然です。

例2：安定した既存系譜
C = 0.45
N_block = 0.28
I = 0.18
decision_class = tolerate

圧力は低く、
conservative profile で自然減衰中心に扱うのが妥当です。

例3：炎症と誤検出のループ
I = 0.71
FP_r = 0.68
decision_class = hold

この場合は、

inflammation trigger
false positive repetition trigger

が発動しやすく、
攻撃圧を落としつつ検出器感度も下げる 必要があります。

14. 最適化指標

DOM v0.1 は、単に減衰式を持つだけでは不十分です。
最適化には観測指標が必要です。

主要指標
novelty_survival_rate
legacy_concentration_ratio
false_positive_rate
hold_to_protect_conversion_rate
hold_to_reject_conversion_rate
副次指標
reuse_diversity_score
time_to_novelty_visibility
legacy_decay_fairness_index
rebalance_stability_score

このモデルは、これらの指標を見ながら調整されます。

15. ガバナンス
調整方針
human-supervised
レビュー周期
30日
調整対象
lambda_lineage
lambda_time
pressure_multiplier
concentration_cap
novelty_block_trigger
inflammation_trigger
false_positive_repetition_trigger
legacy_dominance_trigger
profile selection
禁止される挙動
減衰なき永続的既得権
説明なき圧力応答減衰
減衰を隠れBANとして使うこと
Tolerance 結果の無視
再配分なき新芽抑圧
16. 現時点の位置づけ

Decay Optimization Model v0.1 は、
完成済みの最終最適化モデルではなく、最初の可動モデル です。

この段階で重要なのは、次の5点です。

減衰を 系譜・時間・圧力 に分けたこと
圧力に応じて加速減衰を発動できること
Tolerance Zone と連動すること
プロファイル切替ができること
再配分を減衰と一体で扱うこと

つまり v0.1 は、
文明OSにおける動的忘却と再均衡の最小骨格 です。

17. 今後の拡張候補
Adaptive Profile Switching

メトリクスに応じて、
conservative / balanced / novelty-first を自動切替する。

Domain-Specific Decay Curves

分野ごとに、半減期と圧力係数を最適化する。

Reinforcement-Based Decay Tuning

新芽生存率と偽陽性率に基づいて、係数を強化学習的に調整する。

Immune Map Binding

Immune Map 可視化レイヤーに、減衰軸を接続する。

18. 一文で言えば

Decay Optimization Model v0.1 とは、
古い痕跡を消すのではなく、
居座りすぎる痕跡を自然に薄め、必要なら加速的に再均衡し、
新芽と循環を守るための動的調整モデルです。
