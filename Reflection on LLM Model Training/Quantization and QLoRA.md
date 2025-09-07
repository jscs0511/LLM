### (1) Quantization: Precision-Memory Trade-Off
A technique that reduces numerical precision to improve memory efficiency.  
**Dynamic Quantization**: Quantization during model inference.  
**Static QUantization**: Quantization during model saving/loading.  
**Quantization-Aware Trainning(QAT)**: Quantization simulation during training.  
*In transformers, we can utilize BitsAndBytesConfig library.*  

### (2) QLoRA: Utilizing Quantized Low Rank Matrices
If the base model is quantized, its numerical precision is reduced, so it cannot be further trained effectively.  
**We should quantize and train only the LoRA matrices(adapters) instead of quantizing and training the base model.**  
We use **"W = W_0 + BA"**.  
**W_0**: represents the pretrained base model’s weights.  
**B and A**: lower-rank decomposed matrices.  
W_0 is kept fixed during training, and only B and A are trained for faster computation with less memory usage.   
Separate adapters can be created and used for different tasks.  
*We can utilize 'peft' library for LoRA config.*  

### (3) Important Lora Configs
**lora_alpha**: Scaling factor multiplied to *BA*.  
**r**: A rank of the *low-rank matrices(B and A)* - generally 8, 16, or 32.  
**target_modules**: Specifies which layers in the base model the LoRA adapters will be attached to. (q_proj, v_proj, k_proj, o_proj, ...)
