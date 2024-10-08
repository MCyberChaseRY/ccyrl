# 第一章：强化学习

## 基本概念

强化学习重点在于解决*序贯决策*问题，这与有监督无监督学习解决预测问题不同。

强化学习是机器通过与环境交互，最终实现目标的计算方法，交互过程为：智能体(Agent)感知到环境状态，给出对应的动作以在环境中交互，环境得到动作后产生奖励信号并转移到下一个动作，智能体继续感知下一个状态，以此类推。

用公式表示为：
$S_t -> A_t -> R_t, S_{t+1} -> S_{t+1} -> ...$

重点在于智能体的感知（知道自己在哪），决策（知道自己该做什么），奖励（知道做了什么会有什么好处）。

## 环境的刻画

## 目标

强化学习的目标在于让智能体知道在自己应对不同的场景时，做什么动作会使其获得最大的好处。

在一场交互过程中，每一轮的每一个动作都会有一个 Reward $r$，将该场交互中所有的 Reward $r$ 累加起来可以得到这一场交互的回报，我们的任务是使智能体的策略在不同的环境中获得最大的价值 $V$（回报的期望），这也是强化学习的优化目标。

## 特殊的概念：占用度量

化学习中有一个关于数据分布的概念，叫作占用度量（occupancy measure），其具体的数学定义和性质会在后面讨论，在这里我们只做简要的陈述：归一化的占用度量用于衡量在一个智能体决策与一个动态环境的交互过程中，采样到一个具体的状态动作对（state-action pair）的概率分布。

占用度量有一个很重要的性质：给定两个策略及其与一个动态环境交互得到的两个占用度量，那么当且仅当这两个占用度量相同时，这两个策略相同。也就是说，如果一个智能体的策略有所改变，那么它和环境交互得到的占用度量也会相应改变。

根据占用度量这一重要的性质，我们可以领悟到强化学习本质的思维方式。

* 强化学习的策略在训练中会不断更新，其对应的数据分布（即占用度量）也会相应地改变。因此，强化学习的一大难点就在于，智能体看到的数据分布是随着智能体的学习而不断发生改变的。

* 由于奖励建立在状态动作对之上，一个策略对应的价值其实就是一个占用度量下对应的奖励的期望，因此寻找最优策略对应着寻找最优占用度量。

## 与有监督学习的区别

有监督学习的任务建立在从给定的数据分布中采样得到的训练数据集上，通过优化在训练数据集中设定的目标函数（如最小化预测误差）来找到模型的最优参数。这里，训练数据集背后的数据分布是完全不变的。

在强化学习中，数据是在智能体与环境交互的过程中得到的。如果智能体不采取某个决策动作，那么该动作对应的数据就永远无法被观测到，所以当前智能体的训练数据来自之前智能体的决策结果。因此，智能体的策略不同，与环境交互所产生的数据分布就不同。

