# Model

An artificial intelligence solution that has been trained upon data, trial and error, using machine learning and deep learning.

A model in of itself typically is not trained upon when executing it's actions wtih the user. In order to train a model, it must go through a specific process of re-enforcement, in order to obtain layers on how to respond to a query or series of inputs.

# In the context of LLMs

A collection of *weights*, of which have been produced as a result of training. They may either predict the next word through token-by-token generation, or through [diffusion](./stable-diffusion.md). The former, outputting a word, based on the previous word, and then the latter, being capable of "rounding out" a response through an initial blob, refining it each turn, then producing something that is legible.

# [Mixture of Experts](https://en.wikipedia.org/wiki/Mixture_of_experts)

A technique that breaks down knowledge understanding into several smaller "experts", then puts everything back together into one. [This hugging face page](https://huggingface.co/blog/moe-transformers) [And it's predecessor](https://huggingface.co/blog/moe) do a good job at explaining further.

They are not a bunch of categories (e.g coding, music, etc), but are layers of which can be used to train on individual knowledge aspects. Two advantages stand out with MoE:

* The ability to pre-train much more efficiently
* Reducing active parameter count when actually running the model
    * which means more efficient execution of a model in general

If tokens corelate with certain active parameters, this means that answers can still be relevent to subject matter at hand, while not having to use every paramter in the consideration of a response.

It doesn't mean that a model will fit in a smaller footprint of memory, but it does mean that execution of a model is overall quicker, and said models can be created faster.

MoEs can also allow for parallelism; if there are several experts loaded, this allows the model to predict much quicker by having them all evaluate simulataneously.

# Open-ness

**Open Weight Models** (or shortened as "open models"), refer to those that have been released publically by a vendor, allowing people to self-host a model, understand it's potential responses, or train upon it further in order to tune it for desired outcomes. This is not to be confused with the concept of **Open Training Data**, in other words, the data used to train the model has been released.

Currently, there are two players that share both the training data, and the weights: [Ai2](https://allenai.org/olmo), and [Nvidia](https://research.nvidia.com/labs/nemotron/Nemotron-3-Super/). They are some of those most transaprent on the market, sharing pre, mid, and post training data so that anyone can view the aspects of how to train a model such as these.

This is cruicial in the context of licensing the use of such models. For example, when trying to construct an open-source project, it's important to figure out what the model may attempt to output, in the event it's output represents code from another license.

# Closed-ness

As of this writing, specifically in the united states, companies training on data that is copyrighted is currently [split between fair use, and infringement.](https://en.wikipedia.org/wiki/Artificial_intelligence_and_copyright#Training_AI_with_copyrighted_data) ([Write-up on the matter, by Ben Murphy](https://ben.substack.com/p/two-rulings-on-fair-use-and-llm-training)) 

Further, output from language models specifically is considered [public domain](https://www.copyright.gov/ai/).

With the current confusion on fair-use or not (it appears to be case-by-case), companies, intentional or not, reside on the edge of what's considered permissable, or within an untested gray area (most). For companies using the output of the models themselves, they tend to have a strong edge considering they do not need to disclose usage of LLMs, with it being considered a "trade secret". Public domain usage of model output means that if the output can't be copyrighted, other forms of income would have to be considered.
