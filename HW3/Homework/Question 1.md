## 1.1

NO（引入高估偏差）

## 1.2

YES YES YES

NO YES YES（数据来自其他策略，对Q有偏）

NO YES YES（在线学习的策略函数是贪心的）

NO NO NO（自举误差累积）

YES NO NO（蒙特卡洛回报是无偏的，收敛到行为策略而非Q*）

YES NO NO

## 1.3

Highest: N → $∞$（蒙特卡洛回报的方差随步数增大而增大）

Lowest: N = 1（单步自举方差最小）

## 1.4

BC

## 1.5

**Modified target update with importance sampling:**

$$
y_{j,t} \leftarrow \sum_{t'=t}^{t+N-1} \left( \gamma^{t'-t} \rho_{j,t'} r_{j,t'} \right) + \gamma^N \rho_{j,t+N} \max_{a_{j,t+N}} Q_{\phi_k}(s_{j,t+N}, a_{j,t+N})
$$

**Importance weights definition:**
$$
\rho_{j,t'} = \frac{\pi(a_{j,t'} \mid s_{j,t'})}{\pi'(a_{j,t'} \mid s_{j,t'})}
$$

**When to modify equation (2):**
- For \(N=1\):  NO
  
- For (N → ∞)：YES
  
  





