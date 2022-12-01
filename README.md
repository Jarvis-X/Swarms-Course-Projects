# HW1 - A point mass goes down a parabola then falls freely
- For interactive notebook, go to https://colab.research.google.com/drive/12gTb8SFlF5goO58rhXWqk-Ulhv4A8K08?usp=sharing
- We have a rectanglular area in $2D$ of size $l\times h$ along axes $\boldsymbol{x}$ and $\boldsymbol{y}$, of which the lower left corner is placed at $\left(-\frac{l}{2}, 0\right)$. The walls of the rectangle are not penetrable, which define the ***playground*** of this simulation. 
We release a number of $n$ circular unactuated objects in the playground and simulate the motion of these objects. We highlight an additional rule that the bounding walls boost/nerf the velocity of the circular objects by $p_x\% \text{ and } p_y\%$, *i.e.*, if an object collides with a vertical wall with a velocity vector of $\boldsymbol{v} = \left[v_x, v_y\right]$, then its velocity becomes $\left[-\left(1+\frac{p_x}{100}\right)v_x, v_y\right]$ after the impact. The objects can collide with each other while perserving their momentum and kinetic energy up to a maximum impact force.

# HW2 - $\epsilon$-greedy and UCB
* For interactive notebook, go to https://colab.research.google.com/drive/1PZT9xVR3YC5UJL0eWh2stUKO_czM672M?usp=sharing
### Epsilon greedy

10% of the explorations are for exploration. In each iteration, a random number between 0 and 1 is given. If the random number is between 0 and 0.1, then the program randomly selects a bandit, extracts the reward, and adds to the total reward. The reward is averaged out with the previously extracted rewards that belong to the bandit, and the average reward is used for the greed.

90% of the explorations are for greed. If the random number is between 0.1 and 1.0, the program selects the bandit which has the highest average reward, and extracts the reward which adds to the total reward.

### Upper-Confidence-Bound

Instead of allocating a certain proportion of operations for exploration, UCB integrates a exploration term in the maximization objective function in addition to its avergae reward. This term increases as the number of operations where a bandit is not selected increases, and decreases as the number of operations where a bandit is selected decreases. Such proporty makes the program revisit the less visited bandits even if it used to give slow rewards. I initialized the uncertainties at maximum to make sure all bandits deserve a visit at least.

### Visualization

The first plot shows the total reward comparison between the three policies across all trials.

The second plot shows the change of total reward of the poliocies in one trial.

The third plot shows the optimal rate of the policies in one trial.

### Epsilon-greedy V.S UCB

Through tweaking the mu and sigma in the second cell, I figure out UCB works extra well when the uncertainty is high. Even if the rate of selecting the bandit with the maximum mean value is not significantly higher than that of ϵ-greedy, UCB can still get a higher total reward because of the frequent revisit to the more uncertain bandits. When the variation is high, such revisit often blurs the boundary of rewards between bandits with close mean, which is uncaptured by the ϵ-greedy method.


# HW3: Policy iteration and Value iteration

* For interactive notebook, go to: https://colab.research.google.com/drive/1GY2FlfP-f-kNGjIkGo5mOBnqDHK_Euj7?usp=sharing

* Fisrt block: setup and parameter initializations

* Second block: evaluating the value function of a future state

* Third block: implementation of policy evaluation, tested with 2 robots in a 6x6 environment. γ is set to 0.2 to avoid overflow. The visualization represents the value function of all possible states robots.

  Each non-goal step grants a penalty of -1. Thus, the robots seek to reach the goal in a number of steps as low as possible. Goals are encouraged by assigning a reward of 0. Collisions are avoided by assigning a high penalty as the action takes the current states to one that incurs collision.

  The major drawback of the policy iteration is the requirement to have the value function over all the states evaluated thoroughly before updatin (as is for a basic dynamic programming algorithm.) The largest test case I could assess is 2 robots in a 6x6 areana on Colab with the policy iteration algorithm. Larger state space simply crashes the runtime for the high space complexity. A better choice of algorithm should be a stochastic one instead of deterministic.

* Forth block: implements the value iteration algorithm, which beats the performance of policy iteration algorithm by 95% in the case of 2 robots in a 6x6 areana (2 seconds vs 40 seconds) in runtime. Since the 2-robot scenarios are the case where one can visually interpret the results, I chose to compare the two algorithms in this scenario. It finds the best value function at each sweep. Once the value function is stable, a policy is extracted greedily from the value function.

In the case of a big areana and a large number of robots (5 robots in 10 x 10), the space complexity increases exponetially with the number of robots to take up the entire RAM, which means the method is not scalable.

In the case of a small areana loading a large number of robots (5 robots in 5 x 5), collision dominates the behavior of robots. A smart idea may be programmatically excluding the states of collision to reduce the state space and the corresponding action space.
