# 1.正面tag



## 1.通用正面优化tag

```
 (masterpiece:1,2), best quality, masterpiece, highres, original, extremely detailed wallpaper, perfect lighting,(extremely detailed CG:1.2), drawing, paintbrush,
```

(杰作:1,2)，最好的质量，杰作，高分辨率，原创，非常详细的壁纸，完美的照明，(非常详细的CG:1.2)，绘图，画笔，





# 2.负面tag



## 1.通用负面tag

```
NSFW, (worst quality:2), (low quality:2), (normal quality:2), lowres, normal quality, ((monochrome)), ((grayscale)), skin spots, acnes, skin blemishes, age spot, (ugly:1.331), (duplicate:1.331), (morbid:1.21), (mutilated:1.21), (tranny:1.331), mutated hands, (poorly drawn hands:1.5), blurry, (bad anatomy:1.21), (bad proportions:1.331), extra limbs, (disfigured:1.331), (missing arms:1.331), (extra legs:1.331), (fused fingers:1.61051), (too many fingers:1.61051), (unclear eyes:1.331), lowers, bad hands, missing fingers, extra digit,bad hands, missing fingers, (((extra arms and legs))),
```

NSFW，(最差质量:2)，(低质量:2)，(正常质量:2)，低分辨率，正常质量，((单色))，((灰度))，皮肤斑点，痤疮，皮肤瑕疵，老年斑，(丑陋:1.331)，(重复:1.331)，(病态:1.21)，(残缺:1.21)，(变形:1.331)，变异手，(画得不好的手:1.5)，模糊，(解剖不良:1.21)，(比例不良:1.331)，多肢，(毁容:1.331)，(缺臂:1.331)，(多腿:1.331)，(融合手指:1.61051)，(手指过多:1.61051)，(眼睛不清:1.331)，低，手不好，少了手指，多了手指，手不好，少了手指，((多了胳膊和腿))





# 3.文生图入门与提示词基础



[Stable Diffusion 零基础入门课学习资料汇总 - 幕布 (mubu.com)](https://mubu.com/doc/_2As4DSE4m#o-1WgLvuLcnh)



[Stable Diffusion 新手入门手册 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/619120794)



## 1.提示词基本语法

### 提示词类别

1.内容型提示词

![b2b31116-f792-4be6-a1a8-4260b45c459f-3233270](C:\Users\oyy\Desktop\ai\images\b2b31116-f792-4be6-a1a8-4260b45c459f-3233270.jpg)

2.标准化提示词

![e1fd8e34-8e35-42ce-b11a-962526ba1168-3233270](C:\Users\oyy\Desktop\ai\images\e1fd8e34-8e35-42ce-b11a-962526ba1168-3233270.jpg)

### 提示词语法

1.权重（优先级）增减

![beb5ad55-8b10-4595-aead-4ea66e89eac8-3233270](C:\Users\oyy\Desktop\ai\images\beb5ad55-8b10-4595-aead-4ea66e89eac8-3233270.jpg)

### 书写提示词的模版

![49fd065e-b6c6-44a2-bdb6-2536a58a10bf-3233270](C:\Users\oyy\Desktop\ai\images\49fd065e-b6c6-44a2-bdb6-2536a58a10bf-3233270.jpg)

### 提示词网站

一个工具箱：http://www.atoolbox.net/Tool.php?Id=1101

AI词语加速器：https://ai.dawnmark.cn/

# 4.模型基础概念及应用

- ① 模型搜索网站

  - Hugging Face（抱脸）：https://huggingface.co/models
    - 深度学习和人工智能的专业网站，大佬多，但找起来不是很直观

  - Civitai（C站）：https://civitai.com/
    - 全世界最受欢迎的AI绘画模型分享网站，除了模型还有很多优秀作品展示

![image-20230512151736666](C:\Users\oyy\Desktop\ai\images\image-20230512151736666.png)









5.下载模型。

ControlNet是需要专用模型的，否则无法使用相关功能引导图画。

接下来我们下载模型。

下载地址，https://huggingface.co/lllyasviel/ControlNet/tree/main/models

但是你会发现模型有很多种，选哪种呢？

![图片](https://mmbiz.qpic.cn/mmbiz_png/UmmUuYR5zbicvj47ZBWllDQcMzWFHGliavsPx2jTce1iaH6426aGTpyaJkaQNwCGhuYvLVAmLWpNbICfPv4td5owg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

大家硬盘有限的可以先下载canny，openpose，scribble这三个模型。

canny主要是边缘检测，属于比较通用的模型，Openpose就是传说中的姿势控制专用模型，而scribble是手稿模型，适合随手涂鸦然后生成一个精美的画面，可玩性很高。

（硬盘空间比较大的建议全下载一下，因为每个模型都有自己的使用场景，各有各自的特色。）

下载好之后，把xxx.pth文件放到stable-diffusion-webui > models > ControlNet文件夹下面。

现在大家就已经可以开始用controlnet来玩耍了。

（PS：ControlNet依赖xformers算法框架及Nvidia显卡，Mac系统的同学可能使用效果只能有70-80分，而且速度慢，较难达到文档描述那种哇塞的效果）

怎么玩呢？因为各种controlnet的模型使用还是有点复杂的，会放到后面一篇文章详细讲。

感兴趣的同学记得点赞关注哦～

那么今天的课先到这里，明天见～

更多AI绘图相关文章，请查看[AI绘画文章合集0305](http://mp.weixin.qq.com/s?__biz=MzI2NTQ0MjY5Nw==&mid=2247484815&idx=1&sn=88e3f9fdfa16bcd19b1d25a9ec0a2923&chksm=ea9c0169ddeb887fa6e790876b057d2bb78420bbb01e340f0138a7cf7f5a2e22c13577d1c00d&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_png/UmmUuYR5zbibEu528GUFnPAqtSGibJ05ZrMU9ho8WY0CibkvNr2B5siaicD1iaLaF7M3ZNL2mTQD2sOia9sCTOoznf4Jg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
