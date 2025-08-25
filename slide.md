---
marp: true
title: "\"INCLUDE: Evaluating Multilingual and Geographically Fair LLMs\" の解説"
theme: default
paginate: true
style: |
  .answer-button {
    display: inline-block;
    padding: 0.5em 1em;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1em;
    margin-top: 1em;
  }
  .show {
    color: #cc0000;
    font-weight: bold;
  }

---

# Angelika Romanou et al. "INCLUDE: Evaluating Multilingual and Geographically Fair LLMs" の解説

人間文化研究機構　亀田 尭宙

- ICML2025
- 著者は60人!
- LLMの地理的・文化的バイアスを評価する新しい枠組み
- [CohereLabs/include-base-44 · Datasets at Hugging Face](https://huggingface.co/datasets/CohereLabs/include-base-44) データセットは小規模
- [[2411.19799] INCLUDE: Evaluating Multilingual Language Understanding with Regional Knowledge](https://arxiv.org/abs/2411.19799)

---

# 薬物テストは何を測るためか

*(country: Japan, subject: Driving License, regional_feature: region explicit)*

1. 反応時間  
2. <span id="answer1">血中アルコール濃度</span>
3. 視力  
4. 運転能力

<div class="answer-container">
  <button class="answer-button" onclick="document.getElementById('answer1').parentElement.classList.toggle('show')">
    答え
  </button>
</div>

---

## 問題提起

- 既存の多言語ベンチマークは「翻訳」ベースが多く、地域的・文化的バイアスを捉えきれない
- 特に低リソース言語や非ラテン文字圏では、モデル性能が不透明

➡️ **地域固有の知識・言語能力の評価が必要**

---

## INCLUDEの構成

- **44言語・22,000問超の原言語MCQ（多肢選択）問題**
- ソース：各国の教育試験・資格試験など
- 翻訳なし、各言語で作問
- 地域性レベル（4段階）をラベル付け：
  1. Non-Regional  
  2. Cultural  
  3. Implicit Regional  
  4. Explicit Regional

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
