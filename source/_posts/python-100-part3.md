---
title: Python 100题第三部分（节选自41-60题）
date: 2013-02-17 18:10:31
tags: [python, 算法]
categories: python
---

## 第51-55题
> Python按位操作

对于初学者，推荐学习下Codecademy的[这节课程](http://www.codecademy.com/zh/courses/python-intermediate-en-KE1UJ?curriculum_id=4f89dab3d788890003000096)

<!-- more -->

## 第56-60题以及62-65
> 画图操作

轻松一下：
```python
import Image
import ImageDraw

img = Image.new('RGB', (600, 600))
draw = ImageDraw.ImageDraw(img)

# 头
draw.ellipse((250, 20, 350, 120), fill='yellow')
# 左眼
draw.chord((250, 50, 300, 160), 240, 300, fill='red')
# 右眼
draw.chord((300, 50, 350, 160), 240, 300, fill='red')
# 嘴巴
draw.arc((250, 0, 350, 100), 60, 120, fill='red')
# 身子
draw.line((300, 120, 300, 360), fill='yellow')
# 手臂
draw.arc((200, 150, 400, 350), 200, 340, fill='yellow')
# 左腿
draw.line((300, 360, 200, 500), fill='green')
# 右腿
draw.line((300, 360, 400, 500), fill='green')
# 彩虹
colors = ['red', 'orange', 'yellow', 'green', 'cyan' ,'blue', 'purple']
for i, c in enumerate(colors):
    draw.rectangle((50+20*i, 20, 60+20*i, 120), fill=c)
img.show()
```
输出如下图形：
![彩虹和小人](/images/happyrobot.png)
