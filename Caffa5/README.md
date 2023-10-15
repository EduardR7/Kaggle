![image](https://github.com/EduardR7/Kaggle/assets/126398449/99993ec8-f26c-4426-acd4-76081b040f72)
# CAFA 5 Protein Function Prediction 
*Обзор и анализ источников*

##### В этой ветке приведен код который использован мной в соревновании CAFA5, Kaggle. Наша команда предварительно заняла 103 место, бронзовая медаль. Окончательные итоги будут приведены после 22 декабря 2023 года.

## [Обзор соревнования](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/overview)
>  Цель соревнования
>  Цель этого конкурса - предсказать функцию (терм) набора белков. Участники конкурса разрабатывают модель, обученную на основе аминокислотных последовательностей белков и других данных. Работа участников поможет исследователям микробиологам лучше понять функцию белков, и то, как работают клетки, ткани и органы. Это также может помочь в разработке новых лекарств и методов лечения различных заболеваний.

## Dataset Background

>  Каждая генная цепочка связана с определенными функциями. Эти функции кодируются в базах, в данном соревновании принята Gene Ontology (GO) база.

>  GO — ориентированный ациклический граф. Узлы в этом графе представляют собой функциональные дескрипторы (термы), связанные между собой реляционными связями (is_a, part_of и т. д.). Например, термины «активность связывания белка» и «активность связывания» связаны отношением is_a; однако край на графике часто переворачивается, указывая от связывания к связыванию с белком. Этот граф содержит три подграфа (субонтологии): молекулярная функция (MFO), биологический процесс (BPO) и клеточный компонент (CCO), определенные их корневыми узлами. С биологической точки зрения каждый подграф представляет собой отдельный аспект функции белка: что он делает на молекулярном уровне (MF), в каких биологических процессах участвует (BP) и где в клетке он расположен (CC).

>  В качестве входных условий задачи было предоставлено 141864 уникальных протеиновых цепочек, 20996 уникальный термов GO, минимальная длина цепочки – 53 


##  Files

More details is available on [competition data page](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/data).

| File | Contents |
|:---:|---|
|**train_sequences.fasta**|amino acid sequences for proteins in training set|
|**train_terms.tsv**|the training set of proteins and corresponding annotated GO terms|
|**train_taxonomy.tsv**|taxon ID for proteins in training set|
|**go-basic.obo**|ontology graph structure|
|**testsuperset.fasta**|amino acid sequences for proteins on which the predictions should be made|
|**testsuperset-taxon-list.tsv**|taxon ID for proteins in test superset (Note: you may need to use `encoding="ISO-8859-1"` to read this file in `pandas`)|
|**IA.txt** |Information Accretion for each term. This is used to weight precision and recall (see Evaluation)|
|**sample_submission.csv**|a sample submission file in the correct format|

## Protein Sequences Embedding (From discussion)

1.  ProtVec (word2vec) : Continuous distributed representation of biological sequences for deep proteomics and genomics. [https://arxiv.org/abs/1503.05140](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/url)
2.  SeqVec (ELMo) : Modeling aspects of the language of life through transfer-learning protein sequences. [https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-019-3220-8](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/url)
3.  ESM‐1b (Transformer) : TRANSFORMER PROTEIN LANGUAGE MODELS ARE  
    UNSUPERVISED STRUCTURE LEARNERS. [https://openreview.net/pdf?id=fylclEqgvgd](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/url)
4.  ProtTrans (BERT) : Towards cracking the language of life’s code through self-supervised deep  
    learning and high performance computing. [https://arxiv.org/abs/2007.06225](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/url)
5.  UDSMProt (AWD‐LSTM) : Universal deep sequence models for protein classification. [https://academic.oup.com/bioinformatics/article/36/8/2401/5698270](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/url)
6.  UniRep (mLSTM) : Unified rational protein engineering with sequence-based deep representation learning. [https://www.nature.com/articles/s41592-019-0598-1](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/discussion/url)


## What is Gene Onthology (GO)

Gene Ontology (GO) is a widely used resource in bioinformatics that provides structured and standardized descriptions of genes and their associated biological functions, cellular components, and molecular processes. It serves as a controlled vocabulary to annotate and characterize genes and gene products across different organisms.

The Gene Ontology Consortium develops and maintains GO, and it consists of three main categories or branches:

| Categories or Branches | Abstruct |
|:---:|---|
|**Biological Process (BP)**|This branch describes the series of events or activities that occur within a cell or an organism, contributing to a specific biological function. <br>Examples of biological processes include cell division, metabolism, signal transduction, and immune response.|
|**Cellular Component (CC)**|This branch represents the subcellular structures, locations, and complexes where gene products are active or present.<br> Examples of cellular components include the nucleus, mitochondria, cytoskeleton, and plasma membrane.|
|**Molecular Function (MF)**|This branch describes the specific biochemical activities or properties of gene products, such as catalytic or binding activities.<br> Examples of molecular functions include enzyme activity, receptor binding, DNA binding, and transporter activity.|

The GO terms are organized in a hierarchical structure, with broader terms at the top and more specific terms at the lower levels. This hierarchical structure allows for the representation of relationships between different terms. Additionally, each term is assigned a unique identifier, allowing researchers to refer to specific terms in their analyses.

Gene Ontology analysis involves the systematic examination of gene lists or expression data to uncover functional annotations, biological themes, and relationships within the data. It helps researchers make sense of large-scale genomic or transcriptomic datasets and gain insights into the underlying biology.
