# Automated Requirement Tracing Using Term Extraction and Text Categorization

Master's research project in Software Engineering, University of Mosul (2015).
Tool built in **Java**. Evaluated on two NASA benchmark datasets: **MODIS** and **CM1**.

> **Note:** This repository contains the project summary, results and conclusions. Source code is not included.

## Overview

As software requirements change, analysts must find which design elements and code are affected (change impact analysis). This depends on **requirement tracing**: creating and maintaining links between requirements and design artifacts. Doing this manually is slow and error-prone.

This project automates the linking of unstructured text artifacts (requirements to design elements) using text-mining and information retrieval techniques, with the aim of improving the accuracy of the generated links and saving analyst time.

## Data

| Dataset | Source | Use |
|---|---|---|
| MODIS | NASA | Requirements traced to design elements (19 high-level requirements, 49 design elements) |
| CM1 | NASA | Second dataset used to check the findings |

## Method

1. **Text preprocessing:** stemming with the Porter algorithm and with a dictionary-based stemming approach (proposed in this work).
2. **Input formats:** two new text formats, *Statistical* and *Linguistic*, compared with the baseline *XML* format used in earlier research.
3. **Term weighting and feature selection:** more than 10 metrics compared, including TF-IDF, corpus term frequency, logged term frequency, document term frequency, document term counts, Information Gain and Chi-square.
4. **Similarity measures:** Cosine, Jaccard and Dice.
5. **Filtering:** similarity thresholds (0.2 and 0.25 for MODIS; 0 and 0.05 for CM1).
6. **Relevance feedback:** iterative improvement of the links (iterations 0 to 8).
7. **Evaluation:** Precision and Recall, compared with results published in earlier research. The tool also generates a requirements traceability matrix (RTM) and a traceability report listing requirements with no linked design elements.

## Selected results (MODIS, similarity filter 0.2 and 0.25)

Values are percentages. The baseline is the earlier published result.

| Metric | Recall (0.2) | Precision (0.2) | Recall (0.25) | Precision (0.25) |
|---|---|---|---|---|
| Baseline (XML format) | 19.5 | 21.6 | 19.5 | 32.0 |
| TF-IDF | 14.6 | **100.0** | 12.1 | **100.0** |
| Corpus Term Frequency | 68.2 | 21.8 | 65.8 | 31.0 |
| Document Terms Counts | **70.7** | 22.1 | **70.7** | 32.8 |
| Information Gain | 41.4 | 66.6 | 29.2 | **100.0** |
| Chi-square | 41.4 | 52.6 | 29.2 | **100.0** |

## Results with relevance feedback (MODIS)

| Metric | Recall (iter. 0) | Precision (iter. 0) | Recall (iter. 8) | Precision (iter. 8) |
|---|---|---|---|---|
| Baseline | 0.415 | 0.185 | 0.829 | 0.872 |
| TF-IDF | 0.268 | 0.500 | 1.000 | 0.830 |
| Document Terms Counts | 0.707 | 0.183 | 0.999 | 0.272 |
| Chi-square | 0.682 | 0.379 | 1.000 | 0.564 |

## Conclusions

- **Recall improved strongly.** On MODIS, recall rose from 19.5% to 70.7% (Document Terms Counts) compared with the earlier published result. With relevance feedback, recall reached about 1.0 on both datasets.
- **Cosine similarity gave the best recall and Jaccard the best precision**, on both MODIS and CM1.
- **Precision and recall trade off.** TF-IDF, Information Gain and Chi-square reached up to 100% precision at higher thresholds but with lower recall, while the term-frequency metrics gave high recall with lower precision. After relevance feedback, recall was higher than the baseline but precision was lower.
- **The choice of stemming method (Porter or dictionary-based) had little effect on recall**; the dictionary-based approach gave slightly better precision on MODIS.
- **No single metric was best on every measure**, so the best choice depends on whether the analyst needs completeness (recall) or fewer false links (precision).
- Most recall and precision values in the comparison were better than those in earlier published research.

## Future work

- Extend tracing across more than two life-cycle stages (requirements, design and source code).
- Add further enhancement approaches in addition to relevance feedback.
- Test other information retrieval models in addition to the Vector Space Model.
- Try other (non-IR) techniques instead of information retrieval.

## Publications

- *Requirement Tracing Using Term Extraction*, International Journal of Computer Science and Information Security, Vol. 13, No. 5, 2015.
- *Requirement Tracing Using Feature Selection Metric*, International Journal of Recent Research and Review, Vol. XIII, Issue 3, September 2020.

## Skills demonstrated

Text preprocessing, feature selection, similarity measures, information retrieval, experimental design, evaluation with Precision and Recall, comparison against published baselines, Java.
