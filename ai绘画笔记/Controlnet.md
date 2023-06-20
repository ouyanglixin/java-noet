# 1.ControlNet 缘起简介

ControlNet 作者：张吕敏，他是2021年本科毕业，目前正在斯坦福读博的中国人，为我们这位年轻同胞点赞。ControlNet 是作者提出的一个新的神经网络概念，就是通过额外的输入来控制预训练的大模型，比如 stable diffusion。这个本质其实就是端对端的训练，早在2017年就有类似的AI模型出现，只不过这一次因为加入了 SD 这样优质的大模型，让这种端对端的训练有了更好的应用空间。它很好的解决了文生图大模型的关键问题：单纯的关键词控制方式无法满足对细节精确控制的需要。
之前很火的 Style2Paints 也是这位作者制作的，除此之外他还做了一款名为 YGO PRO 2 的 Unity 纸牌游戏，这款游戏在国内外都有不少粉丝。





## 基础参数

### 1. 启用（Enable）

勾选此选项后，点击 “生成” 按钮时，ControlNet 才会生效。

### 2. 反色模式（Invert Input Color）

将图像颜色进行反转后应用。

### 3. RGB 转 BGR（RGB to BGR）

把颜色通道进行反转，在 NormalMap 模式可能会用到。

### 4. 低显存优化（Low VRAM）

低显存模式，如果你的显卡内存小于等于4GB，建议勾选此选项。

### 5. 无提示词的猜测模式（Guess Mode）

也就是盲盒模式，不需要任何正面与负面提示词，出图效果随机，很有可能产生意想不到的惊喜效果！

### 6. 预处理器（Preprocessor）

在此列表我们可选择需要的预处理器，每个 ControlNet 的预处理器都有不同的功能，后续将会详细介绍。

### 7. 模型（Model）

配套各预处理器需要的专属模型。该列表内的模型必须与预处理选项框内的名称选择一致，才能保证正确生成预期结果。如果预处理与模型不致其实也可以出图，但效果无法预料，且一般效果并不理想。

### 8. 权重（Weight）

权重，代表使用 ControlNet 生成图片时被应用的权重占比。

### 9. 引导介入时机（Guidance Start(T)）

在理解此功能之前，我们应该先知道生成图片的 Sampling steps 采样步数功能，步数代表生成一张图片要刷新计算多少次，Guidance Start(T) 设置为 0 即代表开始时就介入，默认为 0，设置为 0.5 时即代表 ControlNet 从 50% 步数时开始介入计算。

### 10. 引导退出时机（Guidance End(T)）

和引导介入时机相对应，如设置为1，则表示在100%计算完时才会退出介入也就是不退出，默认为 1，可调节范围 0-1，如设置为 0.8 时即代表从80% 步数时退出介入。

### 11. 缩放模式（Resize Mode）

用于选择调整图像大小的模式：默认使用（Scale to Fit (Inner Fit)）缩放至合适即可，将会自动适配图片。
一共三个选项：Just Resize，Scale to Fit (Inner Fit)，Envelope (Outer Fit)

### 12. 画布宽度和高度（Canvas Width 和 Canvas Height）

画布宽高设置，请注意这里的宽高，并不是指 SD 生成图片的图像宽高比。该宽高代表 ControlNet 引导时所使用的控制图像的分辨率，假如你用 SD 生成的图片是 1000x2000 分辨率，那么使用 ControlNet 引导图像时，对显存的消耗将是非常大的；我们可以将引导控制图像的分辨率设置为 500x1000 ，也就是缩放为原本图像一半的分辨率尺寸去进行引导，这有利于节省显存消耗。

### 13. 创建空白画布（Create Blank Canvas）

如果之前使用过 ControlNet 功能，那么将会在 ControlNet 的图像区域留有历史图片，点击该按钮可以清空之前的历史，也就是创建一张空白的画布。

### 14. 预览预处理结果（Preview Annotator Result）

点击该按钮可以预览生成的引导图。例如：如果使用 Canny 作为预处理器，那么点击该按钮之后，可以看到一张通过 Canny 模型提取的边缘线图片。

### 15. 隐藏预处理结果（Hide Annotator Result）

点击该按钮可以隐藏通过 Preview 按钮生成的预览图像窗口（不建议隐藏）



## 2、预处理器功能详解

ControlNet 的核心能力就是能让我们通过设置各种条件来让AI更可控地生成最终图像结果。这些条件就是通过调节预处理器参数来实现的，所以我们首先要先了解下 ControlNet 各种预处理器的功能。

### 1. Canny 边缘检测

Canny 边缘检测预处理器可很好识别出图像内各对象的边缘轮廓，常用于生成线稿。

### · 预处理器分辨率

预处理器分辨率数值越高越精细，也越吃显存。但如果数值太低生成的线条也会很粗糙。默认512，具体设置时需根据素材大小和实际情况来做权衡。

![img](https://pic4.zhimg.com/80/v2-477a30d2b2841b6af2b50332083b8e2b_720w.webp)

### · 长和宽的阈值

这个值越高线条越简单，越低线条越复杂。

![img](https://pic4.zhimg.com/80/v2-c9a9aad26cf5a6d7348fd878ff219c37_720w.webp)

注意：一定要找到和预处理器对应名字一样的模型。

![img](https://pic2.zhimg.com/80/v2-e2d0961d0e0d1aa52aa6e79cf146cf31_720w.webp)

重绘幅度越高，AI越放飞自我。

![img](https://pic1.zhimg.com/80/v2-47a1eb2718b8976f0ee34faae0e431d8_720w.webp)

Prompt: "cute dog"

![img](https://pic4.zhimg.com/80/v2-858eaf8c5a0a318822dac5b7ee9fc1fb_720w.webp)

给线稿上色制作的小动画效果也挺好。[https://twitter.com/izumisatoshi05/status/1625835599017148416](https://link.zhihu.com/?target=https%3A//twitter.com/izumisatoshi05/status/1625835599017148416)

### 2. Depth 深度检测

通过提取原始图片中的深度信息，生成具有原图同样深度结构的深度图，越白的越靠前，越黑的越靠后。

### · MiDaS 深度信息估算

MiDaS 深度信息估算，是用来控制空间距离的，类似生成一张深度图。一般用在较大纵深的风景，可以更好表示纵深的远近关系。

注：有时我们也可以用于生成遮罩蒙版。

![img](https://pic4.zhimg.com/80/v2-861c2a981f9f276c02875e9ef31ba1bf_720w.webp)

### · LeReS 深度信息估算

LeReS 深度信息估算比 MiDaS 深度信息估算方法的成像焦点在中间景深层，这样的好处是能有更远的景深，且中距离物品边缘成像会更清晰，但近景图像的边缘会比较模糊，具体实战中需用哪个估算方法可根据需要灵活选择。

![img](https://pic4.zhimg.com/80/v2-67e47a09e3c058463fda0224287bf293_720w.webp)

如下图能看出我们很好地控制住了生成结果的整体结构，这与原图基本保持一致。

![img](https://pic3.zhimg.com/80/v2-876658b549c26d6c81540b06c096eba6_720w.webp)

### 3. HED 边缘检测

HED 边缘检测可保留更多柔和的边缘细节，类似手绘效果。

![img](https://pic4.zhimg.com/80/v2-8fca3dd2cb640c61b8666e4b789d4faf_720w.webp)

参数也是分辨率越高越精细，但也越吃显存。

![img](https://pic2.zhimg.com/80/v2-8a18d733496592bc9b58011663e3520d_720w.webp)

Prompt: "oil painting of handsome old man, masterpiece"

![img](https://pic2.zhimg.com/80/v2-2b67779a753b73063b5926e9c3dc80c9_720w.webp)

相对于使用普通的 img2img ，边缘线提取的方式可以生成更加清晰完整的图，黑色描边也得到了很好的重绘。

![img](https://pic1.zhimg.com/80/v2-87f6935d7a46d67e12595df639f7ca68_720w.webp)

### 4. M-LSD 线条检测

M-LSD 线条检测用于生成房间、直线条的建筑场景效果比较好。

![img](https://pic4.zhimg.com/80/v2-0a34f6a06447c51f19aaf0470bb831eb_720w.webp)

rompt: "room"

![img](https://pic4.zhimg.com/80/v2-ad82f140140bff707feb834895f37fbb_720w.webp)

Prompt: "building"

![img](https://pic3.zhimg.com/80/v2-cdb416bbb393c1c19de6529e112d707e_720w.webp)

### 5. Normal Map 法线贴图

Normal Map 法线贴图能根据原始素材生成一张记录凹凸信息的法线贴图，便于AI给图片内容进行更好的光影处理，它比深度模型对于细节的保留更加的精确。法线贴图在游戏制作领域用的较多，常用于贴在低模上模拟高模的复杂光影效果。

![img](https://pic4.zhimg.com/80/v2-f8460bebc98db026775cb382ce7ec6bf_720w.webp)

### · RGB 转 BGR

如需要把 Normal map 从 RGB 反转成 BGR 的可把这个选项勾上。（注：因坐标系问题，有时需要反转下通道信息，如生成结果的光照信息和你预期是反的，可能需要勾选此选项）

![img](https://pic2.zhimg.com/80/v2-d7b97642570eed25bd30b4d8a230a571_720w.webp)

### 6. OpenPose 姿态检测

OpenPose 姿态检测可生成图像中角色动作姿态的骨架图，这个骨架图可用于控制生成角色的姿态动作。这个没有涉及手部的骨架，所以手部控制不行有时会出问题。

![img](https://pic2.zhimg.com/80/v2-69da56943407cac0215d05d5c3a42f7d_720w.webp)

![img](https://pic2.zhimg.com/80/v2-248da33312d1d58b5ef571d9ed73193d_720w.webp)

### · OpenPose 姿态及手部检测

OpenPose 姿态及手部检测解决了姿态检测手的问题。如下图有了手部骨骼控制生成的手部效果会更好。

![img](https://pic4.zhimg.com/80/v2-5ea4cf026f838f020760769259e6d4ff_720w.webp)

除了生成单人的姿势，它甚至可以生成多人的姿势，这点非常关键，在此之前AI生成的画面里多个人物的特定动作是几乎无法靠提示词来实现的。

![img](https://pic1.zhimg.com/80/v2-a8ce37e5bc5159e958566be980f4be0c_720w.webp)

通过控制人物姿势，在人物角色设计时也可以得到很好应用。

![img](https://pic4.zhimg.com/80/v2-1c4385a832557a3096f1a9c04224297b_720w.webp)

### 7. PiDiNet 边缘检测（像素差分网络，配合 hed 模型）

PiDiNet 边缘检测生成的线条较粗壮，类似雕刻效果。

![img](https://pic1.zhimg.com/80/v2-f01d497875b2a44fa24f823e1a0ff0e8_720w.webp)

这个预处理器要配合选择 hed 模型效果才会比较好。

![img](https://pic2.zhimg.com/80/v2-eafc4433be9bc3bf405c0c3d11e8630d_720w.webp)

### **8. Scribble 涂鸦（要配合 scribble 模型）**

设置画布高度和宽度，一般默认 512x512 就可以了，点击 “Create blank canves” 创建画布。

![img](https://pic3.zhimg.com/80/v2-127cfe5fef56741b3d125ef91bf6591e_720w.webp)

把画笔调小一点，勾画出想要的图像轮廓（如下图）。

![img](https://pic1.zhimg.com/80/v2-9610db9395f55a8a4cd56c4b7a9dede8_720w.webp)

再添加一些提示词描述，控制下生成效果。

![img](https://pic1.zhimg.com/80/v2-6dd6f71b814d517d2fbd30a68de58a0c_720w.webp)

最终生成的图像效果，如下图。

![img](https://pic2.zhimg.com/80/v2-c35c9d9e6c60aac0b88cae455e936bed_720w.webp)

### · Fake_**Scribble** 伪涂鸦

不用自己画，扔个图片给AI，生成类似涂鸦效果的草图线条。

![img](https://pic1.zhimg.com/80/v2-897660c1e2ae4116317d315108ea3814_720w.webp)

### 9. Segmentation（ADE20k 语义分割，配合seg模型）

语义分割可多通道应用，原理是用颜色把不同类型的对象分割开，让AI能正确识别对象类型和需求生成的区界。

B站大佬的详细视频教程：[https://www.bilibili.com/video/BV1Wg4y1x7Ur](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1Wg4y1x7Ur)

OneFormer 地址：[https://huggingface.co/spaces/shi-labs/OneFormer](https://link.zhihu.com/?target=https%3A//huggingface.co/spaces/shi-labs/OneFormer)

ADE20K 颜色表：[https://drive.google.com/file/d/1lon9OBkWYFwj_xxh9lGFfkcQaZ0ErFAS/view](https://link.zhihu.com/?target=https%3A//drive.google.com/file/d/1lon9OBkWYFwj_xxh9lGFfkcQaZ0ErFAS/view)

![img](https://pic1.zhimg.com/80/v2-8591155f3759d0cce76b07a2b34234ec_720w.webp)

### 10. Binary 二进制（黑白稿提取）

Binary 二进制就是把图像变成只有黑白两色（没有灰），如下图效果。

![img](https://pic1.zhimg.com/80/v2-9e3bfbd0068a4b3c2320d4c6b674ee18_720w.webp)

### 11. Clip_Vision 风格转移（配合 style 模型）

这是近期新出的一个模型，在实际使用中，选择预处理的时候并没有预览图像，猜测是因为风格转移，一种风格并不好预览。

B站大佬教程：[https://www.bilibili.com/video/BV1BL41117ka](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1BL41117ka)

首先生成一张颜色丰富的照片，然后以该照片作为 ControlNet 输入，该预处理器叫做 clip_vision，但是模型叫做 t2iadapter_style。有趣的是可以把一张照片的风格转移到另外一张上，如先生成一把剑，再将上述颜色丰富的照片和剑结合，就可以得到下图效果。

> prompt: just a sword
> Negative prompt: man, woman, person, protagonist
> Steps: 20, Sampler: Euler a, CFG scale: 7, Seed: 2026071917, Size: 512x512, Model hash: fc2511737a, Model: chilloutmix_NiPrunedFp32Fix, ENSD: 31337, ControlNet-0 Enabled: True, ControlNet-0 Module: canny, ControlNet-0 Model: control_sd15_canny [fef5e48e], ControlNet-0 Weight: 1, ControlNet-0 Guidance Start: 0, ControlNet-0 Guidance End: 1

![img](https://pic3.zhimg.com/80/v2-c758b4074c39539c92579bb8d49e6272_720w.webp)

参考：[https://github.com/TencentARC/T2I-Adapter/blob/main/docs/examples.md](https://link.zhihu.com/?target=https%3A//github.com/TencentARC/T2I-Adapter/blob/main/docs/examples.md)

![img](https://pic2.zhimg.com/80/v2-241fc58630cbbf1d13ed001b4f2d0be5_720w.webp)

### 12. Color 色彩继承

色彩预处理后会检测出原图中色彩的分布情况，分辨率影响色彩块的大小。

B站大佬视频教程：[https://www.bilibili.com/video/BV1Uo4y1z7rC](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1Uo4y1z7rC)

![img](https://pic2.zhimg.com/80/v2-22fb1a332250586f732b60a168963c99_720w.webp)

不加任何提示词，生成的图像就艺术感爆棚，观察下颜色和检测出来的颜色分布趋于一致。

![img](https://pic2.zhimg.com/80/v2-ff6bdd896251a6116db8c84b22724b71_720w.webp)

官方介绍 [https://github.com/TencentARC/T2I-Adapter/blob/main/docs/examples.md](https://link.zhihu.com/?target=https%3A//github.com/TencentARC/T2I-Adapter/blob/main/docs/examples.md)

![img](https://pic3.zhimg.com/80/v2-b2397c429bc39e6345fa1fffc793116e_720w.webp)

## 3、附录

### 1. 预处理器与对应模型清单

| 预处理器名称  | 对应ControlNet模型 | 对应腾讯t2i模型                        | 功能描述                                     |
| ------------- | ------------------ | -------------------------------------- | -------------------------------------------- |
| canny         | control_canny      | t2iadapter_canny                       | 边缘检测，适合原画设计师                     |
| depth         | control_depth      | t2iadapter_depth                       | MiDaS深度检测                                |
| depth_leres   | control_depth      | t2iadapter_depth                       | LeReS深度检测                                |
| hed           | control_hed        | 无                                     | 边缘检测但保留更多细节，适合重新着色和风格化 |
| mlsd          | control_mlsd       | 无                                     | 线段识别，识别人物功能极差，适合建筑设计师   |
| normal_map    | control_normal     | 无                                     | 根据图片生成法线贴图，适合CG或游戏美术师     |
| openpose      | control_openpose   | t2iadapter_openpose t2iadapter_keypose | 提取人物骨骼姿势                             |
| openpose_hand | control_openpose   | t2iadapter_openpose t2iadapter_keypose | 提取人物+手部骨骼姿势                        |
| scribble      | control_scribble   | t2iadapter_sketch                      | 应用自画的黑白稿                             |
| fake_scribble | control_scribble   | t2iadapter_sketch                      | 涂鸦风格提取（很强大的模型）                 |
| segmentation  | control_seg        | t2iadapter_seg                         | 应用语义分割                                 |
| binary        | control_scribble   | t2iadapter_sketch                      | 提取黑白稿                                   |
| clip_vision   | 无                 | t2iadapter_style                       | 风格转移                                     |
| color         | 无                 | t2iadapter_color                       | 色彩分布                                     |

### 2. ControlNet 和 T2I-Adapter 有什么区别？

ControlNet 在论文里提到，Canny Edge Detector 模型的训练用了 300 万张边缘-图像-标注对的语料，A100 80G 的 600 个 GPU 小时。Human Pose （人体姿态骨架）模型用了 8 万张 姿态-图像-标注 对的语料, A100 80G 的 400 个 GPU 时。 T2I-Adapter 的训练是在 4 块 Tesla 32G-V100 上只花了 2 天就完成，包括 3 种 condition，sketch（15 万张图片语料），Semantic segmentation map（16 万张）和 Keypose（15 万张）。 两者的差异：ControlNet 目前提供的预训模型，可用性完成度更高，支持更多种 condition detector （9 大类）。 T2I-Adapter ”在工程上设计和实现得更简洁和灵活，更容易集成和扩展” 此外，T2I-Adapter 支持一种以上的 condition model 引导，比如可以同时使用 sketch 和 segmentation map 作为输入条件，或 在一个蒙版区域 (也就是 inpaint ) 里使用 sketch 引导。

### 3. 参考资料汇总

- ControlNet-G站主页：[https://github.com/lllyasviel/ControlNet](https://link.zhihu.com/?target=https%3A//github.com/lllyasviel/ControlNet)
- ControlNet-G站教程：[https://github.com/Mikubill/sd-webui-controlnet#examples](https://link.zhihu.com/?target=https%3A//github.com/Mikubill/sd-webui-controlnet%23examples)
- T2I-G站主页：[https://github.com/TencentARC/T2I-Adapter](https://link.zhihu.com/?target=https%3A//github.com/TencentARC/T2I-Adapter)
- T2I-G站介绍：[https://github.com/TencentARC/T2I-Adapter/blob/main/docs/examples.md](https://link.zhihu.com/?target=https%3A//github.com/TencentARC/T2I-Adapter/blob/main/docs/examples.md)
- 中文教程：[https://openai.wiki/controlnet-guide.html](https://link.zhihu.com/?target=https%3A//openai.wiki/controlnet-guide.html)
- 参考文章：[https://h1cji9hqly.feishu.cn/docx/YioKdqC0oo7XThxvW1ccOmbunEh](https://link.zhihu.com/?target=https%3A//h1cji9hqly.feishu.cn/docx/YioKdqC0oo7XThxvW1ccOmbunEh)
- 模型下载（5G版）[https://huggingface.co/lllyasviel/ControlNet/tree/main/models](https://link.zhihu.com/?target=https%3A//huggingface.co/lllyasviel/ControlNet/tree/main/models)
- 模型下载（700m版）[https://huggingface.co/webui/ControlNet-modules-safetensors/tree/main](https://link.zhihu.com/?target=https%3A//huggingface.co/webui/ControlNet-modules-safetensors/tree/main)

注：700m版为压缩过的16位浮点模型（16fp 表示范围更小，但文件更小，内存需求也更小，每个模型仅700MB）

openpose Editor