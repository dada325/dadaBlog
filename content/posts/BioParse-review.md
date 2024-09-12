---
title: "BiomedParse Review"
date: 2024-06-06T12:54:20+08:00
# weight: 1
# aliases: ["/first"]
tags: ["LLM"]
author: dada
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: ""
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## BiomedParse

## 1. Model Selection and Architecture

BiomedParse is a transformer-based language model specifically designed for parsing biomedical text into structured representations. The key architectural choices are:

- Using a pre-trained BERT (Bidirectional Encoder Representations from Transformers) model as the backbone, which has shown strong performance on various natural language processing tasks. BERT is a deep bidirectional transformer that learns contextual word representations by jointly conditioning on both left and right context.

- Fine-tuning the pre-trained BERT model on a large corpus of biomedical text (PubMed abstracts and PMC full-text articles) to adapt it to the biomedical domain. This domain-specific pre-training allows the model to learn the unique vocabulary, grammar, and semantic relationships in biomedical literature.

- Adding a token classification head on top of the BERT encoder to predict the entity labels (e.g., gene, disease, drug) for each input token. The token classification head is a linear layer followed by a softmax activation, which outputs the probability distribution over the entity labels.

- Adding a relation classification head to predict the relations (e.g., gene-disease association, drug-drug interaction) between pairs of entities. The relation classification head takes the concatenated entity representations as input and outputs the probability distribution over the relation types.

- Jointly training the entity and relation classification heads using a multi-task learning objective, which combines the cross-entropy losses for both tasks. This joint training allows the model to learn the interactions between entities and relations and improve the overall parsing performance.

The transformer architecture allows BiomedParse to capture long-range dependencies and complex semantic relationships in biomedical text, while the domain-specific pre-training and multi-task learning enable it to adapt to the unique characteristics of biomedical literature.

## 2. Data Handling and Preprocessing

BiomedParse was trained on a large corpus of biomedical text, including:

- 14 million PubMed abstracts (3.2 billion words)
- 2.7 million PMC full-text articles (7.5 billion words)

The key preprocessing steps were:

- Tokenizing the text into subword units using the WordPiece tokenizer, which splits words into smaller units based on their frequency in the corpus. This allows the model to handle out-of-vocabulary words and capture morphological patterns.

- Representing each input sequence as a sequence of token IDs, along with special tokens like [CLS] (classification token) and [SEP] (separator token) to demarcate the sequence boundaries.

- Creating entity labels for each token using the BIO (Beginning-Inside-Outside) tagging scheme, where 'B' denotes the beginning of an entity, 'I' denotes the inside of an entity, and 'O' denotes outside of an entity. The entity labels were obtained from existing biomedical named entity recognition datasets.

- Creating relation labels for each pair of entities in the input sequence, based on existing biomedical relation extraction datasets. The relation labels were represented as a binary matrix, where each cell indicates the presence or absence of a relation between two entities.

The preprocessed data was split into training, validation, and test sets for model development and evaluation. No data augmentation was used, as the large size of the training corpus was deemed sufficient for learning robust representations.

## 3. Training Process

BiomedParse was trained using a two-stage process: pre-training on the biomedical corpus, followed by fine-tuning on the entity and relation classification tasks. The key training details are:

- For pre-training, the model was trained using the masked language modeling (MLM) objective, where a random subset of the input tokens are masked and the model learns to predict the original tokens based on the surrounding context. This allows the model to learn bidirectional representations that capture the semantic relationships between words.

- The pre-training was done for 1 million steps with a batch size of 256 sequences, using the Adam optimizer with a learning rate of 1e-4. The model was trained on 8 NVIDIA V100 GPUs for approximately 2 weeks.

- For fine-tuning, the pre-trained model was further trained on the entity and relation classification tasks using the labeled datasets. The entity classification head was trained using the cross-entropy loss between the predicted and true entity labels, while the relation classification head was trained using the binary cross-entropy loss between the predicted and true relation labels.

- The fine-tuning was done for 10 epochs with a batch size of 32 sequences, using the Adam optimizer with a learning rate of 5e-5. The model was fine-tuned on a single NVIDIA V100 GPU for approximately 1 day.

- Hyperparameter tuning was performed using grid search over the learning rate, batch size, and number of fine-tuning epochs, based on the performance on the validation set.

The two-stage training process allows BiomedParse to leverage the large unlabeled biomedical corpus for learning general-purpose representations, while still being able to adapt to the specific entity and relation classification tasks using the labeled datasets.

## 4. Model Performance and Evaluation

BiomedParse was evaluated on several benchmark datasets for biomedical named entity recognition (NER) and relation extraction (RE), including:

- BC5CDR (NER and RE for chemicals and diseases)
- NCBI-Disease (NER for diseases)
- BC2GM (NER for genes and proteins)
- BioCreative VI ChemProt (RE for chemical-protein interactions)

The key evaluation metrics were:

- Precision: the fraction of predicted entities/relations that are correct
- Recall: the fraction of true entities/relations that are predicted
- F1 score: the harmonic mean of precision and recall

BiomedParse achieved state-of-the-art performance on all benchmark datasets, with F1 scores ranging from 87.2% to 91.5% for NER and 76.3% to 83.1% for RE. This represents an improvement of 2-5 percentage points over previous methods based on BiLSTM-CRF (Bidirectional Long Short-Term Memory with Conditional Random Field) and rule-based systems.

Ablation studies showed that both the domain-specific pre-training and multi-task learning contributed significantly to the model's performance, with pre-training providing a larger boost than multi-task learning. The model's performance was also robust to the choice of hyperparameters, with similar results obtained across a range of learning rates and batch sizes.

## 5. Biological Relevance and Interpretation

BiomedParse learns biologically meaningful representations of biomedical entities and their relationships, as evidenced by its ability to accurately extract them from raw text. Some key observations are:

- The model can recognize a wide range of biomedical entities, including genes, proteins, drugs, chemicals, and diseases, based on their textual descriptions. This suggests that the model has learned the relevant biological concepts and terminology.

- The model can identify complex relationships between entities, such as gene-disease associations, drug-drug interactions, and chemical-protein interactions. This demonstrates the model's ability to capture the underlying biological mechanisms and pathways.

- The model's predictions are largely consistent with existing biomedical knowledge bases, such as UniProt, DrugBank, and OMIM, which were used to create the training datasets. This provides external validation of the model's outputs.

- The attention weights of the transformer architecture can be visualized to interpret the model's predictions and identify the key words and phrases that contribute to each entity/relation. This can potentially provide new insights into the biological basis of the model's decisions.

However, as with all machine learning models, BiomedParse's predictions should be interpreted with caution and validated by expert human reviewers. The model may make errors or learn spurious correlations from the training data, and its outputs should be treated as hypotheses rather than definitive facts.

## 6. Computational Efficiency

BiomedParse is computationally efficient compared to traditional rule-based and feature-engineering approaches for biomedical text mining, thanks to the parallelizable architecture of the transformer model:

- The pre-training and fine-tuning can be efficiently distributed across multiple GPUs, allowing the model to be trained on large datasets in a reasonable amount of time (e.g., 2 weeks for pre-training and 1 day for fine-tuning).

- The inference time is fast, taking only a few seconds per abstract on a single GPU. This enables the model to be applied to large-scale literature mining tasks, such as extracting entities and relations from the entire PubMed database.

- The model's memory footprint is relatively small, requiring only a few gigabytes of GPU memory for inference. This makes it possible to deploy the model on standard hardware or cloud computing platforms.

However, the computational cost of training the model from scratch is still significant, requiring access to high-performance computing resources. Fine-tuning the model on new datasets or tasks is more affordable, but still requires some computational overhead.

## 7. Challenges and Limitations

Despite its strong performance and efficiency, BiomedParse has several challenges and limitations that need to be addressed in future work:

- The model's performance depends on the quality and coverage of the training datasets, which may not be representative of all biomedical subdomains or text genres. Expanding the training data to include more diverse sources, such as clinical notes, patents, and social media, could improve the model's generalizability.

- The model's outputs are limited to the entity and relation types that are defined in the training datasets, which may not capture all the relevant information in the text. Developing methods for open-ended information extraction, such as event extraction or knowledge graph construction, could provide a more comprehensive representation of the biomedical knowledge.

- The model's interpretability is limited by the complexity of the transformer architecture and the lack of explicit symbolic representations. Developing more transparent and explainable models, such as rule-based systems or knowledge-infused neural networks, could improve the trustworthiness and acceptability of the model's predictions.

- The model's ability to handle complex linguistic phenomena, such as negation, coreference, and hedging, is limited by the simplicity of the entity and relation classification tasks. Incorporating more sophisticated natural language understanding techniques, such as semantic parsing or discourse analysis, could improve the model's ability to extract accurate and nuanced information from the text.

Addressing these challenges will require a combination of technical innovations, such as new model architectures and training paradigms, as well as interdisciplinary collaborations between computer scientists, biomedical experts, and end users.

## 8. Future Directions and Improvements

There are many promising directions for extending and improving the BiomedParse model, including:

- Expanding the model to handle more diverse biomedical text genres, such as clinical notes, social media, and scientific figures, which may require different preprocessing, tokenization, and modeling techniques.

- Developing methods for open-ended information extraction, such as event extraction, knowledge graph construction, and summarization, which can provide a more comprehensive and structured representation of the biomedical knowledge.

- Incorporating domain knowledge and symbolic reasoning into the model, such as ontologies, rules, and constraints, which can improve the interpretability and robustness of the model's predictions.

- Exploring new model architectures and training paradigms, such as graph neural networks, adversarial learning, and reinforcement learning, which can capture more complex linguistic and semantic relationships in the text.

- Integrating the model with other biomedical data sources and tools, such as databases, ontologies, and visualization platforms, to enable end-to-end knowledge discovery and hypothesis generation.

- Developing user-friendly interfaces and workflows for biomedical researchers and clinicians to interact with the model and incorporate its outputs into their decision-making processes.

Ultimately, the goal is to develop BiomedParse into a powerful and reliable tool for extracting actionable insights from the vast amount of biomedical literature, and accelerating the pace of scientific discovery and clinical translation.

## 9. Conclusion

BiomedParse is a state-of-the-art transformer-based language model for biomedical text parsing, which achieves strong performance on named entity recognition and relation extraction tasks across multiple benchmark datasets. By leveraging domain-specific pre-training and multi-task learning, BiomedParse can learn biologically meaningful representations of biomedical entities and their relationships, and efficiently extract them from raw text.

The key strengths of BiomedParse are its ability to handle the complexity and diversity of biomedical language, its computational efficiency and scalability, and its potential for enabling large-scale literature mining and knowledge discovery. These strengths make BiomedParse a promising tool for accelerating biomedical research and clinical practice, by providing a more efficient and comprehensive way to access and integrate the knowledge contained in the biomedical literature.

However, BiomedParse also has important limitations and challenges, such as its dependence on the quality and coverage of the training data, its limited interpretability and explainability, and its inability to handle more complex linguistic and semantic phenomena. Addressing these limitations will require ongoing research and development efforts, as well as collaborations between the natural language processing and biomedical communities.

Despite these challenges, BiomedParse represents an exciting direction for advancing biomedical text mining and knowledge discovery, by leveraging the power of deep learning and natural language processing. As the model continues to evolve and improve, it has the potential to become a key enabling technology for data-driven biomedical research and precision medicine, helping to unlock the full value of the biomedical literature and accelerate the translation of scientific discoveries into clinical applications.
