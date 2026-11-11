# Corpus d'articles sur la compression et l'interprétabilité des modèles IA


## Plan de rédaction proposé

1. Introduction et motivations : coût des grands modèles, déploiement embarqué, énergie, besoin de confiance.
2. Taxonomie de la réduction de modèle
    1. Quantification : post-training (PTQ) vs entraînement conscient de la quantification (QAT) ; poids seuls vs poids et activations ; 8/4/2 bits, ternaire, formats FP8/FP4.
    2. Élagage : non structuré, structuré, semi-structuré 2:4 ; critères (magnitude, second ordre) ; hypothèse du ticket de loterie.
    3. Distillation : sur les logits, sur les représentations intermédiaires, boîte noire vs boîte blanche, distillation de LLM.
    4. Autres : rang faible, recherche d’architecture (NAS), mixture of experts, sortie anticipée.
    5. Combinaisons, par exemple élagage puis distillation, ou distillation puis quantification.
3. Évaluation de la compression : métriques, benchmarks, écart entre gains théoriques et gains réels sur le matériel.
4. Interprétabilité
    1. Définitions et taxonomie : intrinsèque vs post-hoc, locale vs globale.
    2. Méthodes d’attribution : LIME, SHAP, gradients intégrés, Grad-CAM, et leurs limites.
    3. Méthodes par concepts : TCAV, probing.
    4. Interprétabilité mécaniste : circuits, superposition, autoencodeurs parcimonieux (SAE).
5. Croisement compression × interprétabilité : ce que les modèles compressés « oublient », stabilité des explications, compression comme outil d’interprétation.
6. Pratiques actuelles : ce qui est réellement déployé, et pourquoi.
7. Verrous et perspectives.


## Articles recommandés

### Surveys pour démarrer

- Cheng et al. (2017), A Survey of Model Compression and Acceleration for Deep Neural Networks.
- Zhu et al. (2023), A Survey on Model Compression for Large Language Models, arXiv 2308.07633 : couvre quantification, élagage, distillation et factorisation de rang faible appliqués aux LLM.
- Liu et al. (2025), A survey of model compression techniques: past, present, and future, Frontiers in Robotics and AI : retrace l’évolution historique de ces techniques et discute des pistes comme l’élagage sans réentraînement.
- Girija et al. (2025), Optimizing LLMs for Resource-Constrained Environments, IEEE COMPSAC : orienté déploiement embarqué, avec aussi les mixtures d’experts et la sortie anticipée.

### Quantification

- Jacob et al. (2018), Quantization and Training of Neural Networks for Efficient Integer-Arithmetic-Only Inference, CVPR. Fondateur pour l’INT8.
- Nagel et al. (2021), A White Paper on Neural Network Quantization, Qualcomm. Très pédagogique.
- Gholami et al. (2021), A Survey of Quantization Methods for Efficient Neural Network Inference.
- Dettmers et al. (2022), LLM.int8(). Introduit le problème des activations aberrantes (outliers).
- Frantar et al. (2023), GPTQ, ICLR.
- Xiao et al. (2023), SmoothQuant, ICML.
- Lin et al. (2024), AWQ, MLSys.
- Dettmers et al. (2023), QLoRA.
- Ma et al. (2024), The Era of 1-bit LLMs (BitNet b1.58).

### Élagage

- LeCun et al. (1990), Optimal Brain Damage.
- Han et al. (2015/2016), Learning both Weights and Connections et Deep Compression.
- Frankle & Carbin (2019), The Lottery Ticket Hypothesis, ICLR.
- Blalock et al. (2020), What is the State of Neural Network Pruning? Critique méthodologique essentielle.
- Hoefler et al. (2021), Sparsity in Deep Learning. Survey très complet.
- Frantar & Alistarh (2023), SparseGPT.
- Sun et al. (2024), Wanda: A Simple and Effective Pruning Approach for LLMs.
- Ma et al. (2023), LLM-Pruner.
- Xia et al. (2024), Sheared LLaMA.

### Distillation

- Hinton, Vinyals & Dean (2015), Distilling the Knowledge in a Neural Network.
- Romero et al. (2015), FitNets.
- Sanh et al. (2019), DistilBERT.
- Jiao et al. (2020), TinyBERT.
- Gou et al. (2021), Knowledge Distillation: A Survey.
- Gu et al. (2024), MiniLLM.
- Agarwal et al. (2024), On-Policy Distillation of Language Models (GKD).
- Xu et al. (2024), A Survey on Knowledge Distillation of Large Language Models.
- Muralidharan et al. (2024), Compact Language Models via Pruning and Knowledge Distillation (Minitron). Très représentatif de la pratique industrielle.

### Interprétabilité : fondements et post-hoc

- Doshi-Velez & Kim (2017), Towards a Rigorous Science of Interpretable Machine Learning.
- Lipton (2018), The Mythos of Model Interpretability.
- Ribeiro et al. (2016), LIME.
- Lundberg & Lee (2017), SHAP.
- Sundararajan et al. (2017), Integrated Gradients.
- Selvaraju et al. (2017), Grad-CAM.
- Adebayo et al. (2018), Sanity Checks for Saliency Maps. Indispensable pour discuter des limites.
- Kim et al. (2018), TCAV.

### Interprétabilité mécaniste

- Olah et al. (2020), Zoom In: An Introduction to Circuits, Distill.
- Elhage et al. (2021), A Mathematical Framework for Transformer Circuits.
- Elhage et al. (2022), Toy Models of Superposition.
- Wang et al. (2023), Interpretability in the Wild (circuit IOI).
- Meng et al. (2022), Locating and Editing Factual Associations in GPT (ROME).
- Bricken et al. (2023), Towards Monosemanticity, et Templeton et al. (2024), Scaling Monosemanticity. Les autoencodeurs parcimonieux.
- Bereska & Gavves (2024), Mechanistic Interpretability for AI Safety — A Review.
- Sharkey et al. (2025), Open Problems in Mechanistic Interpretability, TMLR : organise les problèmes ouverts en trois catégories : méthodologiques, applicatifs et socio-techniques. Excellent pour ta partie « perspectives ».

### Croisement compression × interprétabilité

- Hooker et al. (2019/2020), What Do Compressed Deep Neural Networks Forget? Montre que la compression dégrade de façon disproportionnée certains exemples et sous-groupes. À lire absolument.
- Gupte et al. (2025), On the transferability of Sparse Autoencoders for interpreting compressed models, arXiv 2507.15977.
- Rabbi et al. (2026), Same Predictions, Different Reasons: The Effect of Quantization on Model Explanations, arXiv 2607.22872 : compare Grad-CAM et LIME sur cinq architectures CNN en INT8 et INT4.
- arXiv 2504.02010 (2025), sur les modèles de raisonnement compressés : l’analyse identifie la projection MLP de la dernière couche comme un composant critique, et la protéger améliore nettement les résultats de la quantification. Un bon exemple d’interprétabilité mise au service de la compression.
