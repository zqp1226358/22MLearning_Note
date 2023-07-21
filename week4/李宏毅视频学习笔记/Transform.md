## 一、Transformer应用

Transformer就是一个Sequence-to-sequence的model,他的缩写,我们会写做**Seq2seq**

常见的应用有语音辨识、机器翻译、语音翻译、语音合成、聊天机器人、QA、文法剖析、多类别分类、Object detection



## 二、Transformer结构

### 1. 整体结构

整体结构会分为encoder和decoder两部分

input由encoder，decoder决定输出怎样的sequence

从论文的最原始设计看，encoder先注入positional encoding，后续使用Multi-Head Attention模块和Add&Norm两个操作



这里前者Multi-Head Attention模块可以和上节课的自注意力机制联系在一起



>
>
>batch normalization是对不同example,不同feature的同一个dimension,去计算mean跟standard deviation
>——但layer normalization,它是对同一个feature,同一个example裡面,不同的dimension,去计算mean跟standard deviation



Decoder有两种形式，AT和NAT

- AT: 先输入 BEGIN,然后出现 w1,然后再把 w1 当做输入,再输出 w2,直到输出 END 
- NAT:NAT 的 Decoder可能吃的是一整排的 BEGIN 的 Token,你就把一堆一排 BEGIN 的 Token 都丢给它,让它一次产生一排 Token ，如果其中有一个输出了end，其右边就不用显示了

NAT的优点是能够并行化，控制输出的长度，但performance不如AT



encoder 和decoder 的连接  从结构上看 有个residual的设计（残差边？）



## 三、变形的former

比如Local Attention、Reformer、Sinkforn、Linformer等等

具体详见PPT