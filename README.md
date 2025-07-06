# store-sales-forecast
Kaggle: Store Sales Time Series Forecasting with feature engineering and LightGBM

# 🛒 Store Sales - Time Series Forecasting

Kaggleコンペ「[Store Sales - Time Series Forecasting](https://www.kaggle.com/competitions/store-sales-time-series-forecasting)」への参加記録です。  
初心者が段階的にモデルを改善し、ポートフォリオとして記録できるよう、各バージョンでの学びとスコアの推移をまとめています。

---

## 📌 概要

エクアドルのスーパーマーケット「Favorita」の売上を予測する時系列予測タスクです。  
日付、店舗、商品カテゴリ、プロモーション、祝日、外部要因（オイル価格・取引数など）を使い、将来15日間の売上を予測します。

- **評価指標**: Root Mean Squared Logarithmic Error (RMSLE)
- **目的**: 初心者が特徴量エンジニアリングとモデル改善を段階的に学ぶ

---

## 📊 スコア比較（RMSLE）

| Version | 特徴量構成                    | スコア     | コメント                                 |
|---------|-------------------------------|------------|------------------------------------------|
| V1      | 日付情報 + 商品カテゴリなど   | 1.59238    | ベースラインモデル                       |
| V2      | V1 + ラグ/移動平均/標準偏差   | **1.30386** | 売上傾向を捉える特徴量で大幅に改善       |
| V3      | V2 + 祝日フラグ（is_holiday） | 1.32731    | 単純な祝日フラグでは精度悪化             |

---

## 🧪 Versionごとの特徴と学び

### ✅ Version 1: ベースラインモデル

- 特徴量: `store_nbr`, `family`, `onpromotion`, `dayofweek`, `month`, `year`
- モデル: LightGBM（最小構成）
- 学び: 学習〜提出の基本フロー確認

---

### ✅ Version 2: ラグ特徴量と移動平均の追加

- 追加特徴量: `lag_7`, `lag_14`, `rolling_mean_7`, `rolling_std_7`
- 結果: スコアが約18%向上（1.59 → 1.30）
- 学び: 時系列予測におけるラグ特徴量の効果を体感

---

### ✅ Version 3: 祝日フラグの追加

- `holidays_events.csv` から `is_holiday` を作成
- 精度はやや悪化（1.30 → 1.32）
- 学び: 外部情報は処理次第でノイズにもなる

---

## 🔧 今後の改善アイデア

- `transactions.csv` を使った来店者数の導入
- `holiday.type` に基づくOne-hotフラグ（例: `is_Event`, `is_WorkDay`）
- クロスバリデーション（TimeSeriesSplit）
- Optunaによるパラメータ最適化

---

## 🛠 使用技術

- Python (pandas, numpy, lightgbm, sklearn)
- Kaggle Notebook
- 時系列データ処理、特徴量エンジニアリング

---

## 📂 ファイル構成例

