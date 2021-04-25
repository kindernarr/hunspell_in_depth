# 向德语系学生介绍hunspell

本文准备长期更新。

我们学习hunspell的目的，主要是为了研究词典软件里面的词形还原，而不是为了拼写检查。

我将需要用到的文件全部放在以下链接：

[hunspell_in_depth](https://pan.baidu.com/s/1HDlBubR1IIGb14v0i_p3Dg) 提取码: rc9v

在这些文件中，manual文件夹的**man 4 hunspell.pdf**最重要，其次重要的是tests.rar中的示例。



首先明确两点：

1. hunspell是不考虑上下文的单词拼写检查工具。
2. hunspell是基于规则而非概率的词形还原工具。

语料处理中用到几种工具，在此区分一下：

1. tokenizer

   tokenizer把一句话中用空格或标点隔开的词一个个断开，比如：

   Wir sind nicht Staub im Wind. 

   Wir, sind, nicht, Staub, im, Wind.

2. lemmatizer	把词语的屈折形式转化为原形，比如：

   findet -> finden.

3. stemmer	把一个词的词干提取出来，本文中不作“词根、词干、词基”等区分，把一个词去掉词尾的部分称为词干，比如： finden -> find.

4. compound word breaker	把复合词中的组成成分剥离出来，比如德语中“引号”是Anführungszeichen，那么： Anführungszeichen -> Anführung, s, Zeichen. 其中，s是Fugenelement 。
   
5. part-of-speech tagger	词形标注工具，能把一个词是阴性还是阳性，是单数第三人称现在时，还是负数第一人称过去完成时等语言信息分析出来，此类工具的代表是[TreeTagger](https://www.cis.lmu.de/~schmid/tools/TreeTagger/). Hunspell只能实现非常简陋的语法标注能力，而且目前我们实际使用的德语词典文件和规则文件都不提供语法信息。

6. grammar checker	语法检查工具。比如office的德语语法检查插件能够以最新正字法为标准，对一篇文章进行语法检查。



tests文件夹里有许多子文件夹，每个子文件夹提供一个实例，往往涉及到man 4 hunspell中提到的一方面。
一个子文件夹内的文件的文件名有着相同的开头，但扩展名不同。
比如：

- needaffix2.dic
- needaffix2.aff
- needaffix2.morph
- needaffix2.good



我们先看看这些扩展名：

- .dic	词典文件，里面的内容类似纸质词典里的词头(lexem)。
- .aff	还原规则集，里面写了怎样把一个加了前缀后缀或与其他词语复合的复杂形式，转化为一个词典中存在的词头的许多组规则。
- .morph	Hunspell程序在Linux Shell里面运行的结果。
- .good	能通过语法检查的正确词形。
- .wrong	不能通过语法检查的错误词形。
- .sug	针对错误词形或正确但罕见的词形，hunspell会认为用户拼错了，会推荐一些它认为正确的词形供采纳。
