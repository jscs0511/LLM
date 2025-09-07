### (1) Learning rate (lr)
In my personal opinion, learning rate is **the most important parameter** when training a deep learning model(*espcially LLM transformer*). Its main idea is to control how much a model learns *from each batch of data*; It indicates **how much the weights are updated during backpropagation based on the loss value.**   
If too high: drastic updates → may cause divergence.  
If too low: learning speed too low & may get stuck at local minimum.  
#### How to find a best learning rate?  
It is best to experiment with various learning rates. You may utilize a different scheduler to conduct this experiment.  
#### Different sterategy to give diversity to learning rate: lr_scheduler_type
constant_with_warmup: The lr starts at a user-provided value, gradually increases, and then becoms constant at a user-defined point.  
linear_decay: The lr decreases in a linear way.  
cosine_decay: The lr decreases following a cosine curve.  

### (2) Batch Size, Steps, and Epoch
**Batch size** determines how much data the model trains on at once. In LLM training/fine-tuning, maximize it up to the GPU's memory capacity.  
**One step** corresponds to a single batch update — that is, *one forward and backward pass with a batch of data*.  
For example, if the dataset contains 500 samples and the batch size is 10, then each epoch consists of 50 steps.
If max_steps is set to 20, the training will process 20 batches (i.e., 200 samples total, possibly with repetition depending on sampling strategy).  
The total number of steps equals the total number of parameter updates.  
**Epoch** determines how many times the model gets trained for the entire dataset.  
*When both steps and epoch are provided as an argument, epoch is ignored*  

### (3) Context Window and Max Sequence Length
**Context Window** varies between LLM models. It determines how many tokens the model can process in a single pass.  
**Max Sequence Length**(max_seq_length) determines the maximum length during training; Ideally it should be less than context window. Otherwise data can be lost. *Longer max sequence length uses more memory, so batch size usually needs to be smaller to fit GPU limits.*  
