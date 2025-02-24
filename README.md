# Monte Carlo Policy Evaluation & SARSA for Cliff Walking

## Introduction
This project explores two key Reinforcement Learning (RL) techniques: **Monte Carlo (MC) Policy Evaluation for Blackjack** and **SARSA (State-Action-Reward-State-Action) for Cliff Walking** 
to understand how agents can learn optimal strategies through experience. 
The primary objective is to analyze how these methods approximate the value function and improve decision-making in the game. 
The results provide insights into the effectiveness of episodic learning in MC methods and the impact of on-policy learning in SARSA.

## 1. Monte Carlo Policy Evaluation for Blackjack
Monte Carlo methods estimate the value function by averaging returns from complete episodes.
### Environment Setup
I have used OpenAI Gym's `Blackjack-v1` environment, where the agent learns the expected reward (value function) for each state under a fixed policy.

### Implementation Steps
1. **Initialize** value function `V(s)` and visit counts.
2. **Generate complete episodes** Each episode starts from an initial state and follows a given policy until reaching a terminal state.
3. **Compute returns** The return for each state-action pair is computed based on the reward obtained at the end of the episode.
4. **Update the value function** The average of these returns is used to refine the value function.
5. **Repeat for multiple episodes** until convergence.

### Results
The MC evaluation provided a clear understanding of how different policies affect the expected return. The heatmap visualization of the learned state-value function showed that:
- The policy effectively differentiates between strong and weak positions in the game.
- The value function assigns higher values to states where the player holds a sum close to 21.
- States with lower total sums or higher chances of busting have lower expected returns.
- Since MC methods require complete episodes, early convergence depends on how frequently states are visited.

- **Plot 1:** Shows the estimated value function for different player hands.
  ![heatmap](https://github.com/user-attachments/assets/c12af2b6-eeb1-45ea-9477-4d14a95a1ec6)

- **Plot 2:** Displays the improvement of the value function over episodes.
![exc 1 plot](https://github.com/user-attachments/assets/c2b3aa9a-3af6-42ae-86e4-0797c6cf756f)

## 2. SARSA for Cliff Walking
SARSA is an on-policy Temporal Difference (TD) learning algorithm that updates the Q-value of a state-action pair based on the next state and action taken.
### Environment Setup
I have used OpenAI Gym's `CliffWalking-v0` environment, a **4x12 grid** where the agent must navigate from the start to the goal while avoiding the cliff.

### Implementation Steps
1. **Initialize** Q-table with arbitrary values.
2. **Select actions** using an **epsilon-greedy policy**.
3. **Execute actions** and observe rewards and next states.
4. **Update Q-values** using the SARSA update rule:
![update rule](https://github.com/user-attachments/assets/002415d1-5c11-4175-96af-041789ec90a2)
5. **Repeat for multiple episodes**, adjusting the policy over time.

### Results
The SARSA-based policy improved gradually over multiple iterations. Key observations from the learned policy visualization include:
- The Q-values became more refined, favoring actions that maximize long-term rewards while balancing exploration and exploitation.
- Unlike MC methods, SARSA updated values at every step rather than waiting for the end of the episode, leading to faster adaptation.
- The policy showed more conservative behavior in certain states, preferring to stick rather than hit when the risk of busting was high.
- The overall strategy closely resembled optimal Blackjack play, suggesting that the SARSA method successfully learned an effective policy over time.
- **Plot 1:** Shows cumulative reward over episodes, indicating learning progress.
  ![sarsa learnng progress](https://github.com/user-attachments/assets/cb6e1c51-cfc5-499a-b440-c314ee12bccf)

- **Plot 2:** Displays the learned policy as directional arrows for each state.
  ![learned polcy](https://github.com/user-attachments/assets/8a455220-f224-47e3-8a09-f8924e43cc4a)

## Key Learning Points of these Implementations

### Importance of Episodic Tasks in MC Methods
Monte Carlo methods are particularly effective for **episodic tasks**, where interactions naturally terminate after a finite number of steps. 
This makes them suitable for problems like **Blackjack**, where each game is a distinct episode.

### How MC Methods Rely on Complete Episodes to Compute Returns
Unlike Temporal Difference (TD) learning, MC methods update value estimates only at the end of an episode by computing the total return. 
This approach provides an unbiased estimate of the value function, though it may suffer from high variance.

### Impact of the Policy on the Value Function
In both **MC Policy Evaluation** and **SARSA**, the choice of policy significantly impacts learning. In MC methods, an **exploring-start policy** ensures all state-action pairs are visited. 
In SARSA, an **epsilon-greedy policy** balances exploration and exploitation, shaping the learned value function and policy.

## Conclusion
This project illustrates two fundamental RL techniques:
- **Monte Carlo Policy Evaluation** computes state values from complete episodes.
- **SARSA** learns an optimal policy using TD learning with on-policy updates.

Each method has its strengths: **MC is unbiased but high-variance**, while **SARSA provides stable learning but may converge to suboptimal policies**. 
Understanding these methods helps in tackling complex RL problems efficiently.
