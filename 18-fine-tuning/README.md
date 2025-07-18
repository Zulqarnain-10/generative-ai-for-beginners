[![Open Source Models](./img/18-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://aka.ms/gen-ai-lesson18-gh?WT.mc_id=academic-105485-koreyst)

# Fine-Tuning LLM

Using large language models to build generative AI applications comes with new challenges. A key issue is ensuring response quality (accuracy and relevance) in content generated by the model for a given user request. In previous lessons, we discussed techniques like prompt engineering and retrieval-augmented generation that try to solve the problem by _modifying the prompt input_ to the existing model.

In today's lesson, we discuss a third technique, **fine-tuning**, which tries to address the challenge by _retraining the model itself_ with additional data. Let's dive into the details.

## Learning Objectives

This lesson introduces the concept of fine-tuning for pre-trained language models, explores the benefits and challenges of this approach, and provides guidance on when and how to use fine tuning to improve the performance of your generative AI models.

By the end of this lesson, you should be able to answer the following questions:

- What is fine tuning for language models?
- When, and why, is fine tuning useful?
- How can I fine-tune a pre-trained model?
- What are the limitations of fine-tuning?

Ready? Let's get started.

## Illustrated Guide

Want to get the big picture of what we'll cover before we dive in? Check out this illustrated guide that describes the learning journey for this lesson - from learning the core concepts and motivation for fine-tuning, to understanding the process and best practices for executing the fine-tuning task. This is a fascinating topic for exploration, so don't forget to check out the [Resources](./RESOURCES.md?WT.mc_id=academic-105485-koreyst) page for additional links to support your self-guided learning journey!

![Illustrated Guide to Fine Tuning Language Models](./img/18-fine-tuning-sketchnote.png?WT.mc_id=academic-105485-koreyst)

## What is fine-tuning for language models?

By definition, large language models are _pre-trained_ on large quantities of text sourced from diverse sources including the internet. As we've learned in previous lessons, we need techniques like _prompt engineering_ and _retrieval-augmented generation_ to improve the quality of the model's responses to the user's questions ("prompts").

A popular prompt-engineering technique involves giving the model more guidance on what is expected in the response either by providing _instructions_ (explicit guidance) or _giving it a few examples_ (implicit guidance). This is referred to as _few-shot learning_ but it has two limitations:

- Model token limits can restrict the number of examples you can give, and limit the effectiveness.
- Model token costs can make it expensive to add examples to every prompt, and limit flexibility.

Fine-tuning is a common practice in machine learning systems where we take a pre-trained model and retrain it with new data to improve its performance on a specific task. In the context of language models, we can fine-tune the pre-trained model _with a curated set of examples for a given task or application domain_ to create a **custom model** that may be more accurate and relevant for that specific task or domain. A side-benefit of fine-tuning is that it can also reduce the number of examples needed for few-shot learning - reducing token usage and related costs.

## When and why should we fine-tune models?

In _this_ context, when we talk about fine-tuning, we are referring to **supervised** fine-tuning where the retraining is done by **adding new data** that was not part of the original training dataset. This is different from an unsupervised fine-tuning approach where the model is retrained on the original data, but with different hyperparameters.

The key thing to remember is that fine-tuning is an advanced technique that requires a certain level of expertise to get the desired results. If done incorrectly, it may not provide the expected improvements, and may even degrade the performance of the model for your targeted domain.

So, before you learn "how" to fine-tune language models, you need to know "why" you should take this route, and "when" to start the process of fine-tuning. Start by asking yourself these questions:

- **Use Case**: What is your _use case_ for fine-tuning? What aspect of the current pre-trained model do you want to improve upon?
- **Alternatives**: Have you tried _other techniques_ to achieve the desired outcomes? Use them to create a baseline for comparison.
  - Prompt engineering: Try techniques like few-shot prompting with examples of relevant prompt responses. Evaluate the quality of responses.
  - Retrieval Augmented Generation: Try augmenting prompts with query results retrieved by searching your data. Evaluate the quality of responses.
- **Costs**: Have you identified the costs for fine-tuning?
  - Tunability - is the pre-trained model available for fine-tuning?
  - Effort - for preparing training data, evaluating & refining model.
  - Compute - for running fine-tuning jobs, and deploying fine-tuned model
  - Data - access to sufficient quality examples for fine-tuning impact
- **Benefits**: Have you confirmed the benefits for fine-tuning?
  - Quality - did fine-tuned model outperform the baseline?
  - Cost - does it reduce token usage by simplifying prompts?
  - Extensibility - can you repurpose the base model for new domains?

By answering these questions, you should be able to decide if fine-tuning is the right approach for your use case. Ideally, the approach is valid only if the benefits outweigh the costs. Once you decide to proceed, it's time to think about _how_ you can fine tune the pre-trained model.

Want to get more insights on the decision-making process? Watch [To fine-tune or not to fine-tune](https://www.youtube.com/watch?v=0Jo-z-MFxJs)

## How can we fine-tune a pre-trained model?

To fine-tune a pre-trained model, you need to have:

- a pre-trained model to fine-tune
- a dataset to use for fine-tuning
- a training environment to run the fine-tuning job
- a hosting environment to deploy fine-tuned model

## Fine-Tuning In Action

The following resources provide step-by-step tutorials to walk you through a real example using a selected model with a curated dataset. To work through these tutorials, you need an account on the specific provider, along with access to the relevant model and datasets.

| Provider     | Tutorial                                                                                                                                                                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OpenAI       | [How to fine-tune chat models](https://github.com/openai/openai-cookbook/blob/main/examples/How_to_finetune_chat_models.ipynb?WT.mc_id=academic-105485-koreyst)                | Learn to fine-tune a `gpt-35-turbo` for a specific domain ("recipe assistant") by preparing training data, running the fine-tuning job, and using the fine-tuned model for inference.                                                                                                                                                                                                                                              |
| Azure OpenAI | [GPT 3.5 Turbo fine-tuning tutorial](https://learn.microsoft.com/azure/ai-services/openai/tutorials/fine-tune?tabs=python-new%2Ccommand-line?WT.mc_id=academic-105485-koreyst) | Learn to fine-tune a `gpt-35-turbo-0613` model **on Azure** by taking steps to create & upload training data, run the fine-tuning job. Deploy & use the new model.                                                                                                                                                                                                                                                                 |
| Hugging Face | [Fine-tuning LLMs with Hugging Face](https://www.philschmid.de/fine-tune-llms-in-2024-with-trl?WT.mc_id=academic-105485-koreyst)                                               | This blog post walks you fine-tuning an _open LLM_ (ex: `CodeLlama 7B`) using the [transformers](https://huggingface.co/docs/transformers/index?WT.mc_id=academic-105485-koreyst) library & [Transformer Reinforcement Learning (TRL)](https://huggingface.co/docs/trl/index?WT.mc_id=academic-105485-koreyst]) with open [datasets](https://huggingface.co/docs/datasets/index?WT.mc_id=academic-105485-koreyst) on Hugging Face. |
|              |                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 🤗 AutoTrain | [Fine-tuning LLMs with AutoTrain](https://github.com/huggingface/autotrain-advanced/?WT.mc_id=academic-105485-koreyst)                                                         | AutoTrain (or AutoTrain Advanced) is a python library developed by Hugging Face that allows finetuning for many different tasks including LLM finetuning. AutoTrain is a no-code solution and finetuning can be done in your own cloud, on Hugging Face Spaces or locally. It supports both a web-based GUI, CLI and training via yaml config files.                                                                               |
|              |                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## Assignment

Select one of the tutorials above and walk through them. _We may replicate a version of these tutorials in Jupyter Notebooks in this repo for reference only. Please use the original sources directly to get the latest versions_.

## Great Work! Continue Your Learning.

After completing this lesson, check out our [Generative AI Learning collection](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) to continue leveling up your Generative AI knowledge!

Congratulations!! You have completed the final lesson from the v2 series for this course! Don't stop learning and building. \*\*Check out the [RESOURCES](RESOURCES.md?WT.mc_id=academic-105485-koreyst) page for a list of additional suggestions for just this topic.

Our v1 series of lessons has also been updated with more assignments and concepts. So take a minute to refresh your knowledge - and please [share your questions and feedback](https://github.com/microsoft/generative-ai-for-beginners/issues?WT.mc_id=academic-105485-koreyst) to help us improve these lessons for the community.
