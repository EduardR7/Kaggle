![image alt="drawing" width="100"](https://github.com/EduardR7/Kaggle/assets/126398449/300f0d2a-861b-4602-908e-a9d63364da77)
## [CAFA 5 Protein Function Prediction, leaderboard](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/leaderboard)

##### Наша команда предварительно заняла 103 место из 1675, бронзовая медаль. Окончательные итоги будут приведены после 22 декабря 2023 года.

## [1. Цель конкурса](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/overview)
>  Цель этого конкурса - предсказать функцию (терм) набора белков. Участники конкурса разрабатывают модель, обученную на основе аминокислотных последовательностей белков и других данных. Работа участников поможет исследователям микробиологам лучше понять функцию белков, и то, как работают клетки, ткани и органы. Это также может помочь в разработке новых лекарств и методов лечения различных заболеваний.

##  2.	Основные моменты решения

>  Для оценки качества предсказания использовалась нестандартная метрика – F-мера. Код приводился в [GitHub](https://github.com/BioComputingUP/CAFA-evaluator). Большее значение меры соответствовало более высокому месту на Leaderboard

>  Набором признаков, X_train на начальном этапе обучения являлись генные последовательности train_taxonomy.csv. Далее эти последовательности обрабатывались LLM языковыми моделями (на основе Keras/Tensorflow, PyTorch) для получения предсказаний и эмбедингов последнего скрытого слоя. Так как существуют общепризнанные эмбединги для генных последовательностей, выполненные с помощью пакетов предоученных специализированных пакетов T5 и ProtBert, в целях оптимизации времени обучения, на соревновании использовались и загружались именно эти готовые эмбединги (без загрузки - train_sequences.fasta, train_terms.tsv, train_taxonomy.tsv. 
>  Лучшие результаты показали эмбединги пакетов T5 и в меньшей степени – ProtBert.
>  В качестве оптимайзера лучшие результаты показали [Sophia](https://github.com/kyegomez/Sophia), и известный алгоритм Adam.
>  Правилами соревнований допускалось использовать эмбединги опубликованные в общем доступе и сгенерированные самостоятельно. Так как тест был открыт на этом соревновании, впоследствии участниками до обучались и использовались другие эмбединги в формате Numpy массивов. Они также использовались мной как входные данные X_train.
>  Для прохода по графу GO создан отдельный класс, с учетом ограничений по памяти, специализированные пакеты faiss, annoy не импортировались.
>  Для получения приемлемых сроков расчета использовался GPU.
>  Ограничения по памяти в Kaggle – GPU – 12ГБ, CPU – 18ГБ.
>  Выходной файл submission – 300 до 1500МБ
>  В финальной стадии активно использовался блендинг.


##  3. Личный объем участия

>  В самостоятельно части соревнования я корректировал блокнот и подготавливал эмбединги для дальнейшей оптимизации. Для расчета использовались ноутбуки на основе baseline организаторов и других участников, доработанные с учетом собственного понимания оптимального решения.
>  Для получения более широкого спектра результатов, подходящих для финального блендинга, я использовал нестандартные соотношения GO namespaces, отличные от - {'BPO': 1100, 'MFO': 450, 'CCO': 300}. Данные соотношения принимались как submission файлы, давали хороший скор на LB (Leaderboard), однако, при проведении финального блендинга было необходимо привести их к общему виду.
>  Для этого я подготовил [расчетный блокнот], который обеспечивал конвертацию и приведение файлов с нестандартными соотношениями namespaces к общему виду и их последующий блендинг.
>  В ходе соревнования, один из моих скорингов, оказался лучшим для нашей команды и обеспечил бронзовую медаль в предварительной части, с public test.
Окончательный результат будет объявлен в декабре, когда компания CAFA проведет полный цикл обследований и получит полный (private) тестовый набор.


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
