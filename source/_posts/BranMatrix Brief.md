---
title: BranMatrix Brief
date: 2016-08-21 22:51:37
tags:
---

<div align="center">
<img src="/images/BrainMatrix/BrainMatrix.jpg" width = "500" height = "200" alt="图片名称" align="center" />
</div>

# 简介
　　随着计算机机器学习领域的突飞猛进，市场对人工智能的热情也越来越高，产出一个灵活性高、扩展性强的机器学习框架是相关从业者的心声。
　　开源项目MXNET是由百度IDL深度学习实验室李沐、卡耐基梅隆大学陈天奇组织开发的一个深度学习框架，基于CXXNET, 用mshadow来做具体的数据计算，C++保证运行效率的轻量级开源平台。 在其它各种开源平台中综合性能突出，现在也在飞速发展中。
　　而我们开发的BrainMatrix项目基于MXNET，不仅是深度学习，而且集成机器学习算法都适用的scala语言计算平台。

# MXNET特点
1、轻量级调度引擎。
2、符号计算支持。
3、混合执行引擎。
4、支持多GPU运算和分布式计算（核心竞争力）
5、代码简洁高效。
# BrainMatrix特点
1.具有MXNET以上的所有特点，而且对使用者提供了更多自定义的可能。
2.Scala语言一方面吸收继承了多种语言中的优秀特性，一方面右没有抛弃Java这个强大的平台，运行在JVM之上，轻松实现和Java类互联互通。它既是纯面对对象语言，又支持函数式编程，并且它确是严格意义上的静态语言。
3.相对于C++而言，Scala更加易于机器学习从业者学习和使用，提供更多DIY（自定义）操作。
4.Scala 语言也是分布式框架Spark的原生语言，易于和Spark完成对接工作。
5.将提供其它机器学习接口，比如ladder Network, Spiking等。

# 组织结构
　　MXNET主要分为三个层次：Symbol Graph , Computational Graph，Operator。这三个层次依次递减，Symbol Graph负责抽象计算图，提供接口。Computational Graph 负责生成节点计算图和优化计算图，分配GPU和内存空间。Operator提供具体的运算。分工明确，组织合理。
　　MXNET-Scala框架则是将Symbol Graph部分，用Scala实现并改进，使Scala部分有了更多的操作范围和空间。
<div align="center">
![jpg](/images/BrainMatrix/architecture_2.jpg)
</div>
