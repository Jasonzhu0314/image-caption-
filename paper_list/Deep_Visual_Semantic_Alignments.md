# Deep Visual-Semantic Alignments for Generating Image Descriptions
## 1. 主要思想
   我们通过将文本作为弱标签充分利用利用图片-文本数据集，句子中词的临近的分割等于一些特定成分，但是并不知道对应图片中的什么位置。我们的方法是推断图片中的区域和文本对齐，并使用这些图片文本对去训练文本生成模型。
   
   （1）我们设计一个深度神经网络去推断句子片段和他们所描述的图像区域之间的潜在关系。我们的模型通过多模型嵌入空间和一个结构化目标将两种模型连接起来。我们在图文检索实验上评估这种方法的有效性，并达到了STOA
   （2）

## 2. 我们的模型
   我们介绍一个模型，对齐文本片段到视觉区域，并通过多模型嵌入描述他们，在训练的时候将对齐的文本用于第二阶段的训练
### 2.1 Representing
   （1）描述图片（representing image）：
使用RCNN，使用预训练过后的CNN模型，将一张图片转化为4096维的向量。

   （2）描述句子（representing sentences）：
这点类似于机器翻译，直接翻译的话相当于没有考虑语言中句子的顺序，和词内容信息，为了解决这个问题，我们提出了双向RNN，每个词被定义为字典中的one-hot向量，加入已经训练好的300维的word-embedding，在训练的时候被固定，BRNN的输出St是词的位置和它周围的内容的一个函数，技术上说，每一个St代表了一句话中的整个句子，但是我们实验发现，这个词表示St和word在位置II的视觉概念对齐。
### 2.2. 对齐目标：
   A. Karpathy, A. Joulin, and L. Fei-Fei. Deep fragment embeddings
for bidirectional image sentence mapping. arXiv preprint arXiv:1406.5679, 2014.
  论文中推断图片部分和句子中的词段的点积能够被作为相似性估量，如果说句子中的词段和图片中的部分对齐的话，点积会有很大的值，也就代表两个形式之间对齐。
这就说明了在训练的过程中，必须要让图片和句子转化为相同的嵌入空间，才能让图片和句子进行匹配。
## 3.缺点：
（1）在生成图片区域所对应的文本的时候，由于区域描述过于综合性和丰富性，不能被考虑加入到句子的生成中去，例如，纽带扣，烟囱，空调加湿器等等，
Grounded Image Sentence Retrieval这个词要怎么解释
## 4.优点：
生成句子的长度不一样，生成的单词多样性

生成文本与以前论文的区别：
以前的一部分方法生成image caption都是基于固定的模板，固定的模板都是那种基于图片的内容或者生成语法，但是这种方法限制了输出的多样性。
kior也提出了一种双线性模型能够生成一个句子的完整描述，但是模型使用固定的窗口内容长度，我们的模型是根据以前生成的词产生后面的词。



