---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: ai
  language: python
  name: ai
---

(sanstyle:intro)=
# Sanstyle 家族

为了方便管理代码和数据创建仓库：

- [xinetzone/dash-xinet](https://github.com/xinetzone/dash-xinet)：简化 Dash 的使用。
- [SanstyleLab/plotly-dastsets](https://github.com/SanstyleLab/plotly-dastsets)：存储一些数据集以及展示图片。
- [xinetzone/sanstyle](https://github.com/xinetzone/sanstyle)：处理一些常见任务。

安装：

```sh
pip install dash-xinet sanstyle -i https://pypi.org/simple/ 
```

## `dash_xinet`

```python
from dash_xinet.server import create_app, run_server
from dash_xinet.utils.nav import create_nav

external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']
app = create_app(__name__, external_stylesheets=external_stylesheets)
```

Dash 应用使用和运行：

```python
layout = ... # 布局
await run_server(app, layout, port=8050) # 启动应用
```

更多内容可阅读：[Sansty Dash — Dash 手册 (xinetzone.github.io)](https://xinetzone.github.io/dash-book/)。

## `sanstyle`

可以直接批量修改文件后缀：

```python
rename_suffix(root, old, new)
```

`root`
:   需要修改的跟目录

`old`
:   被修改的文件后缀，如 `.txt`

`new`
:   修改后的文件后缀，如 `.rst`

### 创建 `<embed>` 元素

```{code-cell} ipython3
from sanstyle.display.html import Embed

snippet_url = 'https://dash-book.herokuapp.com'
figure_n_slider_dash = Embed(snippet_url + '/examples/figure-n-slider',
                   className='w3-pale-blue',
                   height=500)
figure_n_slider_dash
```

```{code-cell} ipython3
:tags: [remove-input]
from myst_nb import glue
glue("figure_n_slider_dash", figure_n_slider_dash, display=False)
```

## 导入 `plotly-dastsets`

```{code-cell} ipython3
import pandas as pd
from sanstyle.github.file import lfs_url

url = lfs_url('SanstyleLab/plotly-dastsets',
              'simple/usa-agricultural-exports-2011.csv')
df = pd.read_csv(url)
df.head()
```