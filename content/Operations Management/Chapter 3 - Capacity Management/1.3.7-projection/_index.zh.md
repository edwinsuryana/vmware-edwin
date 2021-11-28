---
title: "7. 投影"
date: 2021-06-14T11:43:43+10:00
draft: false
weight: 70
---

预测的准确性取决于数据量和周期长短。具有季度末高峰的工作负载自然至少需要 6 个月才能准确。如果有足够的数据，vRealize Operations 将考虑 6 个月以上的数据。虽然它对最近的数据给予了额外的重视，但如果出现突然但持续时间短的变化，它可能不足以影响预测。

![峰值比较](1.3.7-fig-1.png)

短期和一次性的瞬态峰值不应影响容量规划，因此在预测中影响可能并不明显。

持续的峰值将持续更长时间并影响预测。如果峰值不是周期性的，由于指数衰减，对投影的影响将随着时间的推移而减少。

周期性峰值表现出周期性模式或波。例如，每小时、每天、每周、每月、每月的最后一天等。可以有多个重叠的循环模式，它们也会被检测到。虽然您不应仅根据几天的数据做出容量决策，但您确实需要 5 分钟的粒度作为输入。应考虑每小时重复一次的 5 分钟高峰。

如果您没有 3 个月而只需要总体尺寸，请考虑使用第 97 个百分位值。为什么是第 97 个百分位？它基于标准差原理。距离中点的两个 [标准差](https://en.wikipedia.org/wiki/Standard_deviation) 等于 95%，3 个标准差 = 99.7%。因此，第 97 个百分位数在 2 SD 和 3 SD 之间提供了良好的平衡。通常，它会捕获适量的峰值和异常值。

**剩余容量（%）** 使用的是未来 3 天的预测值，因此它可能与当前使用的容量不同。由于是未来值，所以存在置信区间。您可以在激进（基于带的上限）和保守（基于实际轨迹）之间进行选择。另一方面，如果当前利用率超过可用容量，vRealize Operations 会将剩余容量的值设置为 0%。

请注意，CPU 剩余容量 (%) 和剩余内存容量 (%) 在策略中显示为已启用，但无法使用。这是一个应该隐藏的内部指标。

![缓冲区和 HA 容量](1.3.7-fig-2.png)

**剩余时间** 衡量容量耗尽前的天数。最长预测为1年，超过1年的时间只显示为1年。保守值基于剩余容量预测的上限。

**剩余虚拟机** 衡量可以装入集群的平均大小的 VM 数量。平均 VM 大小是自动计算的，因此它会随着时间和集群而变化。 vSphere 数据中心和 vCenter 级别的其余 VM 只是子集群的总和。未计算这些级别的平均 VM 大小，因此您喜欢混合大小。此外，VM Remaining 值不会低于 0。数据中心可能会显示正的 VM Remaining 值，即使其成员集群之一短暂下降。

**推荐大小** 基于规划窗口中的最高投影值，而不是窗口末尾的投影值。默认情况下，VM 的规划窗口为 60 天。这来自于30天配置缓冲+30天（剩余时间的默认阈值在绿色区域，如截图所示）。

![剩余时间滑块](1.3.7-fig-3.png)

如果 VM 使用量随着时间的推移而增加，预测可能会随之而来，您将获得一个在未来 60 天内存在的数字。

如果您的操作可以经常调整，请将剩余时间窗口更改为 0。这将提供 30 天的调整期。

请注意，推荐的内存大小四舍五入到最接近的 GB。

![推荐内存](1.3.7-fig-4.png)