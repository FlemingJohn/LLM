# LLM and Generative AI Notes

## Understanding LLM (Large Language Model) - Basics

LLM is a type of AI that can understand and generate human-like text. It is trained on a massive dataset of text.

### How it works?
1. **Pre-training**: The model is trained on a massive dataset of text (e.g., Wikipedia, books, articles). This stage teaches the model grammar, facts, and some reasoning abilities.
2. **Fine-tuning**: The model is further trained on a smaller, specific dataset to perform a particular task (e.g., medical advice, coding assistance).

### Key Terms
*   **Tokens**: The basic units of text that an LLM processes (could be words or characters).
*   **Parameters**: The internal variables that the model learns during training. A higher number of parameters generally means a more capable model.
*   **Context Window**: The maximum number of tokens a model can consider at one time (its "memory" for a single conversation).

---

## Transformer Architecture

The Transformer is the core architecture behind most modern LLMs (like GPT, Claude, Llama).

### Key Components
1. **Self-Attention Mechanism**: This allows the model to weigh the importance of different words in a sentence, regardless of their distance from each other.
   - Example: "The animal didn't cross the street because **it** was too tired." (The model knows "it" refers to the animal).
2. **Encoders and Decoders**:
   - **Encoder**: Processes the input text.
   - **Decoder**: Generates the output text.
   - *Note: GPT models are "Decoder-only" architectures.*

---

## Tokenization and Embeddings

How machines "read" text.

### 1. Tokenization
The process of breaking down text into tokens.
- Example: "Generative AI" -> ["Generative", " AI"] or ["Gen", "erative", " AI"].

### 2. Embeddings (Vectors)
Tokens are converted into numerical vectors (lists of numbers) in a high-dimensional space.
- Similar words are placed closer together in this space (e.g., "king" and "queen").

---

## Hallucination in LLMs

**Hallucination** occurs when an LLM generates information that sounds plausible but is factually incorrect.

### Why does it happen?
1. **Probabilistic Nature**: LLMs predict the "next most likely token" rather than "retrieving" facts like a database.
2. **Outdated Data**: The model might not have information on recent events.
3. **Leading Questions**: If a user asks a biased question, the model might follow the bias.

### How to Reduce Hallucinations?
- Use **RAG (Retrieval-Augmented Generation)**.
- Provide clear context and constraints.
- Ask for citations.

---

## Fine-Tuning Process

Adjusting a pre-trained model for specific needs.

### Steps in Fine-Tuning:
1. **Base Model Selection**: Start with a pre-trained model (e.g., Llama 3).
2. **Supervised Learning**: Train the model with specific, labeled examples.
   - Train the model with a specific format and tone.
   - In this step, we increase the weights (**Gradient Descent**).
3. **Parameter Efficiency**:
   - **Frozen vs Unfrozen Layers**:
     - **Frozen layer**: Weights do not update during training.
     - **Unfrozen layer**: Weights are updated during training.
   - **LoRA (Low-Rank Adaptation)**: A parameter-efficient fine-tuning (PEFT) method. LoRA doesn't touch the base model weights; it adds small adapters for fine-tuning.
4. **Output Behavior Alignment**:
   - Refuse certain questions.
   - Can give sources for the output.

### Challenges:
1. **Overfitting**: Instead of generalizing, the model memorizes the training data.
2. **Catastrophic Forgetting**: The model degrades its "base knowledge" while learning the new task.

---

## RLHF (Reinforcement Learning from Human Feedback)

A technique to align LLMs with human values and preferences. It "trains the model how to behave."

### Steps in RLHF:
1. **Supervised Fine-Tuning (SFT)**:
   - Curated dataset creation.
   - High-quality prompts and human-preferred responses.
   - **Model Mimicry**: Producing human-like responses (explaining answers with simple English and metaphors).
2. **Reward Modeling**:
   - **Response Generation**: For a single prompt, generate multiple responses.
   - **Human Evaluation and Ranking**: Humans select the best response and rank them (Best, Worst, Average).
   - **Reward Model Training**: Based on human rankings, a separate model automatically learns what a "good" response looks like.
3. **Reinforcement Learning via PPO**:
   - **PPO (Proximal Policy Optimization)**:
     - i) Generate Response.
     - ii) Score by Reward Model.
     - iii) Adjust weights via PPO to maximize the reward score.

---

## Multimodal LLMs

Moving **Beyond Text** to understand different types of data.

Advanced models can process **Text, Images, Tables/Graphs, Audio, and Video**.
- **Text**: Summarize an article.
- **Image**: "What is shown in this photo?"
- **Graph/Table**: "Explain this chart/table."
- **Audio**: "Transcribe this speech."
- **Video**: "Describe what happens in this clip."

---

## Prompt Engineering

The art of crafting prompts to get accurate and useful output from an LLM.

### 3 Steps in Prompting:
1. Understand how the model predicts the prompt.
2. Framing the instruction or prompt.
3. Iterating and refining the prompts.

### The Basic Structure:
**Instruction + Context + Format** = **Good Prompt Structure**.

### Modular Prompt Design:
1. System Role
2. Task Instruction
3. Formatting Rules
4. Input Data
5. Tone or Voice
6. Output Expectation

---

## Prompting Frameworks

### 1. CREATE
- **C** -> Context
- **R** -> Role
- **E** -> Examples
- **A** -> Asks (Task)
- **T** -> Tone
- **E** -> Expectations

### 2. TREE
- **T** -> Task
- **R** -> Reasoning
- **E** -> Example
- **E** -> Evaluation

### 3. CRISP
- **C** -> Clarify
- **R** -> Refine
- **I** -> Inject Style
- **P** -> Personalize

---

## Flow of an LLM
**Tokens** -> **Vectors** -> **Transformer Layers** -> **Autoregression** (Token Prediction)
