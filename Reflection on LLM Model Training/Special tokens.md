### (1) End of Text
Let the model to *stop generating text* by this token.  

### (2) Padding
LLM models use **a padding token** to fix input length to make GPU parallel processing more efficient.  
Pad tokens are ignored when computing the loss value during training. Attention mask indicates whether each token is a padding or not.  
#### Note that if the number of input tokens exceeds the maximum context window, the extra tokens are truncated before being passed to the model.  

### (3) Tip: Ensure you add a eos_token at the end of training data
The model needs to know when each input sequence ends during training.  

### (4) Tip: Do not set the eos_token as the pad_token. Use a reserved token for pad_token
The model needs to know when each input sequence ends during training using *eos_token*. If 'tokenizer.pad_token = tokenizer.eos_token' is set, the model will not be properly trained on the *eos_token* and may fail to learn when to stop generating text. Also, using eos_token as padding can cause issues in loss computation because the eos_token is treated as a valid token unlike a pad_token.**So, you should use a separate reserved token for pad_token.**

