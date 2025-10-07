---
title: 降采样知识备忘
comments: false
---

### 降采样知识备忘：400Hz 降采样到 50Hz

**问题**  
直接降采样时，信号出现锯齿波形，主要是因为没有进行抗混叠滤波，导致高频成分混叠失真。

**关键点**  

- 降采样前必须先做低通滤波，滤除高于新采样率一半（25Hz）的频率成分。  
- 使用 `scipy.signal.decimate` 函数可以自动完成抗混叠滤波和降采样。  
- 推荐使用 FIR 滤波器（`ftype='fir'`），效果更平滑，避免锯齿。

**示例代码**

```python
from scipy.signal import decimate

downsample_factor = 8  # 400Hz 降到 50Hz
y = decimate(x, downsample_factor, ftype='fir')
```