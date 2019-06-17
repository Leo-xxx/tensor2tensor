## 已开源！谷歌将AutoML应用到Transformer架构，实现机器翻译最佳性能

关注前沿科技 [量子位](javascript:void(0);) *今天*

##### 铜灵 发自 凹非寺 量子位 出品 | 公众号 QbitAI

AutoML在NLP领域中的应用又多了新资源。

谷歌最新博客表示，此前在语言建模和翻译等序列任务中，Transformer架构已经展现出了极大的优势，但这些架构几乎均为手动设计，与视觉领域差异巨大。

能不能用更自动的方式应用这一高效的架构？

谷歌研究人员就此一试，找到一种新的Transformer架构，代号**Evolved Transformer**（简称**ET**）来测试自动机器学习方法AutoML在Transformer架构中应用如何。

和以往其他Transformer不同，ET能够根据特定任务进行定制，在机器翻译领域得到了最先进的结果，并且对语言建模任务也进行了改进。

这条推特发出后收获了不少关注，目前有800多个点赞，近300人转发了这项研究。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtA4cHOuHJibUghtT1ypRqwhcBjsMl1ysSjqEiajT08n4y15hpeZ1WicZicF1icI4of3N8GAgS2CBdxtYgw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

网友对此表示认可，表示和人类教机器相比，机器教机器才是正解嘛！

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtA4cHOuHJibUghtT1ypRqwhcXqCPj0JetG0frH5AZYW5vh7QVo03xs6N5bMLehibQDnubbiaDWMvJuIA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

目前，Evolved Transformer已开源，也是Google基于TensorFlow新架构Tensor2Tensor的一部分了，任何人都可以免费使用。

## “混合体”架构

想要在翻译任务上进行大规模NAS（神经网络架构搜索），必须先要评估每个架构的适应性任务。在这个预热阶段，有两种方法。

一种是通过暖启动（warm starting）的方式，研究人员在初始种群中用Transformer进行播种，不采用随机模型，这有利于在搜索空间中的搜索。

第二种方法被称为Progressive Dynamic Hurdles (PDH)，增强了进化搜索，将更多资源分配给更强健的候选者，若模型不好则PDH就会终止评估，重新分配资源。

利用这两种方法，研究人员在机器翻译上进行大规模NAS，找到了Evolved Transformer。

和大多数序列到序列的神经网络架构类似，Evolved Transformer的编码器能将输入序列作为嵌入，解码器能将嵌入输出序列。

Evolved Transformer还有一个有趣的特点，它的编码器和解码器模块底部的卷积层的添加模式很有意思，在两个地方都以类似的分支模式添加，即在合并到一起时，输入通过两个独立卷积层。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtA4cHOuHJibUghtT1ypRqwhc4QoHdEj8uMWcmVt0MHV4SRwDTcr0CjOp9PnnUqxQdVDLkbicgHibXrcA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上图为Evolved Transformer（右）与最初Transformer编码器架构对比。

虽然最初的Transformer架构依赖于自注意，但Evolved Transformer为一个混合结构，利用了自注意和宽卷积。

## SOTA结果

研究人员进行了不同类型的测试，证明Evolved Transformer是有效的。

先是用英语到德语的翻译任务，对Evolved Transformer和原始Transformer进行对比。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtA4cHOuHJibUghtT1ypRqwhcf25j70SbFKpAGXAclpEqPHdO0K9WQyueZ0j9NDUtogpcUMb6679BMg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果显示，在所有参数size下，Evolved Transformer的BLEU和perplexity performance的表现均超越原始Transformer。

此外，在WMT14 En-De英语-德语测试集上，Evolved Transformer实现了最佳性能，BLEU得分为29.8，SacreBLEU得分为29.2。

研究人员还在不同NLP任务上对比了这两种Transformer架构。

他们测试了用不同语言对的翻译任务，Evolved Transformer有所提升，其margin与英语-德语类似。因为新模型高效利用参数，因此对中型模型的提升较大。

在利用LM1B进行语言建模时，Evolved Transformer性能提升了将近两个perplexity。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtA4cHOuHJibUghtT1ypRqwhcQvTkZvI4lYQ8iaOeVLqzLdG85sk0ibHSBibG2P8ZtX2N2AFBN7vxPnrSQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 传送门

Google官方博客：
https://ai.googleblog.com/2019/06/applying-automl-to-transformer.html

开源地址：https://github.com/tensorflow/tensor2tensor/blob/master/tensor2tensor/models/evolved_transformer.py

论文地址：
https://arxiv.org/abs/1901.11117

— **完** —

**小程序|全类别AI学习教程**

[![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtDpADEKp9rvicB48XgA8ueVdwNbXM1wibYx0ic2pYicwu3UCU5BM6fpDvbH8c4e9JV3uGvYaWAhvGiaTVQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=MzIzNjc1NzUzMw==&mid=2247523311&idx=5&sn=d1cb9f9cfb03a0d7ba3e4358883e233a&chksm=e8d02c9ddfa7a58b8843750299eedc28dc3ef548247d02573366eca469100e0b08afa609d96e&mpshare=1&scene=1&srcid=&key=90581f21d61583cc4ba5175117ebb8176a467076b1c422572069fb9ec7be480366a2f433313c0720067c38281c9a622c76e93a602eedf835c6f6aa7d2176fe526984ab42f55b3c2ad5882b5a2e58ff69&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=lSXmjyoUzLt6sFLOXrRFLTDRyJ5BUSGQ7PkWTjG%2FqLBF52iwTvO2c5rdGGHprOuH)

**AI社群|与优秀的人交流**



![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtDcZyEBVM81oW4VRoNAibJWw1qt2Fxv2MINM4SsViaaOsD7exDSlDnoBKicLIXhuZlgPEPrne0p3NqNg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtCQYLj62wpY5xicKlLfDCpKV2aTXlvJODSNPV9Q3zHNEu7UibkwluIwr0TN705vZawerScqBhC67HDQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



**量子位** QbitAI · 头条号签约作者





վ'ᴗ' ի 追踪AI技术和产品新动态

   喜欢就点「在看」吧 ! 













微信扫一扫
关注该公众号