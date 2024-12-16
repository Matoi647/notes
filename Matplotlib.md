### VS Code ssh 调试 Matplotlib 无法显示（画图时阻塞）

``` python
import matplotlib
matplotlib.use('Agg')   # Headless
import matplotlib.pyplot as plt
```
