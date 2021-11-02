---
title: pyautogui挂实验室时长
date: 2021-11-02 13:00:59
tags: [python,小程序]
---

 利用pyautogui实现高校实验室挂时长

原理其实很简单 就是实现每隔五分钟点一下鼠标的作用

一般用于夜晚电脑开着挂

<h1>第一步

先导包

```python
import pyautogui

import time
```

第二部写个for循环

```python
for i in range(0,100):
    print(i)
    pyautogui.click(1113,209, clicks=5,interval=1,duration=0.5)
    time.sleep(298)
```

github仓库源代码  https://github.com/fengxiaop/pyautogui

有用的话记得点个 star

