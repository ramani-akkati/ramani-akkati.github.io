# Internal Data Intelligence Datathon 2025

## Recap & Summary

On July 24–25, the Data Intelligence team hosted data factory’s first-ever Data Blending Challenge at NVIDIA headquarters. The event brought together more than forty annotators from across the data factory. Over the course of two days, the seven participating teams, each composed of three to four members, explored new ways to blend existing data factory datasets with the goal of either improving model performance or unlocking entirely new use cases.

By the end of the challenge, a total of 102 blends had been submitted, averaging fourteen per team over the two days. Three of seven teams surpassed every provided baseline, and all seven teams beat at least two baselines; mean aggregate score was 38.66 with a 0.17 standard deviation across 102 submissions, indicating rapid convergence under a 10,000‑row cap.

## Workflow, Insights, and Solutions

The two-day sprint was structured to balance enablement with rapid, data-driven iteration. It opened with a concise briefing that outlined the challenge objectives, reviewed the seven annotated source corpora (RLHF Workflow 1, RLHF Simplified 1, RLHF Simplified 2, SLM4NPC, Physical AI, Tennis Summarization, 9K Audio Caption) and walked participants through the mechanics of the internal blending platform. Then Pratyush Muthukumar, Data Intelligence Team Lead, followed with a focused NVIDIA DLI mini-course on multimodal curation and LoRA fine-tuning, ensuring that every annotator could navigate the full toolchain before the first submission was logged.

To encourage diverse approaches, the challenge ran on two concurrent tracks. The Beat-the-Baseline track rewarded the highest aggregate benchmark lift, while the New-Use-Case track focused on blends that unlocked functionality impossible with any single dataset. Although the incentive structures differed, both tracks shared the same hard constraints-identical hyper-parameters, fixed compute budget, and the 10,000-row limit-so results remained directly comparable across teams and objectives.

During the first day, most participants concentrated on familiarizing themselves with the platform and establishing baseline blends that combined two or three corpora in straightforward ratios. The evening leaderboard provided the first tangible signals, prompting several groups to pivot their strategies overnight. By mid-morning on day two, a clear pattern had emerged: incremental row reweighting and targeted data hygiene routinely produced larger uplifts than wholesale expansions of any single corpus. Teams responded by tightening their loops (reducing blend size, pruning redundant rows, and experimenting with lightweight prompt templates) to capitalize on these findings before the final evaluation window closed.

Teams documented recipe logic, weights, preprocessing steps, and links to artifacts in the EmbedSim Dataset Portal DataCards to ensure full reproducibility beyond leaderboard metrics.

## Illustrative Solutions and Results

Two blends stood out in the final leaderboard and highlighted distinct yet complementary paths to improvement.

The first, produced by Mix Masters, won the New‑Use‑Case track with SportsScribe—a tennis recap assistant. The blend emphasized 85% Tennis Summarization for event context, 10% SLM4NPC for persona‑driven dialogue, and 5% RLHF Workflow 1 for multi‑step reasoning, with text normalization and deduplication; the team reported a small HellaSwag uplift and a demo‑ready recap format.

The second winning blend came from Datablenders, which topped the Beat‑the‑Baseline track. They incrementally reweighted RLHF Workflow 1 with both RLHF Simplified variants and added targeted synthetic slices, achieving an aggregate 38.91 with per‑benchmark gains (MMLU 56.2, HellaSwag 51.8, HumanEval 8.74) versus their selected baselines under the 10k‑row cap.

Runner‑up efforts reinforced the same themes. Total Data Island emphasized NeMo Curator cleaning and targeted synthetic code slices, reporting an increase on HumanEval from 8.15 to 9.28 in their best run. Finding NeMo combined SLM4NPC, RLHF, 9K Audio Caption, and controlled code QA augmentation via EmbedSim/Perplexity. They noted that adding 450 additional code QA pairs in Run 4 reduced MMLU (−0.4) and HumanEval (−0.14) relative to Run 3, indicating diminishing returns from larger synthetic additions. Taken together, these results confirm that modest, well-reasoned adjustments - rather than wholesale data expansion - deliver the most reliable returns under the challenge’s time and resource constraints.


## Operational Insights Drawn from 102 Submissions

A close examination of the full submission record reveals several patterns that are likely to generalize beyond this single event. The first and most consistent finding concerns iteration speed. Rapid iterate‑and‑measure cycles, captured in live telemetry and a narrow 0.17 SD, correlated with faster convergence to high‑leverage recipes within the two‑day window. In practice, rapid feedback allowed the faster groups to detect when a blend plateaued after one or two evaluation cycles and to redirect their effort toward fresh configurations rather than refining an approach that showed limited early promise.

A second observation involves the composition of each blend. Winning and top‑performing blends typically combined 3–9 slices (average ~5–6). The advantage stemmed from the additional coverage and perspective introduced by smaller, diverse slices without diluting their individual signal. As teams discovered, inserting even a modest number of rows that addressed a clearly identified gap-conversational tone, domain-specific terminology, or step-by-step reasoning-often yielded larger aggregate gains than attempting to enlarge an already familiar dataset.

Data hygiene also emerged as a low-cost but high-return practice. For code‑reasoning, keeping synthetic slices under ~15% of tokens yielded gains up to ~1 percentage point, while exceeding ~30% often reversed gains under fixed hyper‑parameters. Simple measures such as duplicate removal and consistent row normalization, carried out before upload, translated directly into cleaner gradient signals during fine-tuning and, ultimately, more stable benchmark scores. Because the submission platform imposed fixed hyper-parameters and compute budgets, blends burdened with redundant or conflicting examples offered no compensatory benefit and, in several cases, actually suppressed performance relative to leaner alternatives.


## Quantitative Summary and Performance Patterns

Across 102 submissions, the mean aggregate score was 38.66 with a 0.17 standard deviation, indicating rapid convergence under fixed hyper‑parameters and a 10,000‑row cap. Top blends achieved +1.20 pp on MMLU and +1.13 pp on HumanEval. Three of seven teams surpassed every baseline and all seven beat at least two baselines, with lean blends combining roughly 3–9 slices (average ~5–6) and strong cleaning/dedup outperforming larger, noisier mixes. Synthetic augmentation delivered lift when kept under ~15% token share, while increases beyond ~30% often degraded performance.

## Impact, Adoption, and Next Steps

The outcomes of the Data Blending Challenge are already influencing both day-to-day operations and longer-term project planning.Immediately after the event, the team consolidated top blends into a curated library with per‑entry slice lists, weights, preprocessing scripts, and DataCards (recipe logic and artifact links) to enable exact reruns and downstream adoption.

The challenge demonstrated that disciplined recombination of existing assets can deliver measurable performance improvements and new product capabilities within a constrained time frame and compute budget. By integrating these practices into standard workflows and validating across additional domains, the organization can continue to realize returns from existing datasets.

