---
title: "6. 性能 SLA"
date: 2021-06-13T15:03:58+10:00
draft: false
weight: 60
---

谷歌“性能SLA”VMware，你只会找到几篇相关的文章。字符串性能 SLA 必须在引号内，因为它不是性能和 SLA，而是 **性能 SLA**。是的，我正在寻找带有性能 SLA 字样的网页。如果您只是在没有报价的情况下使用谷歌搜索 VMware Performance SLA，您将得到许多不相关的结果。

我只是在 2021 年 3 月 14 日再次尝试。Google 返回的结果不到 20K，高于 2015 年 10 月的 1.6K 结果。前 10 个如下所示。注意其中 8 个来自我的博客、书籍或演讲活动。来自 [Sunny Dua](https://sunnydua.com/) 的一项，谈论我们提出的相同性能 SLA 概念，出现在前 10 名。最后一项来自 Michael Webster，他曾在 VMware 工作几年前。

![谷歌结果截图](1.2.6-fig-1.png)

我检查了前 10 个结果。除了我自己的文章，谷歌只返回了少数相关文章。如果您仔细阅读，其余的实际上并不相关。相关文章提到了性能 SLA，但没有定义和量化性能 SLA 是什么。如果某件事没有量化，那就是主观的。如果界限不明确，就很难快速、一致地与客户达成正式协议。如果您与客户，尤其是付费客户存在分歧，请猜猜谁会赢。

可用性 SLA 可在停机时为您提供保护。性能 SLA 在出现性能问题时为您提供保护。

vSphere 的性能 SLA 在下表中定义：

![vSphere 性能 SLA - 服务等级](1.2.6-fig-2.png)

使用典型的 30 天月份

你知道为什么你应该只使用 CPU Ready 而从 Performance SLA 中排除 CPU Co-Stop 和 CPU Contention 吗？

我花了很多年才意识到这个错误。

答案在本书末尾的 [第 4 部分：测验答案](/zh/miscellaneous/chapter-1-quiz-answers/4.1.1-part-1-operations-management/) 中。

绩效管理的全部意义在于能够_在客户抱怨之前_知道问题。如果您不能在客户之前看到问题，那么您就没有进行绩效管理。 _manage_ 这个词意味着积极主动。被动等待警报或投诉触发故障排除过程不是管理。 Proactive 需要一个比外部正式商定的 SLA 更严格的内部阈值。这就是 KPI 的来源。