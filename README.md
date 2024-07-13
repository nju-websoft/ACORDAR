# ACORDAR

ACORDAR is a test collection for ad hoc content-based dataset retrieval, which is the task of answering a keyword query with a ranked list of datasets. Keywords may point to the metadata and/or the data of a dataset. For details about the construction of this test collection, please refer to the following paper.

## Paper and Citation

Tengteng Lin, Qiaosheng Chen, Ruoqi Zhao, Qing Shi, Xiaxia Wang, Gong Cheng, Ahmet Soylu, Basil Ell, Yu Gu, Evgeny Kharlamov, Wei Hu, Yuzhong Qu. ACORDAR: A Test Collection for Ad Hoc Content-Based (RDF) Dataset Retrieval. Submitted to SIGIR 2022.

## Datasets

This test collection involves 31,589 RDF datasets collected from 543 data portals. The "./Data/datasets.json" file provides the ID and metadata of each dataset in JSON format. The dataset itself can be downloaded via the links in the download field, or from Zenodo: https://doi.org/10.5281/zenodo.6683710. We recommend using Apache Jena to parse the downloaded datasets.

## Queries

The "./Data/all_queries.txt" file contains 493 queries, one query per line, where each line has two tab-separated fields: query_id and query_text. The queries can be divided into synthetic queries created by our human annotators (see "./Data/synthetic_queries.txt") and TREC queries imported from the ad hoc topics (titles) used in the English Test Collections of TREC 1-8 (see "./Data/trec_queries.txt").

## Relevance Judgments

The "./Data/qrels.txt" file contains 10,671 relevance judgments in TREC's qrels format, one judgment per line, where each line has four tab-separated fields: query_id, iteration (always zero and not used), dataset_id, and relevancy (0: irrelevant; 1: partially relevant; 2: highly relevant).

## Splits for Cross-Validation

To allow comparable evaluation results, one should use the train-valid-test splits we provide for five-fold cross-validation. The "./Data/Splits for Cross Validation" folder has five sub-folders, one for each fold. In each sub-folder we provide three relevance judgment files as the training, validation, and test sets.

# Baselines

We evaluated four baseline retrieval models: TF-IDF based cosine similarity, BM25F, Fielded Sequential Dependence Model (FSDM), and Language Model using Dirichlet priors for smoothing (LMD). We ran them over an inverted index of four metadata fields (title, description, author, tags) and four data fields (literals, classes, properties, entities). Due to their unsupervised nature, in each fold we ignored the training set but employed the validation set for tuning field weights from 0 to 1 in 0.1 increments using grid search based on NDCG@10.

The "./Baselines" folder contains rankings outputted by the baselines in TREC's results format. Below we show the evaluation results averaged over the test sets in all the five folds. One can use trec_eval for evaluation.

|        | NDCG@5 | NDCG@10 | MAP@5  | MAP@10 |
| ------ | ------ | ------- | ------ | ------ |
| TF-IDF | 0.5088 | 0.5452  | 0.2871 | 0.3976 |
| BM25   | 0.5538 | 0.5877  | 0.3198 | 0.4358 |
| FSDM   | 0.5932 | 0.6151  | 0.3592 | 0.4602 |
| LMD    | 0.5465 | 0.5805  | 0.3266 | 0.4324 |

# Contact

Tengteng Lin (tengtenglin@smail.nju.edu.cn) and Gong Cheng (gcheng@nju.edu.cn)
