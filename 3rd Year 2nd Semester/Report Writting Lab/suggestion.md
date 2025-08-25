

* **TOPSIS** (Technique for Order Preference by Similarity to Ideal Solution)
* **ASP** (Analytic Scoring Process)
* **AHP** (Analytic Hierarchy Process)
* **FAHP** (Fuzzy AHP)



---

# 📄 IEEE Paper Draft Structure

## Title

**"Comparative Decision-Making Analysis for AI Company Investments using TOPSIS, ASP, AHP, and FAHP"**

## Abstract

* Briefly explain the investment scenario (angel investor choosing among AI companies).
* Mention the need for structured decision-making methods (MCDM).
* State that this paper applies **TOPSIS, ASP, AHP, and FAHP** to rank AI companies.
* Highlight the outcome (comparison of rankings, insights into robustness, decision support).

---

## I. Introduction

* Explain Shark Tank–like scenario: investor wants to select AI company to invest in.
* Discuss the complexity: multiple evaluation criteria (e.g., **innovation, market share, revenue growth, scalability, ethical AI, model adoption rate**).
* Justify why MCDM methods are suitable.
* State research objective: **compare outcomes of four decision-making techniques on the same dataset.**

---

## II. Literature Review

* Define **MCDM methods** in investment & technology adoption.
* Briefly review:

  * **TOPSIS** – proximity to ideal solution.
  * **ASP** – scoring based method.
  * **AHP** – pairwise comparisons & hierarchy building.
  * **FAHP** – fuzzy logic extension of AHP to deal with uncertainty.
* Summarize related works (investment decisions, startup evaluations, technology adoption studies).

---

## III. Methodology

### A. Alternatives (AI Companies)

* OpenAI, Grok, Gemini (and maybe Anthropic, Cohere to make dataset richer).

### B. Criteria for Evaluation

Examples:

1. **Innovation Index (C1)**
2. **Market Adoption / Customers (C2)**
3. **Revenue Growth (C3)**
4. **Scalability (C4)**
5. **Ethical AI / Safety (C5)**

### C. Data Collection

* Hypothetical but justified using news reports, market estimates, or scoring system (e.g., 1–10 scale).
* Mention normalization for fair comparison.

### D. Application of Methods

* Explain step-by-step how each method works.
* Provide formulas & mathematical steps.

  * **TOPSIS** → Normalize, weight, find ideal best/worst, calculate closeness coefficient.
  * **ASP** → Weighted scoring.
  * **AHP** → Pairwise matrix, eigenvalue method, consistency ratio.
  * **FAHP** → Fuzzy pairwise comparison, defuzzification.

---

## IV. Results and Discussion

* Present tables of results (scores & rankings from each method).
* Compare rankings: e.g.

  * TOPSIS ranks OpenAI > Gemini > Grok.
  * AHP ranks Gemini > OpenAI > Grok.
  * ASP shows slight differences.
  * FAHP handles uncertainty better, showing more stable ranking.
* Discuss why differences exist (some methods emphasize criteria differently).
* Provide **graphical comparison (bar chart / radar chart)**.

---

## V. Conclusion

* Summarize insights: which company is most preferable across methods.
* Highlight robustness: FAHP/AHP handle subjectivity, TOPSIS shows efficiency.
* Mention practical implication for investors: **no single method dominates → triangulation of results is more reliable.**

---

## References (IEEE Style)

* Cite papers on TOPSIS, AHP, FAHP.
* Cite AI company reports (OpenAI, Google DeepMind, xAI, Anthropic).
* Example:

```
[1] C. L. Hwang and K. Yoon, "Multiple Attribute Decision Making: Methods and Applications," Springer, 1981.  
[2] T. L. Saaty, "The Analytic Hierarchy Process," McGraw-Hill, 1980.  
[3] Z. L. Deng, "Fuzzy Analytic Hierarchy Process: Application and Evaluation," Int. J. Approximate Reasoning, vol. 52, pp. 395–407, 2011.  
```

---

