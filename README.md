# MetagenomicClassifier-KGI

## Contributors
* Ryan Fue* - Dept of Mathematics UC Los Angeles, Los Angeles CA 90095
* Joshua Barrow* - Donald Bren School of Information and Computer Sciences UC Irvine, Irvine CA 92697
* J. Cesar Ignacio-Espinoza - Riggs School of Life Sciences, Keck Graduate Institute, Claremont CA 91711

*Both students contributed equally to this work, which was conducted as part of a summer research experience at KGI.


## Abstract
Microbial communities, such as those found in the gut or the ocean, play a crucial role in digestion, oxygen production, and numerous other biological processes. However, our understanding of microorganisms in these communities remains limited due to cultivation bias, which limits our ability to grow specific bacteria and their associated viruses in the lab. Metagenomics, the sequencing of entire microbial communities, has emerged as a way to circumvent this limitation[1]. Yet, efficiently and accurately classifying metagenomic sequences remains a major challenge. 

Here, we apply a pre-trained protein language model (ESM-META)[2] to generate protein-level vector representations (embeddings), hypothesizing that some embedding dimensions encode taxonomic signals. These embeddings are then used as input for several machine learning classifiers aimed at delivering a binary virus/bacteria prediction. 

All models achieved over 95% accuracy when genome fragments contained at least 10 proteins, demonstrating the utility of our approach. Additionally, to better reflect fragment sizes commonly recovered from metagenomic datasets, we simulated shorter fragments, and logistic regression consistently outperformed other methods, achieving an accuracy of 90% even with a single-protein input. 

Overall, our results highlight a promising approach for accurately discriminating metagenomic sequences, with the potential to be extended for more granular classifications beyond a binary output.

## Introduction
Transformer-based language models[3] have revolutionized modern science and are now widely applied in biology, including genomic and protein language models.

These models are trained to predict missing or next words by learning the rules of a text corpus. During training, they capture the semantic meaning of words as vector representations (Figure 1). For example, words with related contextual properties, such as gender or grammatical role, are placed near each other in this vector space.

Similarly, protein language models can learn biological properties such as cellular localization and structural features.

<img width="1055" height="418" alt="image" src="https://github.com/user-attachments/assets/343a32b0-4ce6-4f95-9888-d3748295a481" />
<small> Figure 1. Transformer-based language models for natural language and protein sequences. Transformers process input sequences by encoding tokens as vectors and refining their relationships through attention mechanisms (left). Word embeddings can capture semantic properties such as size (green) or gender (yellow) (top right). Similarly, protein language models learn biologically relevant features, including cellular localization and structural properties (bottom right). These learned representations can distinguish context-dependent meanings (e.g., bat as an animal vs. bat in sports) and may also capture taxonomic signals, enabling the separation of protein sequences from complex metagenomes. </small>


#### We hypothesize that these learned representations also capture taxonomic information, allowing discrimination of protein sequences from complex metagenomic samples.


## Methods

<img width="1213" height="339" alt="image" src="https://github.com/user-attachments/assets/81af8c15-d0c9-4a09-b9df-29b23cf51a45" />


## Results

Initial UMAP dimensionality reduction of protein language model (PLM) vector representations (input vector size = 1280) for 300,000 protein sequences clustered by genome into about 1,000 mean embeddings revealed a clear separation between viral and bacterial sequences (Figure 2). This demonstrates that taxonomic information is captured and retained by the model, forming a strong separator in protein sequence space. These findings pave the way for the binary classification of metagenomic protein sequences and open the possibility of discovering novel viral sequences.

<img width="930" height="639" alt="image" src="https://github.com/user-attachments/assets/d7041a5a-986a-422d-9dbc-2e8ecb07e2df" />

<small> Figure 2. UMAP visualization of protein embeddings. UMAP projection of PLM-derived embeddings showing viral sequences (red) and bacterial sequences (blue). The distinct clustering indicates that the model encodes taxonomic signals, enabling discrimination of viral and bacterial proteins within complex metagenomic datasets. </small>

Given that the vector representation of protein sequences captures meaningful biological patterns, we sought to develop a proof-of-concept binary classification algorithm. We implemented several classification methods, among which logistic regression outperformed all others (Figure 3). Finally, we simulated metagenomic data using genome fragments containing between one and twenty genes to assess the discriminative power of our method. We found that the taxonomic signal from the embeddings was strong enough to achieve 95% classification accuracy when 10 genes were included."

<img width="1102" height="539" alt="image" src="https://github.com/user-attachments/assets/20177f3a-ca87-482f-8f22-b8c5cec57814" />

<small> Figure 3. Performance of classification models for taxonomic discrimination using protein sequence embeddings. (A) Confusion matrix for the logistic regression model showing strong separation between viral and bacterial sequences, with minimal misclassification. (B) Heatmap of classification accuracy for four algorithms (KNN, Random Forest, Logistic Regression, and Support Vector Classifier) as a function of the number of genes per simulated genome fragment (1–23). Accuracy increases with fragment size, with logistic regression consistently outperforming other models. (C) ROC curve for four algorithms (KNN, Random Forest, Logistic Regression, and Support Vector Classifier). High ROC AUC score for all models with logistic regression performing the best </small>

## Conclusions 

Our work demonstrates the utility of protein language models (PLMs) for classifying metagenomic sequences. While this proof-of-concept is based on a binary classifier, its modular and scalable design allows for potential expansion to more granular, multi-class classification tasks. Finally, we predict that fine-tuning the PLM could enable the discovery of novel viral sequences with only distant homologs in existing databases.

## Acknowledgements

We would like to thank Prof. Angelika Niemz for her guidance, support, and daily check-ins throughout our summer internship, as well as for running and maintaining the summer internship program. We also extend our gratitude to the Laguna CARC-USC HPC system and its team, without their existence and the access they provide, this work would not have been possible. 

## References

[1] Handelsman, J., et al. "Molecular biological access to uncultivated microorganisms: a review." Applied and Environmental Microbiology 64.9 (1998): 3480–3488. [2] Zeming Lin et al., Evolutionary-scale prediction of atomic-level protein structure with a language model.Science379,1123-1130(2023). [3] Vaswani, A., et al. Attention is all you need. Advances in neural information processing systems, 30 (2017) [4] Pedregosa, F., et al. Scikit-learn: Machine Learning in Python. The Journal of Machine Learning Research, Volume 1 Pages 2825 - 2830 (2011)








