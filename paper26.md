
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
- **Paper ** Guard

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐
  
  - **Link :** 
  - **Brief description :** 
  - **How to reproduce :**
  - **How to extend :** 

## Topic 2 : Agentic Systems

- **Supervisor** Giulio

- **Paper** Think Twice Before You Act: Protecting LLM Agents Against Tool Description Poisoning via Isolated Planning

  * 👨‍🏫: ⭐

  * 🖥️: ⭐⭐⭐

  * **Link:** [Think Twice Before You Act: Protecting LLM Agents Against Tool Description Poisoning via Isolated Planning](https://openreview.net/forum?id=jiNw5AgBbw)

  * **Brief description:** LLM-based agents can interact with their environment through tools. These tools are supplied in context through their function definitions, argument schemas, return values, and natural-language descriptions. Because tools, skills, and MCP servers may be downloaded from or exposed by untrusted sources, an attacker can embed instructions in these descriptions. One class of attack subtly steers an agent’s trajectory towards different tool choices, making it less conspicuous than direct malicious-instruction injection. This work addresses tool-description poisoning attacks that steer an agent towards invoking otherwise benign tools. Tool-Guard classifies tool calls along two binary dimensions: aligned versus misaligned, and normal versus suspicious. Tools associated with calls classified as misaligned or suspicious are moved to an influenced list, over which planning is performed separately from the normal tool list.

  * **How to reproduce:** The code for this paper is fully available. You will reproduce **Experiment 1** or **Experiment 3** using two LLMs of your choice. One model must be self-hosted, while the other must be accessed through an inference provider. I can direct you towards suitable options depending on your available hardware and budget; free or low-cost options are also available. 

  * **How to extend:** Separated-planning defenses against prompt injection, tool or skill poisoning, and malicious MCP servers incur additional inference overhead. This overhead may itself be amplified by attacks such as the one proposed in [this paper](https://arxiv.org/pdf/2602.14798). As an extension, you should implement a small set of overthinking-inducing tools and evaluate whether Tool-Guard identifies them as suspicious or misaligned. If time permits, an extension of Tool-Guard that mitigates overthinking-inducing tools can also be explored.


-- **Supervisor** Zhiwen
- **Paper ** XXXXX

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐
  
  - **Link :** 
  - **Brief description :** 
  - **How to reproduce :**
  - **How to extend :** 


-- **Supervisor** Roberto
- **Paper ** XXXXX

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐
  
  - **Link :** 
  - **Brief description :** 
  - **How to reproduce :**
  - **How to extend :** 



## Topic : Structured Data Generation
- **Supervisor** Aditya
- **Paper** WaveStitch: Flexible and Fast Conditional Time Series Generation with Diffusion Models

  - 👨‍🏫: ⭐⭐
  - 🖥️: ⭐⭐
  
  - **Link :** https://dl.acm.org/doi/10.1145/3769842
  - **Brief description :** Traditional imputation and forecasting methods often require retraining or adapting separate models for different missingness ratios, observation positions, or forecasting scenarios. Another limitation is generating long time series sequences: conventional methods divide sequences into smaller windows and generate them sequentially, making inference increasingly slow as the horizon grows. WaveStitch overcomes the first limitation by training one universal model once and then guiding it at inference to handle arbitrary observation patterns and missing-value ratios, without scenario-specific retraining. High generation speed for long sequences is achieved via "stitching". Instead of generating windows sequentially, it generates multiple windows in parallel and progressively propagates synchronisation information through a pipelined process, ensuring global temporal coherence. The result is a scalable, flexible, and efficient framework that transforms time-series generation: one model, any missingness pattern, and fast generation of arbitrarily long sequences.
  - **How to reproduce :** Please follow the code repository of the paper: https://github.com/adis98/WaveStitch
  - **How to extend :** While The original paper focuses on time series generation, it would be interesting to see how well the concept of "stitching" generalises to generating other sequential data, specifically, languages. The goal would be to first understand and reproduce the original time series version, then experiment with language diffusion models, including masked diffusion, multinomial, or pure continuous architectures and adapt the stitching mechanism to these scenarios.

-- **Supervisor** Jeroen
- **General description :** 
- **Paper ** XXXXX

  - 👨‍🏫: ⭐
  - 🖥️: ⭐⭐⭐
  
  - **Link :** 
  - **Brief description :** 
  - **How to reproduce :**
  - **How to extend :** 




