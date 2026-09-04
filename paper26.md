
#  Topics, papers, and supervisors

## Topic 1: AI Safety 

- **Supervisor** Gert
- **Paper** Verbalizable Representations Form a Global Workspace in Language Models (Anthropic, 2026)

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐
  
  - **Link :**   [Anthropic Transformer Circuits Thread](https://transformer-circuits.pub/2026/workspace/)
  - **Brief description :** This paper introduces the Jacobian Lens (J-lens), an interpretability method for identifying internal representations that a language model can verbalize. The corresponding set of representations, called J-space, appears to function as an internal workspace. The method estimates, for each layer, the average Jacobian mapping from that layer’s residual stream to the final residual stream, then transports an intermediate activation through this mapping and decodes it with the model’s normal unembedding to obtain vocabulary-level concepts. One particularly interesting result is that ablating J-space strongly affects tasks that require internal reasoning, while allowing the model to write out a chain-of-thought can partially reduce this dependence. This suggests that explicit chain-of-thought may act as an external scratchpad, allowing information that would otherwise need to be maintained internally in J-space to instead be stored in the token context. 
  - **How to reproduce :** First reproduce a small subset of the original Jacobian Lens experiments on an open-source language model using the authors' released implementation. Thus first fit a J-lens on a small open model, then reproduce the reasoning experiment comparing direct reasoning with explicit chain-of-thought reasoning under J-space ablation. Evaluate performance on a manageable reasoning benchmark such as GSM8K or a synthetic dataset. The basic question is whether explicit chain-of-thought makes reasoning less sensitive to interventions on J-space.
  - **How to extend :**  Investigate whether there is a measurable trade-off between information represented in chain-of-thought and information represented internally in J-space. The hypothesis is that when an intermediate reasoning variable is explicitly written into the context, the model no longer needs to maintain that same information as strongly in its internal workspace.
    Construct tasks with identifiable intermediate variables, for example X → Z → Y, where Z is necessary to compute the final answer. Compare three conditions:
    the model must compute Z but is not allowed to write it down,
    the model explicitly writes Z as part of its chain-of-thought,
    Z is already supplied in the context, so the model does not need to compute it itself.
    The central question is whether there is a CoT/J-space substitution effect: after information has been externalized into the chain-of-thought, does the model become less dependent on maintaining the same information in J-space?
    A stronger extension is to study this dynamically over a reasoning trajectory. Suppose a problem requires a → b → c → d: without CoT, J-space may need to internally carry the sequence a → b → c → d, whereas with external CoT the context can accumulate a, then a,b, then a,b,c, while J-space only needs to represent the next active variable b, then c, then d. This would suggest that CoT does not simply reduce J-space activity, but instead frees J-space from maintaining already externalized information, allowing it to function as a more limited workspace. 
    Lastly, an interesting intervention is to remove or mask previously written CoT information and compare the resulting performance drop with a J-space ablation; if both interventions disrupt the same intermediate computation, this would provide evidence that the CoT and J-space are substitutes

  

- **Supervisor** Summer
- **Paper** Steerable Visual Representations — Trustworthy Visual Steering

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐
  
  - **Link** : [SteerViT Project Page](https://jonaruthardt.github.io/project/SteerViT/)
  - **Brief description :** This paper introduces SteerViT, which injects text into a frozen vision foundation model through lightweight cross-attention modules. The resulting visual representations can focus on text-specified objects while largely preserving the general-purpose representation quality of the original vision encoder.
  - **How to reproduce :** Use the released checkpoint to reproduce the main object-steering experiments and visualizations. Students can also train a lightweight version on a subset of RefCOCO or RefCOCOg with a frozen DINOv2 backbone.
  - **How to extend :** There are three promising directions. First, improve the steering mechanism itself by making it evidence-aware, so that the model can reduce or reject steering when the text describes an absent, incorrect, or ambiguous object. Second, apply text-steered DINO features to dino-based video generation settings (E.g.: [CAGE](https://arxiv.org/abs/2403.14368)) for controllable video generation, allowing users to select an object with language and control its motion while preserving other objects and the background. Third, extend the method to medical images or other domains, where clinical text can steer the model toward relevant abnormalities, while an uncertainty or abstention mechanism prevents unsupported prompts from creating false visual evidence. Self-proposed extensions are also appreciated.
 
 
- **Supervisor** Abel
- **Paper** Token-Efficient Change Detection in LLM APIs

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐

  - **Link:**
  [Paper](https://openreview.net/pdf?id=7cMlZZYZT0)
  - **Brief description:**
    The black-box nature of LLM APIs, where users do not have access to the model weights or even output probabilities, poses a considerable problem for trustworthy AI systems. A provider may update a model's weights, serving configuration, or safety behavior without downstream users being able to directly verify that the system they previously evaluated is still the same. The highlighted paper introduces Black-Box Border Input Tracking (B3IT), a low-cost method for detecting such changes only through sampling output tokens. The key idea is to search for border inputs: short prompts for which two or more token values have very close output probabilities; even relatively small changes to the model can noticeably alter their output distribution. B3IT first discovers and calibrates a small set of such inputs, then periodically resamples them and detects changes by shifts in their output distributions.
  - **How to reproduce:**
    As a preliminary check, run the demo provided in the B3IT repository, which replays a real model-change event from recorded API observations and reproduces the complete detection pipeline. Then, reproduce the main parts of the in vitro results. Specifically, recreate a scaled-down version of Figures 1-3 for a subset of the 9 models and most TinyChange perturbation types covered by the original paper. Only part of the baselines in Figures 2-3 may be considered in addition to the proposed method.
  - **How to extend:**

    (i) Study how well B3IT can detect changes that specifically affect safety and reliability rather than merely arbitrary changes to the model. For example, create controlled model variants that differ through a changed system or safety prompt, a small safety fine-tune, or a LoRA adapter.

    (ii) Investigate B3IT's effectiveness for implementation changes meant to optimize serving or reduce cost. Potential aspects to consider include changes to the tokenizer or decoding configuration, inference engine, and routing (in an endpoint that does not always serve a single model, but a set of models based on some criteria).

    (iii) Try to improve B3IT's capabilities by actively searching for better border inputs instead of brute-force probing, optimizing for border inputs that provide reliable signals across many perturbation types, or dynamically decreasing the number of observations for sample detection to reduce cost.

- **Supervisor** Roberto
- **Paper :** Watermarking Diffusion Language Models

  - 👨‍🏫: ⭐⭐
  - 🖥️: ⭐
  
  - **Link :** [Paper](https://proceedings.iclr.cc/paper_files/paper/2026/file/a30d1f9de116aa3184e66a3e9d96b69d-Paper-Conference.pdf) | [GitHub](https://github.com/eth-sri/diffusion-lm-watermark)
  - **Brief description :** Watermarking is a set of techniques that enable tracing the origin of synthetic data. The paper extend a  watermarking scheme vastly used for LLMs to diffusion language models. The watermarking scheme modifies the sampling behavior of the model to follow a pattern, so that such pattern can be verified on the data. The watermarked text should be of similar quality to the non-watermarked reference, it should be verifiable, and it should be resistant to attacks and perturbations.
  - **How to reproduce :** The main experiments of the paper can be reproduced by following the installation instruction in the repository README and running the adequate scripts in the script directory.
  - **How to extend :** Implement new attacking strategies to hinder watermark verifiability. Attacking strategies require to modify the text (e.g., paraphrasing) without changing its utility. **(Bonus)** If an effective attack has been found. A new strategy to mitigate this attack can be developed.
    
## Topic 2 : Agentic Systems

- **Supervisor** Giulio

- **Paper** Think Twice Before You Act: Protecting LLM Agents Against Tool Description Poisoning via Isolated Planning

  * 👨‍🏫: ⭐

  * 🖥️: ⭐⭐⭐

  * **Link:** [Think Twice Before You Act: Protecting LLM Agents Against Tool Description Poisoning via Isolated Planning](https://openreview.net/forum?id=jiNw5AgBbw)

  * **Brief description:** LLM-based agents can interact with their environment through tools. These tools are supplied in context through their function definitions, argument schemas, return values, and natural-language descriptions. Because tools, skills, and MCP servers may be downloaded from or exposed by untrusted sources, an attacker can embed instructions in these descriptions. One class of attack subtly steers an agent’s trajectory towards different tool choices, making it less conspicuous than direct malicious-instruction injection. This work addresses tool-description poisoning attacks that steer an agent towards invoking otherwise benign tools. Tool-Guard classifies tool calls along two binary dimensions: aligned versus misaligned, and normal versus suspicious. Tools associated with calls classified as misaligned or suspicious are moved to an influenced list, over which planning is performed separately from the normal tool list.

  * **How to reproduce:** The code for this paper is fully available. You will reproduce **Experiment 1** or **Experiment 3** using two LLMs of your choice. One model must be self-hosted, while the other must be accessed through an inference provider. I can direct you towards suitable options depending on your available hardware and budget; free or low-cost options are also available. 

  * **How to extend:** Separated-planning defenses against prompt injection, tool or skill poisoning, and malicious MCP servers incur additional inference overhead. This overhead may itself be amplified by attacks such as the one proposed in [this paper](https://arxiv.org/pdf/2602.14798). As an extension, you should implement a small set of overthinking-inducing tools and evaluate whether Tool-Guard identifies them as suspicious or misaligned. If time permits, an extension of Tool-Guard that mitigates overthinking-inducing tools can also be explored.


- **Supervisor:** Zhi Wen 
- **Paper:** Active Layer-Contrastive Decoding Reduces Hallucination in Large Language Model Generation

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐⭐

  - **Link:** [Paper](https://aclanthology.org/2025.emnlp-main.150.pdf) | [GitHub](https://github.com/actlcd/ActLCD)

  - **Brief description:** The paper proposes ActLCD, which learns when to activate layer-contrastive decoding during text generation. A policy trained with offline reinforcement learning chooses between standard decoding and contrasting predictions from shallow and deep transformer layers. This selective intervention aims to reduce hallucination while avoiding unnecessary adjustments.

  - **How to reproduce:** Reproduce the experiments in Table 1 on TruthfulQA, LongFact, StrategyQA, and GSM8K using at least three models from the paper. Compare greedy decoding, DoLa, and ActLCD using the paper's evaluation protocol. GPU access is required, and quantized models are allowed. Report the quantization settings and keep them consistent across methods.

  - **How to extend:** Adapt ActLCD to large audio-language models (LALMs), choosing at least two models for evaluation. **Bonus credit:** Modify or extend the decoding strategy, or propose a new one, and show a further reduction in hallucination compared with the adapted ActLCD baseline under the same evaluation protocol.




## Topic : Structured Data Generation
- **Supervisor** Aditya
- **Paper** WaveStitch: Flexible and Fast Conditional Time Series Generation with Diffusion Models

  - 👨‍🏫: ⭐⭐
  - 🖥️: ⭐⭐
  
  - **Link :** https://dl.acm.org/doi/10.1145/3769842
  - **Brief description :** Traditional imputation and forecasting methods often require retraining or adapting separate models for different missingness ratios, observation positions, or forecasting scenarios. Another limitation is generating long time series sequences: conventional methods divide sequences into smaller windows and generate them sequentially, making inference increasingly slow as the horizon grows. WaveStitch overcomes the first limitation by training one universal model once and then guiding it at inference to handle arbitrary observation patterns and missing-value ratios, without scenario-specific retraining. High generation speed for long sequences is achieved via "stitching". Instead of generating windows sequentially, it generates multiple windows in parallel and progressively propagates synchronisation information through a pipelined process, ensuring global temporal coherence. The result is a scalable, flexible, and efficient framework that transforms time-series generation: one model, any missingness pattern, and fast generation of arbitrarily long sequences.
  - **How to reproduce :** Please follow the code repository of the paper: https://github.com/adis98/WaveStitch
  - **How to extend :** While The original paper focuses on time series generation, it would be interesting to see how well the concept of "stitching" generalises to generating other sequential data, specifically, languages. The goal would be to first understand and reproduce the original time series version, then experiment with language diffusion models, including masked diffusion, multinomial, or pure continuous architectures and adapt the stitching mechanism to these scenarios.

– **Supervisor :** Jeroen

* General description : This work aims to identify the ability to safeguard LLMs
during inference, using explainability methods. Herein, focusing on a lightweight sol
ution proposed by Virginia Smith's group.
* **Paper :** SAEs Can Improve Unlearning.
  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐

- **Link :** ArXiv: https://arxiv.org/abs/2504.08192
- Source: https://github.com/aashiqmuhamed/DynamicSAEGuardrails
- Additional code can be provided that contains basic fixes to run the code.
  - **Brief description :**
This paper investigates whether sparse autoencoder (SAE) features permit targeted unlearning in language models. It introduces Dynamic SAE Guardrails (DSG), which identify SAE features associated with the forget set and dynamically intervene on them when relevant inputs are detected. The method aims to reduce access to the target knowledge while limiting effects on unrelated capabilities.
  - **How to reproduce :**
Choose one or more open-source models with available SAE, and apply the work o
n one of the benchmarks used in the paper, or use another available benchmark. Herein,
focusing on Table 1 and Figure 4. Showing that you can perform knowledge editing on
seperate, or multiple unlearning tasks.
  - **How to extend :**
      - Transferability of SAE features: Test whether SAE features selected for one forget set transfer to other prompts or datasets.
      - Massive edits: Extend the method from a small number of target concepts to a large number of simultaneous edits. Extending the few-shot (1 – 4) with low (100) to massive (1000+) edits.
      - Application to MDLMs: Apply the SAE-based unlearning method to masked diffusion language models (MDLMs). When targeting this extension, identify an MDLM with an available SAE/encoder, either for an annealed (AR -> MDM) or for an MDLM from scratch.
      - Transferability of features: Apply SAEs from (base) models on fine-tuned models, or chat model SAEs on obliterated models. Herein, we study the capability of the method to
resist model editing outside the scope of the original paper.
      - SAE quality impact: Herein, we study the impact of the used SAE/encoder method. For example, taking community SAE models to evaluate the ability to steer models in varying settings.

- Basile
  - 👨‍🏫: ⭐⭐
  - 🖥️: ⭐⭐

  - Link: [NeMoS: Nearest Neighbors Bandit meets Active Learning for Online Model Selection](https://openreview.net/forum?id=CSjewjplO1)

  - Description:

	This subject addresses the problem of model selection under budget constraints, which has received a lot of traction lately. The original article is a bandit framework that couples nearest neighbor reward estimation with an active learning strategy. This system operates in the prompt embedding space and estimates the reward of incoming prompts based on feedback from their nearest neighbors. The active learning component helps accelerating convergence by querying ground-truth value when deemed necessary.

  - How to reproduce:

    Students should reproduce the proposed algorithm, focusing on the simpler datasets. The algorithm should run locally on publicly available models, using the smallest ones. The existing codebase should enable easy implementation.

  - How to extend:

    The students should consider one or several of the following extension path :
      - Considering other modalities for the selected models, notably text. This requires using other models as well as considering new metrics for evaluation.
      - Taking into account the different costs of the models. For now, the algorithm only optimizes along one direction (output quality), further work could study how to obtain the most cost-efficient model usage.
	  - Developing compatibility for multi-turn conversations. Most routing mechanisms focus on finding the best model for a specific prompt, which does not account for the real life use-case where several prompts can be used one after the other.


