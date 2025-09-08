## Why vLLM?
When using LLMs in real products, inference efficiency is key to speed and cost. Larger models(more parameters) are slower and more expensive, but various optimization techniques are continuously being developed to address these challenges. vLLM efficiently manages GPU memory, supports multiple models via Hugging Face, and is optimized for handling many concurrent requests.  

## KV Cache
During inference, caching Key and Value matrices removes redundant computation and speeds up processing, but increases GPU memory usage. This highlights the growing need for more efficient GPU memory management techniques. (This leads to the development of techniques like paged attention.)  

## Paged attention
GPU memory is managed in small blocks (pages), loading only necessary KV cache onto the GPU and storing the rest on the CPU.  
Pros: Lower GPU memory use and support for multiple concurrent requests.  
Cons: Latency from GPU-CPU page swapping. If needed KV cache isn’t on the GPU, fetching from the CPU over the PCIe bus causes delays. Frequent page misses increase this latency.  
In vLLM, 'gpu_memory_utilization' parameter mainly controls the amount of KV cache stored on the GPU. Adjusting it balances GPU memory use and CPU offloading, optimizing memory management and performance.  

## Continous Batching
User requests are dynamically managed, based on individual generation steps.
If any request finishes early during GPU processing (When an EOS token is generated),
the resources allocated to that request are immediately released and reused to process a new waiting request in the next generation step.  
GPU operates almost continuously without idle time, significantly improving throughput. Resources are quickly released and reallocated, maximizing GPU utilization efficiency.

## Drawback
**Only one inference model can be used at a time,** and switching to a different model after creating an instance requires destroying the current instance each time.  

