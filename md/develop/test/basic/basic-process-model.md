# 测试理论 - 软件开发过程模型

[[toc]]

# 内容

> 软件开发模型(Software Development Model)是指**软件开发全部过程、活动和任务的结构框架**。
> 软件开发包括需求、设计、编码和测试等阶段，有时也包括维护阶段。 软件开发模型能清晰、直观地表达软件开发全过程，明确规定了要完成的主要活动和任务，用来作为软件项目工作的基础。对于不同的软件系统，可以采用不同的开发方法、使用不同的程序设计语言以及各种不同技能的人员参与工作、运用不同的管理方法和手段等，以及允许采用不同的软件工具和不同的软件工程环境。

![](/_images/test/basic/软件开发模型.png)

软件开发过程模型是**软件开发人员在公司里工作的过程.**

常见的软件开发过程模型

* 瀑布模型
* 快速原型模型
* 增量模型
* 螺旋模型

## 瀑布模型

![](/_images/test/basic/瀑布模型.png)

1970年温斯顿·罗伊斯（Winston Royce）提出了著名的“瀑布模型”，直到80年代早期，它一直是唯一被广泛采用的软件开发模型。

瀑布模型将软件生命周期划分为制定计划、需求分析、系统设计、程序编写、软件测试和运行维护等六个基本活动，并且规定了它们自上而下、相互衔接的固定次序，如同瀑布流水，逐级下落。

**核心思想**

在瀑布模型中，软件开发的各项活动**严格按照线性方式进行**，当前活动接受上一项活动的工作结果，实施完成所需的工作内容。当前活动的工作结果需要进行验证，如果验证通过，则该结果作为下一项活动的输入，继续进行下一项活动，否则返回修改。

**地位**

瀑布模型是最早出现的软件开发模型, 在软件工程中占有重要的地位,它提供了软件开发的基本框架.

**优缺点**

优点:

1. 为项目提供了按阶段划分的检查点,软件开发的每个阶段都很清晰明了
2. 当前阶段完成后,只要去关注后续阶段
3. 可在迭代模型中每轮迭代很类似于一个小的瀑布模型
4. 它提供了一个模版,这个模版使得分析、设计、编码、测试可以在改模版下有一个共同的指导

缺点:

1. 各个阶段的划分完全固定，阶段之间产生大量的文档，极大地增加了工作量
2. 由于开发模型是线性的，**用户只有等到整个过程的末期才能见到开发成果，从而增加了开发风险**
3. 突出缺点是不适应用户需求的变化
4. 软件的实际情况必须到项目开发的后期客户才能看到，这要求客户有足够的耐心

**使用范围**

* 用户的需求非常清楚全面，且在开发过程中没有或很少变化；
* 开发工作对用户参与的要求很低。

## 快速原型模型

![](/_images/test/basic/快速原型模型.png)

快速原型模型的第一步是建造一个快速原型，实现客户或未来的用户与系统的交互，用户或客户对原型进行评价，进一步细化待开发软件的需求。通过逐步调整原型使其满足客户的要求，开发人员可以确定客户的真正需求是什么；第二步则在第一步的基础上开发客户满意的软件产品。

**核心思想**

快速原型是利用原型辅助软件开发的一种新思想。经过简单快速分析，快速实现一个原型，用户与开发者在试用原型过程中加强通信与反馈，**通过反复评价和改进原型，减少误解，弥补漏洞，适应变化**，最终提高软件质量。

**优缺点**

优点:

克服瀑布模型的缺点,**适应需求的变化**,能够开发出更加让用户更加满意的需求

缺点:

1. 所选用的开发技术和工具不一定符合主流的发展；
2. 快速建立起来的系统结构加上连续的修改可能会导致产品质量低下。
3. 使用这个模型的前提是要有一个展示性的产品原型，因此在一定程度上可能会限制开发人员的创新。

**使用范围**

* 不适合大型项目的研发
* 对所开发的领域比较熟悉而且有快速的原型开发工具

## 增量模型

![](/_images/test/basic/增量模型.png)

增量模型又称为渐增模型，是把待开发的软件系统模块化，将每个模块作为一个增量组件，从而分批次地分析、设计、编码和测试这些增量组件。运用增量模型的软件开发过程是递增式的过程。相对于瀑布模型而言，采用增量模型进行开发，开发人员不需要一次性地把整个软件产品提交给用户，而是可以分批次进行提交。

**基本思想**

增量模型在各个阶段并不交付一个可运行的完整产品，而是交付满足客户需求的一个子集的可运行产品。整个产品被分解成若干个构件，开发人员逐个构件地交付产品，这样做的好处是软件开发可以较好地适应变化，客户可以不断地看到所开发的软件，从而降低开发风险。

**优缺点**

优点:

1. 将待开发的软件系统模块化，可以**分批次地提交软件产品**，使用户可以及时了解软件项目的进展
2. 以组件为单位进行开发降低了软件开发的风险。一个开发周期内的错误不会影响到整个软件系统。
3. 开发顺序灵活。开发人员可以对组件的实现顺序进行优先级排序，先完成需求稳定的核心组件。当组件的优先级发生变化时，还能及时地对实现顺序进行调整。

缺点:

1. 要求待开发的软件能给进行增量式的开发,否则会很麻烦
2. 在软件开发过程中需求变化是不可避免的,增量模型的灵活性可以使其适应这种变化的能力大大优于瀑布模型和快速原型模型，但也很容易退化为边做边改模型，从而是软件过程的控制失去整体性.

**使用场景**

* 进行已有产品升级或新版本开发

## 螺旋模型


1988年，巴利·玻姆(Barry Boehm)正式发表了软件系统开发的“螺旋模型]”，它将瀑布模型和快速原型模型结合起来，强调了其他模型所忽视的风险分析，特别适合于大型复杂的系统。

![](/_images/test/basic/螺旋模型.png)

如图所示，螺旋模型沿着螺线进行若干次迭代，图中的四个象限代表了以下活动： 　　

1. 制定计划：确定软件目标，选定实施方案，弄清项目开发的限制条件； 　　
2. 风险分析：分析评估所选方案，考虑如何识别和消除风险； 　　
3. 实施工程：实施软件开发和验证； 　　
4. 客户评估：评价开发工作，提出修正建议，制定下一步计划。

螺旋模型由风险驱动，强调可选方案和约束条件从而支持软件的重用，有助于将软件质量作为特殊目标融入产品开发之中。

**优缺点**

优点:

1. 设计灵活可以在项目各个阶段进行变更
2. 风险驱动,每个项目上线前都要进行风险分析

缺点:

1. 螺旋模型强调风险分析,需要相当丰富的风险评估经验和专门知识,在风险较大的项目开发中，如果未能够及时标识风险，势必造成重大损失；
2. 如果执行风险分析将大大影响项目的利润，那么进行风险分析毫无意义，

使用场景

* 适合使用大规模的软件项目