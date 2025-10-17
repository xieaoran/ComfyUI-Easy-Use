### Personal Solution for ComfyUI-Easy-Use

Original Repository: [https://github.com/yolain/ComfyUI-Easy-Use](
https://github.com/yolain/ComfyUI-Easy-Use)

This repository contains my personal solution for compatibility issues of 
ComfyUI-Easy-Use Loop Nodes with the ComfyUI's `DependencyAwareCache`, 
which helps to avoid OutOfMemory (OOM) errors during video generation workflows.

**YOU NEED TO HACK COMFYUI SOURCE CODE TO MAKE IT WORK!**

1. Append `HierarchicalDependencyAwareCache` to `comfy_execution/caching.py`
   (implementation under [comfy_patches/comfy_execution/caching.py](./comfy_patches/comfy_execution/caching.py):

2. Change `DependencyAwareCache` to `HierarchicalDependencyAwareCache` 
   in `execution.py > CacheSet > init_dependency_aware_cache`

3. Add a single line of `server.executor = self` in `execution.py > PromptExecutor > __init__`

4. Add a single line of `self.executor = None` in `server.py > PromptServer > __init__`

*You could also use the provided files under [comfy_patches](./comfy_patches), 
but these are provided as-is and may not be compatible with your specific ComfyUI version.*