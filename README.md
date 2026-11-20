# Can Claude Ingratiate While Pushing Back?

**How an AI assistant's warmth and agreement vary with the user's motivation and emotional state: an analysis of 245,927 real Claude.ai conversations.**

Exploratory data analysis of Anthropic's privacy-preserving [Anthropic Insights dataset](https://huggingface.co/datasets/Anthropic/enabling-independent-research) (Oxford subset, released August 2026).

📄 [Full report](report.md) · 📊 [Notebook](ingratiation_analysis.ipynb) · 📎 [Supplementary material](supplementary.md)

---

## Why this question

Recent studies show that language models trained or prompted to be warm become more likely to agree with users and to withhold criticism, especially when users appear emotionally vulnerable (Ibrahim et al., 2026; Li et al., 2026). Anthropic's constitution for Claude asks for both warmth and the avoidance of sycophancy. This project uses real-world usage data to describe how Claude's warm, affirming behaviour ("ingratiation") and reserved, factual behaviour ("withdrawal") are distributed across users with different motivations and emotional states, and how they combine with flattery, agreement and pushback.

## Key findings


1. **Ingratiation follows emotional openness, not only positive emotion.** It was most frequent for users seeking connection or support, such as *longing* (66.5% vs 32.0% overall) and *acute distress* (51.4%). Withdrawal was most frequent for task-focused users with *impatient frustration* (57.4% vs 42.3%) or *perfectionism* (53.6%).
2. **Ingratiation tracks how pleasant the user's state is, not how energetic.** As users were rated happier, ingratiation rose from 27% to 88%. It fell as both frustration (high-energy) and boredom (low-energy) increased, and barely changed with tiredness.
3. **Whether the user's state could be read at all matters most.** In 10 of 11 user-state tables, the strongest association involved the "not applicable" category. For example, ingratiation was 66% when a positive state such as `feel_good` was rated, and 32% when it was not.
4. **Emotionally open conversations were more engaged in both directions.** They received more agreement *and* more disagreement, and more mixed flattery/challenge. Pure flattery was elevated only for *longing* (21.9% vs 8.0%).

**Bottom line:** the data show *where* warm and challenging behaviour co-occur. They cannot show whether Claude avoided sycophancy, because no label measures whether an agreement was warranted.

## Data and approach

| | |
|---|---|
| **Data** | 245,927 Claude.ai conversations (April–May 2026), released as aggregated two-way tables; questions designed by the University of Oxford, labels produced by a Claude model |
| **Variables** | 1 behaviour facet (ingratiation/withdrawal), 4 related behaviour facets, 8 user-motivation groups, 11 user-state scales (1–6) |
| **Statistics** | Cramér's V (with and without "not applicable"), adjusted standardised residuals, percentage-point differences from the whole sample; no p-values (n ≈ 246,000) |
| **Validation** | Structural `assert` checks, unit-tested statistics helpers, a fingerprint check that the raw data is never modified, and a known-groups check to infer the direction of unlabelled rating scales |

## Skills demonstrated

- **Working with unfamiliar, aggregated data.** Reverse-engineering the dataset structure (clusters, levels, cross-tab columns, suppressed cells), and documenting gaps such as 1.4% of conversations missing from one facet.
- **Statistical reasoning for categorical data.** Choosing effect sizes over significance tests at large n, and separating "not rated" from real ratings.
- **Measurement validity.** Inferring scale direction with a known-groups design (the rating scales were published without anchors), and defining labels empirically from co-occurring behaviours.
- **Reproducible analysis.** One notebook that runs top to bottom, with built-in checks, saved tables and figures, and pinned package versions.
- **Scientific communication.** A structured report with limitations, references and testable follow-up studies.

## Limitations

All labels (user states, motivations and Claude's behaviour) were produced by one Claude model and were not validated against human raters. The data contain only two-way tables, so results are associations, not causes. Sycophancy itself is not measured. Details: [report §1.4 and §6](report.md#6-limitations).

## Repository structure

```
├── README.md
├── report.md                       # full report: introduction, method, results, discussion, references
├── supplementary.md                # S1–S5: scale checks, label profiles, full tables
├── ingratiation_analysis.ipynb     # complete analysis (data loading → figures)
├── requirements.txt
└── outputs/
    ├── figures/                    # Figures 1–4 and S1
    └── tables/                     # every computed table as CSV
```


## Key references

- Anthropic (2026). [Enabling independent research on how people use Claude](https://www.anthropic.com/news/enabling-independent-research) (and appendix).
- Anthropic (2026). [Claude's constitution](https://www.anthropic.com/constitution).
- Ibrahim, Hafner & Rocher (2026). Training language models to be warm can reduce accuracy and increase sycophancy. *Nature*. [doi:10.1038/s41586-026-10410-0](https://doi.org/10.1038/s41586-026-10410-0)
- Li et al. (2026). [Affective context amplifies sycophancy in LLM responses](https://arxiv.org/abs/2608.21242). arXiv.

Full reference list in the [report](report.md#references).

---

**Author:** Arkadij Kisielius
Data: [Anthropic/enabling-independent-research](https://huggingface.co/datasets/Anthropic/enabling-independent-research), CC BY 4.0.
