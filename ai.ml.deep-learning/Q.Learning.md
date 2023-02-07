
# Reinforcement Learning

## What is Reinforcement Learning?

**Environment** - the AI will perform in ca certain environment.
**Agent** - It is the AI that will learn from the environment.
**Action** - The agent will perform certain **actions** in the **environment**.
**State** - The state of the agent in the environment which will be changed by the actions.
**Reward** - The reward is the **feedback** from the environment to the agent. It is a number that indicates how good the agent performed in the current state.

The agent will keep making actions in the environment and will learn from the reward. The goal is to **maximize** the reward.
By this the agent will learn the environment and will be able to perform better in the future.

## The Bellman Equation

s - State
a - Action
R - Reward
$\gamma$ - Discount Factor
V - Value of the state

starting form this equation:

$$ V(s) = \max _a (R(s,a) + \gamma V(s')) $$

If the Agent is in state $s$ it can perform action $a$ and will get reward $R(s,a)$ and will be in state $s'$. From all possible actions the agent will choose the one maximum one: $\max _a()$.

The discount factor $\gamma$ is discounts the value of the state $s'$ as it is further away from the wanted state.

## Markov Decision Process (MDP)

**Deterministic Search** - The agent will **always** choose the same action in the same state.
**Non-Deterministic Search** - The agent will choose the action based on probability. (stochastic search)

**Markov process** is a stochastic process where the future is **independent** of the past given the present. The Markov property is that the future is independent of the past given the present.

**Markov Decision Process** is a Markov process where the **agent** can choose an action. The agent will choose the action based on the reward.

$$ V(s) = \max _a (R(s,a) + \gamma  \sum _{s'} P(s,a,s') V(s') ) $$

where $P$ is the **probability** of the transition from state $s$ to state $s'$ by performing action $a$.

## Policy vs Plan

**Plan** - The plan is the **sequence** of actions that the agent will perform. The plan is the **best** sequence of actions in the current state.

**Policy** - The policy is the **strategy** of the agent. It is a function that maps the state to the action. The policy is the **best** action in the current state.

## Living Penalty

The agent will get a **living penalty** if it does not reach the goal. The **living penalty** is a `negative` reward that the agent will get if it does not reach the goal. The living penalty will encourage the agent to reach the goal as soon as possible.

## Q-Learning

MDP - Markov Decision Process

$$ V(s) = \max _a (R(s,a) + \gamma  \sum _{s'} P(s,a,s') V(s') ) $$

$Q(s,a)$ - "quality" of the action and depends on the possible future rewards.

$$ Q(s,a) = R(s,a) + \gamma  \sum _{s'} P(s,a,s') V(s') $$

so:

$$ Q(s,a) = R(s,a) + \gamma  \sum _{s'} P(s,a,s') \max _{a'} (Q(s',a')) $$

The algorithm based on the model above is called **Q-Learning**.

## Temporal Difference

$$ Q(s,a) = R(s,a) + \gamma  \sum _{s'} P(s,a,s') \max _{a'} (Q(s',a')) $$

easy representation:

$$ Q(s,a) = R(s,a) + \gamma \max _{a'}Q(s',a') $$

but keep in mind that by $ \gamma \max _{a'} Q(s',a') $ we mean $\sum_{s'} P(s,a,s') \max _{a'} (Q(s',a')) $

The $Q(s,a)$ is the **quality** of the action $a$ in the state $s$ which is recalculated by the **reward** $R(s,a)$ and the **future reward** $ \gamma \max _{a'}Q(s',a') $.
Then is compared with the current $Q(s,a)$  and the difference is calculated:

$$ TD(a,s) = R(s,a) + \gamma \max _{a'}Q(s',a') - Q(s,a) $$

$TD$ - stands for **Temporal Difference**.

to update the $Q(s,a)$ we use the **learning rate** $\alpha$:

$$ Q(s,a) = Q(s,a) + \alpha TD(a,s) $$

adding the time to the formula to emphasis the iterative nature of the algorithm:

$$ TD(a,s) = R(s,a) + \gamma \max _{a'}Q(s',a') - Q_{t-1}(s,a) $$

$$ Q_t(s,a) = Q_{t-1}(s,a) + \alpha TD(a,s) $$

Full equation of the algorithm:

$$ Q_t(s,a) = Q_{t-1}(s,a) + \alpha (R(s,a) + \gamma \max _{a'}Q_{t-1}(s',a') - Q_{t-1}(s,a)) $$

$\alpha$ - learning rate - has influence on the speed of the learning. The higher the $\alpha$ the **faster the learning** but the algorithm will be **more unstable**.
