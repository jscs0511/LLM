### XXX-Inst model  
Already trained by instruction dataset. Able to answer the user's query quite well without further tuning.  
### Performance?
It is somewhat hard to fine-tune an inst model compared to fine-tune a base model.  
If you have a good quality of dataset, probably fine-tuning base model would be a better choice.  
Otherwise, you can of course try fine-tuning an inst model.  
However, the best approach is to fine-turn both an inst and a base model..!  
### When training an inst model  
Make sure you strictly follow instruction formatting when training it.  
Special token (end_of_text for example) could be different from a base model.  
