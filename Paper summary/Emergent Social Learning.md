Emergent Social Learning via Multi-agent Reinforcement Learning


Summary:
We are able to obtain generalized social learning strategies that enable agents to: i) discover complex skills that cannot be learned from single-agent training; ii) adapt to new environments online by taking cues from experts present in the new environment.

总括：
我们能够获得广义社会学习策略，使智能体能够：i）发现从单一智能体训练中无法学到的复杂技能；ii）通过从新环境中存在的专家那里获得线索，在线适应新环境。


The difference from imitation learning:
Interactions in social learning are directly mediated by the environment. A novice can acquire problem-solving skills by watching a selfish expert perform the same task without explicitly imitating the expert. Beyond simple imitation, social learning enables individuals to develop complex behaviors or innovations from others that a person would not be able to discover from scratch in a lifetime.

与模仿学习的区别：
社会学习中的交互是直接由环境介导的。一个新手通过观察一个自私的专家完成相同的任务就可以获得解决问题的能力，而无需明确模仿专家。除了简单的模仿，社会学习使得个人能够从他人的基础上发展出复杂的行为或创新，这是一个人在一生中无法从零开始发现的。

具备社会学习能力的人类和动物能够在没有外部系统介入的情况下，识别与自身兴趣相关的
任务专家并从他们那里学习。在新环境中，社会学习使得能够"在线适应"新任务，这是模仿学习无法做到的。

Setting:
Humans and animals with social learning capabilities are able to identify and learn from experts on tasks relevant to their interests without the intervention of external systems. In new environments, social learning enables "online adaptation" to new tasks, which imitation learning cannot do.


Focus on two hypotheses related to social learning: H1) Social learning can discover more complex strategies that are difficult to discover through expensive individual exploration; H2) Social learning can be used when the social learning strategy encodes how to learn from cues from experts , online adaptation in new environments.

Settings representative of real-world human environments: Multi-agent reinforcement learning (MARL). This setting represents real-world multi-agent problems, such as autonomous driving.

When social learning occurs, it enables agents to learn more complex behaviors than agents and experts trained alone can achieve on their own.

问题设置
关注与社会学习相关的两个假设：H1）社会学习可以发现通过昂贵的个体探索难以发现的更复杂的策略；H2）社会学习可以用于当社会学习策略编码了如何从专家的线索中学习时，在新环境中进行在线适应。

代表真实世界人类环境的设置：多智能体强化学习（MARL）。这个设置代表了现实世界的多智能体问题，比如自动驾驶。

当社会学习发生时，它使代理能够学习到比单独训练的代理和专家自己还要复杂的行为。

Model-Free Sparse Reward Social Learning
Consider an example environment where an agent must first pick up a key and use it to get through a door to a target. In this sparse reward, hard-to-explore environment, the agent only receives rewards when it reaches the goal; at other times, the reward is 0. Suppose there is an unlimited supply of keys, and when one agent passes through the door, it closes - so that other agents cannot change the environment to make the task easier. Instead, the expert agent can exhibit a new state s~ that is difficult to generate through random exploration: open the door. We hope that the novice agent will learn this exemplary state s~ by updating its internal representation, and eventually learn how to generate this state.

Consider Q-learning, where Q(a,s)=𝔼π{[}∑t=0∞γt rt+1|a,s{]} represents the total expected reward of taking action a in state s. Since the agent will only receive 0 rewards during training, all Q values will approach zero. Even if the agent observes a useful new state s~, since Q(a,s)→0,∀a∈𝒜,s∈𝒮, the goal of Q-learning becomes:
Q(s~,a)=r+γmaxa′Q(s′,a′)=0+γ0=0(2)
Therefore, this goal forces the value of Q(s~,a) to be zero. In this case, in order to produce an output of zero, there is no need to model entering or leaving state s~, since all other Q values are already zero. As can be seen from both cases above, before a model-free reinforcement learning agent receives rewards from the environment, it will have a hard time modeling new states or transition dynamics, making learning from expert cues particularly difficult.

Social Learning with Auxiliary Losses
A method for increasing model-based prediction losses in novice agents. Specifically, we add an additional layer θA based on the policy network encoding the current state st, as shown in Figure 1. We introduce an unsupervised mean absolute error (MAE) auxiliary loss to train the network to predict the next state st+1, given the current state st and action at:

If the new presentation state is in a trajectory, s^k∈(0,T), then the term |s~k−s^k| will be part of the goal. It is non-zero only if the agent learns to perfectly predict the new presentation state. Thus, cues from the expert will provide gradients that enable a novice to improve its representation of the world, even if it does not receive any reward from the demonstration. This architecture also implicitly improves the agent's ability to model the strategies of other agents, since in order to accurately predict the next state, it must correctly predict the actions of other agents. It can do this without explicit access to the other agent's state or actions, or even any labels indicating which elements in the environment constitute the other agent. We call our approach social learning with an auxiliary prediction loss and hypothesize that it will improve the agent's ability to learn from expert cues.

Social Learning Environments
Humans and animals are most likely to rely on social learning when individual learning is difficult or dangerous
A novel environment specifically designed to encourage social learning by making individual exploration difficult and expensive and introducing prestige cues is introduced.



Model-Free Sparse Reward Social Learning
考虑一个示例环境，其中代理必须先拿起一把钥匙，并使用它通过门到达目标。在这个稀疏奖励、难以探索的环境中，代理只有在到达目标时才能接收到奖励；其他时间，奖励都为0。假设有无限供应的钥匙，并且当一个代理通过门后，它会关闭 - 这样其他代理就无法改变环境以使任务变得更容易。相反，专家代理可以展示一个通过随机探索很难产生的新状态s~：打开门。我们希望新手代理能够通过更新其内部表示来学习这个示范状态s~，并最终学会如何产生这个状态。

考虑Q学习，其中Q(a,s)=𝔼π{[}∑t=0∞γt rt+1∣a,s{]}表示在状态s中采取动作a的总期望奖励。由于训练过程中代理只会收到0的奖励，所有的Q值都会趋近于零。即使代理观察到一个有用的新状态s~，由于Q(a,s)→0,∀a∈𝒜,s∈𝒮，Q学习的目标变为：
Q(s~,a)=r+γmaxa′Q(s′,a′)=0+γ0=0(2)
因此，该目标迫使Q(s~,a)的值为零。在这种情况下，为了产生一个零的输出，不需要对进入或离开状态s~进行建模，因为所有其他的Q值已经为零。从上述两种情况可以看出，在无模型强化学习代理从环境中获得奖励之前，它将很难对新的状态或转换动态进行建模，这使得从专家的线索中学习变得特别困难。

Social Learning with Auxiliary Losses
在新手代理中增加基于模型的预测损失的方法。具体而言，我们在策略网络对当前状态 st 进行编码的基础上，添加了额外的层 θA，如图1所示。我们引入了一个无监督的平均绝对误差（MAE）辅助损失，用于训练网络来预测下一个状态 st+1，给定当前状态 st 和动作 at：

如果新的演示状态在一个轨迹中，s^k∈(0,T)，那么术语 |s~k−s^k| 将成为目标的一部分。只有当代理学会完美地预测新的演示状态时，它才不为0。因此，来自专家的线索将提供梯度，使新手能够改善其对世界的表示，即使它没有从演示中获得任何奖励。这种架构还隐含地提高了代理建模其他代理策略的能力，因为为了准确预测下一个状态，它必须正确预测其他代理的动作。它可以在没有明确访问其他代理的状态或动作的情况下做到这一点，甚至没有任何指示环境中哪些元素构成其他代理的标签。我们将我们的方法称为带有辅助预测损失的社交学习，并假设它将提高代理从专家线索中学习的能力。

Social Learning Environments
当个体学习困难或存在危险时，人类和动物最有可能依赖社会学习
引入了一个专门设计的新颖环境，通过使个体探索困难和昂贵，并引入威望提示，来鼓励社会学习。
