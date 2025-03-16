# Important-GENAI-Concept-for-Interviews
# LoRA & QLoRA :
## Low-Rank Adaptation (LoRA)
* LoRA is a parameter-efficient fine-tuning method for large language models.
* It addresses the high memory requirements of full parameter fine-tuning which updates all model weights.
* Instead of directly updating all the model's weights, LoRA tracks the changes needed for those weights.
* These changes are represented by two smaller matrices (LoRA adapters) that are multiplied together.
* The resulting matrix of changes is added to the original model's weight matrix.
* This significantly reduces the number of trainable parameters compared to full fine-tuning.
* The 'rank' of these smaller matrices determines their size and influences the precision of the updates.
* Achieving performance comparable to full fine-tuning generally requires applying LoRA to all layers of the network.
* Within a certain range (8 to 256), the rank may not significantly impact the final performance if LoRA is used on all layers.
* Other hyperparameters include Alpha (a scaling factor for the weight changes) and Dropout (to prevent overfitting).
## Quantized Low-Rank Adaptation (QLoRA)
* QLoRA is considered "LoRA 2.0" and is a quantized version of LoRA.
* It further reduces memory usage compared to LoRA by quantizing the model's parameters to a lower bit representation (e.g., 4-bit) during fine-tuning.
* QLoRA employs a method to recover the original precision of the model after fine-tuning.
* This allows for fine-tuning large models with significantly less memory while aiming to maintain performance.
* The QLoRA paper provides specific Dropout values used for different model sizes (e.g., 0.1 for 7B/13B and 0.05 for 33B/65B).

## The five levels of chunking strategies :
### **Level 1: Fixed Size Chunking**:
* This is the simplest method, breaking text into chunks of a specified number of characters.
* It doesn't consider the content or structure of the text.
* Frameworks like Langchain and LlamaIndex offer classes such as CharacterTextSplitter and SentenceSplitter for this technique.
* Key concepts include how text is split (by single character), how chunk size is measured (by number of characters), chunk_size (the number of characters in the chunks), chunk_overlap (the number of overlapping characters between chunks), and separator (the character(s) to split on, defaulting to "").

### **Level 2: Recursive Chunking:**
* This method divides text hierarchically and iteratively using a set of separators.
* It attempts to split the text and if the chunks are not the desired size, it recursively splits the resulting chunks with a different separator.
* The Langchain framework provides the RecursiveCharacterTextSplitter class, which uses default separators like “\n\n”, “\n”, “ “,””.
* It offers an alternative to fixed-size chunking by considering text structure.
### **Level 3: Document Based Chunking:**
* This approach splits a document based on its inherent structure.
* It considers the flow and structure of content but might be less effective for documents without clear structure.
* Examples include:
  * Documents with Markdown, where Langchain's MarkdownTextSplitter can be used.
  * Documents with Python/JS code, where Langchain's PythonCodeTextSplitter or the from_language method of RecursiveCharacterTextSplitter can be used.
  * Documents with tables, where preserving relationships requires formatting (e.g., HTML <table> tags, CSV with ';') and often involves summarising the table for embedding.
  * Documents with images (Multi-Modal), where multi-modal models (like GPT-4 vision) can summarise images and their embeddings can be stored. Unstructured.io's partition_pdf can extract images from PDFs.
### **Level 4: Semantic Chunking:**
* This method focuses on extracting semantic meaning from embeddings and assessing semantic relationships between chunks.
* It aims to keep semantically similar chunks together.
* LlamaIndex provides the SemanticSplitterNodeParse class, which adaptively picks breakpoints between sentences using embedding similarity.
* Key concepts include buffer_size (initial window for chunks), breakpoint_percentile_threshold (threshold for splitting), and embed_mode (the embedding model used).
* Unlike previous levels, it deals with the meaning rather than just the content and structure, and doesn't necessitate a constant chunk size.
### **Level 5: Agentic Chunking:**
* This strategy uses LLMs to determine how much and what text should be included in a chunk based on context.
* It uses the concept of Propositions to generate initial stand-alone statements from raw text. Langchain offers a propositional-retrieval template for this.
* An LLM-based agent then decides whether a proposition should be added to an existing chunk or if a new chunk should be created.
* Propositions are either created or included in existing chunks by the agent.

