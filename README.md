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

