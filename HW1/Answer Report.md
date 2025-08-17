# 1.1 证明 $\sum_{s_{t}}|p_{\pi_{\theta}}(s_{t})-p_{\pi^{*}}(s_{t})|\leq 2T\varepsilon$

**证明思路：**

1. 利用状态分布差异与策略差异的关系
2. 通过联合界（union bound）累加时间步差异

**证明步骤：**
1. 定义策略差异：
   $$\mathbb{E}_{p_{\pi^{*}}(s_t)}[\pi_{\theta}(a \neq \pi^{*}(s_t) | s_t)] \leq \varepsilon$$

2. 状态分布差异上界：
   $$|p_{\pi_{\theta}}(s_t) - p_{\pi^{*}}(s_t)| \leq \sum_{i=1}^{t} \mathbb{E}_{p_{\pi^{*}}(s_i)}[\pi_{\theta}(a \neq \pi^{*}(s_i) | s_i)] \leq t \varepsilon$$

3. 对所有状态和时间步求和：
   $$\sum_{t=1}^{T} \sum_{s_t} |p_{\pi_{\theta}}(s_t) - p_{\pi^{*}}(s_t)| \leq 2T\varepsilon$$

**结论：**
$$\sum_{s_t} |p_{\pi_{\theta}}(s_t) - p_{\pi^{*}}(s_t)| \leq 2T\varepsilon$$

---

# 1.2(a) 证明 $J(\pi^{*}) - J(\pi_{\theta}) = O(T\varepsilon)$（仅最后状态有奖励）

**假设条件：**
- $r(s_t) = 0$ 对所有 $t < T$
- $|r(s_T)| \leq R_{\max}$

**证明步骤：**
1. 回报表达式：
   $$J(\pi) = \mathbb{E}_{p_{\pi}(s_T)}[r(s_T)]$$

2. 性能差异：
   $$|J(\pi^{*}) - J(\pi_{\theta})| = |\mathbb{E}_{p_{\pi^{*}}(s_T)}[r(s_T)] - \mathbb{E}_{p_{\pi_{\theta}}(s_T)}[r(s_T)]|$$

3. 应用1.1结论：
   $$\leq R_{\max} \cdot 2T\varepsilon$$

**结论：**
$$J(\pi^{*}) - J(\pi_{\theta}) = O(T\varepsilon)$$

---

# 1.2(b) 证明 $J(\pi^{*}) - J(\pi_{\theta}) = O(T^{2}\varepsilon)$（任意奖励）

**假设条件：**
- $\forall t, |r(s_t)| \leq R_{\max}$

**证明步骤：**

1. 回报展开：
   $$J(\pi) = \sum_{t=1}^{T} \mathbb{E}_{p_{\pi}(s_t)}[r(s_t)]$$

2. 差异分解：
   $$|J(\pi^{*}) - J(\pi_{\theta})| \leq \sum_{t=1}^{T} |\mathbb{E}_{p_{\pi^{*}}(s_t)}[r(s_t)] - \mathbb{E}_{p_{\pi_{\theta}}(s_t)}[r(s_t)]|$$

3. 逐项上界：
   $$\leq \sum_{t=1}^{T} R_{\max} \cdot 2t\varepsilon \leq 2R_{\max}\varepsilon \frac{T(T+1)}{2}$$

**结论：**
$$J(\pi^{*}) - J(\pi_{\theta}) = O(T^{2}\varepsilon)$$

---

**注：**
1. 所有证明基于策略差异的期望上界$\varepsilon$
2. $O(\cdot)$记号隐含了$R_{\max}$常数项
3. 1.2(b)的平方项来源于误差随时间的累积效应