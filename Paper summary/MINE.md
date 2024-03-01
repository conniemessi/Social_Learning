MINE(Learning Strategic Network Emergence Games)

The paper investigates whether independent reinforcement learning agents in a multi-agent environment can learn to use social learning to improve their performance.

By imposing constraints on the training environment and introducing a model-based auxiliary loss, the paper shows that agents can discover complex skills and adapt online to novel environments by taking cues from experts present in the new environment.

现实世界的网络，特别是由生物主体（例如人类、动物）的行动而产生的网络，是基于旨在最大化个体或集体利益的潜在战略机制的结果。为了捕捉这些战略洞察力，构建用于理解这些机制的学习方法具有解释性和灵活性优势，这些优势对于超越观察是必要的。为此，我们考虑了一个考虑到潜在战略机制的网络生成的博弈论形式，并将其应用于观察到的数据。我们提出了一种新的学习框架MINE（Multi-agent Inverse models of Network Emergence mechanism），它使用多智能体逆向强化学习来解决马尔可夫完美网络生成博弈。

我们的数据包括n个玩家之间的图结构（由节点表示），观察到的结构是这n个玩家在某种未知的收益下进行战略交互的结果。MINE的一个主要创新之处在于明确将网络博弈动态纳入到学习框架中，以同时发现代理人的策略和可能统治观察到网络生成的未知收益机制。

Method

To develop a practical learning framework, we rely on Markov Quantized Response Equilibrium (MQRE) as the solution concept and build our algorithm on the recently proposed inverse reinforcement learning technique, where the learned rewards are Explained as a revenue mechanism. Finding an equilibrium in our setting can be viewed as a combinatorial search task of finding an agent's policy (strategy) that leads to an equilibrium network in the set of all feasible networks. For efficient learning in a graph-structured environment, we use state representation based on graph neural network (GNN) [41], continuous action space, and maximum entropy reinforcement learning algorithms to update the policy in the inner loop of reward learning.

方法：

为了开发一个实际的学习框架，我们依赖于马尔可夫量化响应均衡（MQRE）作为解决概念，并以最近提出的逆向强化学习技术为基础来构建我们的算法，其中学习到的回报被解释为收益机制。在我们的设置中寻找均衡可以被视为在所有可行网络的集合中寻找导致均衡网络的代理人策略（策略）的组合搜索任务。为了在图结构环境中进行有效的学习，我们使用基于图神经网络（GNN）的状态表示，连续动作空间和最大熵强化学习算法来更新奖励学习的内循环中的策略。
