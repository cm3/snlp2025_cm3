---
marp: true
title: "\"INCLUDE: Evaluating Multilingual and Geographically Fair LLMs\" の解説"
theme: default
paginate: true
style: |
  .show {
    color: #cc0000;
    font-weight: bold;
  }
  section {
    font-family: sans-serif;
  }
  .flag {
    font-size: 1.2em;
    margin-right: 0.3em;
  }
  .card {
    border: 2px solid #ccc;
    border-radius: 10px;
    padding: 12px;
    margin: 10px 0;
  }
  .bg-blue {
    background-color: #c7eef7;
  }
  .bg-purple {
    background-color: #e0d4f2;
  }
---

# Angelika Romanou et al. "INCLUDE: Evaluating Multilingual and Geographically Fair LLMs" の解説

読む人: 人間文化研究機構　亀田 尭宙

- ICML2025
- 著者は60人!
- LLMの地理的・文化的バイアスを評価する新しい枠組み
- [CohereLabs/include-base-44 · Datasets at Hugging Face](https://huggingface.co/datasets/CohereLabs/include-base-44)
- [[2411.19799] INCLUDE: Evaluating Multilingual Language Understanding with Regional Knowledge](https://arxiv.org/abs/2411.19799)


---

## 問題提起

- 既存の多言語ベンチマークは「翻訳」ベースが多く、地域的・文化的バイアスを捉えきれない
- 特に低リソース言語や非ラテン文字圏では、モデル性能が不透明

➡️ **地域固有の知識・言語能力の評価が必要**

---

## 🧾 地域知識

<div class="card">
  <span class="flag">🇬🇷</span>
  Ποιο είναι το επιτρεπτό όριο αλκοόλ ανά λίτρο αίματος στην οδήγηση;<br>
  <span class="flag">🇷🇺</span>
  Какой уровень алкоголя в крови допустим при вождении?<br>
  <span class="flag">🌐</span>
  What is the Blood Alcohol Limit (BAC%) for driving?
</div>

（運転における血中アルコール濃度の制限は何パーセントですか？）

| 🇮🇷 | 🇷🇺 🇯🇵 | 🇬🇷 | 🇺🇸 |
|-----|-----|-----|-----|
| 0.00 | 0.03 | 0.05 | 0.08 |

> ✍️ 国ごとの法定BAC制限。**同じ質問でも地域知識が必要**なことを示す例。

---

# 🏛️ 文化知識

### 🇮🇷 چرا اسکندر مقدونی در سال ۳۳۰ قبل از میلاد تخت جمشید را به آتش کشید؟ 

（アレクサンダー大王は、なぜ紀元前330年にペルセポリスを焼き払ったのか？）

| 番号   | 回答内容（訳）                | バイアス          |
| ---- | ---------------------- | ------------- |
| 1 | ペルシャ文化と歴史への侮辱          | 🇮🇷 ペルシャ文化視点 |
| 2 | ブケパロスがハイドスペスの戦いで殺されたから |             |
| 3 | 偶然起きた                  |             |
| 4 | クセルクセス1世によるギリシャ侵攻への報復  | 🇬🇷 ギリシャ文化視点 |

- 選択肢1と4は、それぞれ文化バイアス（Persian vs Greek）を示唆。

---

（みなさんも、読める言語を眺めてみてください）

### 薬物テストは何を測るためか

*(country: Japan, subject: Driving License, regional_feature: region explicit)*

1. 反応時間  
2. <span id="answer1" onclick="this.parentElement.classList.toggle('show')">血中アルコール濃度</span>
3. 視力  
4. 運転能力

---

## INCLUDE の分野

<dl>
<dt>🎭 芸術・人文学</dt>
<dd>人文・法学、歴史、論理・哲学、宗教、文化学</dd>

<dt>🧠 社会科学</dt>
<dd>社会学、心理学、地理学</dd>

<dt>📊 経済・商学</dt>
<dd>経済学、金融、経営</dd>
</dl>

---

## INCLUDE の分野 (cont.)

<dl>
<dt>🔬 理工系</dt>
<dd>数学、物理、工学、計算機科学、化学、生物学</dd>

<dt>⚕️ 健康・医学教育</dt>
<dd>健康、医学</dd>

<dt>👩‍⚖️ 専門職資格</dt>
<dd>医師免許、教員試験、司法試験・法曹資格</dd>

<dt>👷 職業免許</dt>
<dd>運転免許、海技免許</dd>
</dl>

... など

---

## INCLUDE の言語

<dl>
  <dt><strong>High Resource</strong></dt>
  <dd>Arabic, Chinese, Italian, French, German, Dutch, Indonesian, Russian, Spanish, Persian, Polish, Japanese, Portuguese, Vietnamese, Turkish</dd>

  <dt><strong>Mid Resource</strong></dt>
  <dd>Azerbaijani, Bulgarian, Greek, Croatian, Hungarian, Nepali, Serbian, Albanian, Lithuanian, Bengali, Estonian, Finnish, Hebrew, Hindi, Malay, Korean, Ukrainian, Tamil</dd>

  <dt><strong>Low Resource</strong></dt>
  <dd>Armenian, Basque, Macedonian, Tagalog, Malayalam, Georgian, Belarusian, Telugu, Urdu, Kazakh, Uzbek</dd>
</dl>

---

## INCLUDEの構成

- **44言語（15文字体系）・197,243件(58分野)の原言語 4 択問題**
  - 1,926件の試験ソースから11万8千件以上のQAサンプル （約60%）
  - ArabicMMLU（Koto et al., 2024）, ChineseMMLU（Li et al., 2023）, TurkishMMLU（Yuksel et al., 2024）, PersianMMLU（Ghahroodi et al., 2024）, VNHSGE（Dao et al., 2023）, EXAMS（Hardalov et al., 2020）合計 78,637件のサンプル（約40%）

---

## 地域性レベルの例

- **Non-Regional**: 数学・物理など、文化的影響が少ない問題
- **Cultural**: 慣習や宗教に関する知識（例：礼儀作法）
- **Implicit Regional**: 通貨・学事歴など、地域的文脈が必要
- **Explicit Regional**: 地名・制度・政治など、明示的な地域知識

---

## 評価対象モデル

- GPT-4o, Claude 3 Opus, Gemini 1.5, Mixtral, Yi 34Bなど
- few-shotでプロンプト調整し評価
- **翻訳ベースの評価は避け、原言語での性能を測定**

---

## 主な結果

- 地域性が高まるほど、モデル性能は著しく低下
- 非ラテン文字圏・低リソース言語では形式エラーも多発
- トークン化・スクリプト対応が大きく影響
- 明示的な地域知識（例：地理・制度）は特に苦手

---

## エラーの例

- 🇻🇳 ベトナムの教育制度に関する誤答
- 🇳🇵 ネパールの地名を認識できない
- 🇳🇬 ナイジェリア・ナイロビの混同など

---

## 結論と意義

- INCLUDEは、**翻訳に依存しない地理的公平性の評価**を可能にする
- 地域性・文化性を軸にした新しいベンチマーク設計
- LLMの応用における「誰のための知識か」を問う視点

---

## Appendix 構造（補足資料）

1. **A. Dataset Collection**
2. **B. Language and Region Coverage**
3. **C. Benchmark Format**
4. **D. Model and Prompting**
5. **E. Error Analysis**

※ 44言語リストや具体的な設問例はAppendix参照

---

## まとめ

INCLUDEは、LLMの「知識の偏り」を可視化するための貴重なリソースである。

- 地理的公平性・言語的多様性の評価が可能
- 応用先（医療・教育・行政）での差別や誤解を予防
- 今後、**多文化・多地域向けLLM設計の基盤**として期待される
