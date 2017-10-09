# Maester
我们打算搞一个知识库，用来整理和记录平时科研和项目开发当中积累的知识。
目前的Motivation主要有两个：
* **备忘**。毕业了，我们的工作常常就被遗忘了，甚至我们自己也会忘记自己做过的工作。
只留下压缩包里的代码和几篇文档是远远不够的。一个工作真的要被很好地继续下去，
隐藏在代码、论文和实验结果之间的那些没有被详尽记录的细节才是关键。
这些细节往往都是一些对问题和结果的思考与观察，抑或是对于一篇论文的解读和评价，这些细节所构成的知识库，才是一个团队的灵魂。

* **分享**。一个我们自以为完善的工作、一个我们自以为熟悉的领域，其中往往有很多被我们忽略的东西。
这可能是一篇相关的文献，可能是另外一个相关的方法、一个可以参考的系统。一个人的知识结构总是不够完善的，
如果大家可以协同起来完善和分享一个知识库，对大家都是有益的，尤其对刚刚入学的新同学。

于是，先给这么一个有点像笔记，有点像博客，有点像wiki，又有点像知识图谱的四不像取个名字，
就叫Maester吧，取自《冰与火之歌》当中学城里传(wu)道(ren)受(zi)业(di)大学士。

## 怎么写？

### 1.语言
首先为了减轻维护负担，我们目前用中文来写。英文版本以后再考虑。
但是要求：
* 所有的术语和专有名词尽可能用英文表达；
* 所有的内容要客观、简介、准确；
* 所有内容用markdown编写，并遵守下面的结构规范；

### 2.如何参与
首先学会用github和markdown。

我们的知识库用git管理，大家先fork一份到自己的github账号下，然后clone自己的repo。
以我的repo为例
```bash
$ git clone git@github.com:dbiir/maester.git
```
然后推荐大家用intellij来查看和编辑clone下来的内容。intellij的下载和使用：
https://www.jetbrains.com/idea/
community版本就可以。打开它之后，File -> Open -> 选择clone下来的maester目录。

然后就可以用intellij编辑和查看其中的markdown文档。intellij会自动提醒你安装markdown插件，跟着向导做就可以。

编辑完之后，commit到自己的repo中：
```bash
$ git add -A
$ git commit -m 'you message'
$ git push origin master
```

然后根据需要，可以提交pull request到dbiir的maester repo中。管理知识库的同学会审核并给出修改意见，
符合要求的pull request会合并到dbiir的repo中。

### 3.结构规范
clone下来之后，会有一个maester目录，这是maester的根目录，下面简称根目录。

根目录下面会有若干个子目录，每个子目录是一个domain，即一个研究领域，例如：HDFS列存储优化、字符串相似连接、海量RDF数据查询分析等。
一个domain的范围大致等同于一篇毕业论文或者一篇综述论文所涵盖的范围。
每个人可以负责一个domain、另外参与多个domain的维护。一个domain可以由一个或者多个人主要负责。

建议大家开题之后就开始维护一个domain，毕业的时候完成这个domain。

根目录下除了domain目录，还有一个INDEX.md文件，这是所有domain的索引文档，里面列出所有的domain，并分别用一段话描述每一个domain是什么、和其他domain有什么关系。

在一个domain目录下，有若干个markdown文档，每个markdown文档是一个topic。topic可以是一个非常具体的问题或者一篇论文的总结等。

一个Topic的长度尽量不要超过一屏，topic中尽量不要划分章节，如果过长或者需要划分章节，则应考虑拆成多个topic。

topic文档中可以分段，注意每一段只说一个事情，每段第一句话交代本段的关键内容。段落中必须是客观描述，描述务必准确、不要有歧义或指代不清。
每一段的末尾要集中列出该段中用到的参考文献。

每一个domain目录下还有一个INDEX.md文件和一个REF.md文件。INDEX.md是该domain的索引文档列出该domain下的所有topic，并像写综述那要去把topics组织成一个有逻辑的连贯的文档。
REF.md中列出该domain中用到的所有参考文献，并分别简要描述各个参考文件所做的内容以及在哪些topic中被引用了，这相当于是该domain下的一个reading list。