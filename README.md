### Personal Solution for ComfyUI-Easy-Use

Original Repository: [https://github.com/yolain/ComfyUI-Easy-Use](
https://github.com/yolain/ComfyUI-Easy-Use)

This repository contains my personal solution for compatibility issues of 
ComfyUI-Easy-Use Loop Nodes with the ComfyUI's `DependencyAwareCache`, 
which helps to avoid OutOfMemory (OOM) errors during video generation workflows.

**YOU NEED TO HACK COMFYUI SOURCE CODE TO MAKE IT WORK!**

1. Add `HierarchicalDependencyAwareCache` Class to `comfy_execution/caching.py`
   (implementation under [comfy_patches/comfy_execution/caching.py#L480](./comfy_patches/comfy_execution/caching.py#L480))

2. Add `_clean_cache_recursive` Function to `comfy_execution/caching.py > BasicCache`
   (implementation under [comfy_patches/comfy_execution/caching.py#L176](./comfy_patches/comfy_execution/caching.py#L176))

3. Change `DependencyAwareCache` to `HierarchicalDependencyAwareCache` 
   in `execution.py > CacheSet > init_dependency_aware_cache`

4. Add a single line of `server.executor = self` in `execution.py > PromptExecutor > __init__`

5. Add a single line of `self.executor = None` in `server.py > PromptServer > __init__`

*You could also use the provided files under [comfy_patches](./comfy_patches), 
but these are provided as-is and may not be compatible with your specific ComfyUI version.*