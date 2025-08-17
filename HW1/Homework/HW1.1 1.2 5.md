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

# 5.1 证明 $$C(\tilde{\pi}^n) \leq A(T,n)$$，其中 $$A(t,n)$$ 满足：

$$
\begin{cases} 
A(0,n) = 0, \\ 
A(t,0) = 0, \\ 
A(t,n) = \alpha \varepsilon t + \alpha(1-\varepsilon)A(t-1,n) + (1-\alpha)A(t,n-1). 
\end{cases}
$$

**证明步骤**：  

1. **基例**：  
   - 当 $$t=0$$ 或 $$n=0$$ 时，$$C(\tilde{\pi}^n) = 0 \leq A(0,n)$$ 或 $$A(t,0)$$ 直接成立。  
   
2. **递推**：  
   - 策略 $$\tilde{\pi}^n$$ 的误差来源：  
     - 以概率 $$\alpha$$：当前步错误概率 $$\leq \varepsilon$$，后续 $$t-1$$ 步误差受 $$A(t-1,n)$$ 约束。  
     - 以概率 $$1-\alpha$$：误差受 $$A(t,n-1)$$ 约束。  
     
   - 因此：  
   
     $$C(\tilde{\pi}^n) \leq \alpha (\varepsilon t + (1-\varepsilon)A(t-1,n)) + (1-\alpha)A(t,n-1) = A(t,n).$$  

---



# 5.2 证明 $$C(\bar{\pi}^n) \leq Tn\alpha$$

**证明步骤**：  

1. 策略 $$\bar{\pi}^n = S^{X_n}(\hat{\pi}^n, \tilde{\pi}^{n-1})$$ 的误差分两部分：  
   - 前 $$X_n$$ 步误差 $$\leq X_n$$（因 $$\varepsilon \leq 1$$）。  
   - 剩余步误差 $$\leq C(\tilde{\pi}^{n-1}) \leq T(n-1)\alpha$$（归纳假设）。  

2. 由 $$X_n \sim \text{Geom}(1-\alpha)$$，有 $$\mathbb{E}[X_n] = \frac{\alpha}{1-\alpha} \leq \alpha$$（当 $$\alpha \leq 1/2$$）。  

3. 综上：  

   $$C(\bar{\pi}^n) \leq \mathbb{E}[X_n] + T(n-1)\alpha \leq \alpha + T(n-1)\alpha = Tn\alpha.$$  

---

# 5.3 当 $$n \geq T$$ 且 $$\alpha \leq 1/T$$ 时，证明  $$C(\pi^n) \leq C(\bar{\pi}^n) + Te^{\frac{n}{(1-\alpha)T}}.$$  

**证明步骤**：

1. $$\pi^n$$ 与 $$\bar{\pi}^n$$ 的差异仅发生在 $$X^* \leq T$$ 时（$$X^* = \sum_{i=1}^n X_i$$）。  

2. 由 Chernoff 界：  

   $$\Pr[X^* \leq T] \leq e^{-\frac{(1-\alpha)^2 n}{2\alpha}} \leq e^{\frac{n}{(1-\alpha)T}} \quad (\text{因 } \alpha \leq 1/T).$$  

3. 因此：  

   $$C(\pi^n) \leq C(\bar{\pi}^n) + T \cdot \Pr[X^* \leq T] \leq C(\bar{\pi}^n) + Te^{\frac{n}{(1-\alpha)T}}.$$  

---

# 5.4  选择 $$\alpha$$ 和 $$N$$ 使得 $$C(\pi^N) = O(T \log(1/\varepsilon))$$。  

**结论**：  
1. 设 $$\alpha = \varepsilon$$，$$N = \frac{T \log(1/\varepsilon)}{1-\alpha}$$。  
2. 代入 5.2 和 5.3 的结论：  
   $$
   \begin{aligned}
   C(\pi^N) &\leq TN\alpha + Te^{\frac{N}{(1-\alpha)T}} \\
   &= T \cdot \varepsilon \cdot \frac{T \log(1/\varepsilon)}{1-\alpha} + T \cdot \varepsilon \\
   &= O(T \log(1/\varepsilon)).
   \end{aligned}
   $$
   （因 $$e^{\frac{N}{(1-\alpha)T}} = e^{\log \varepsilon} = \varepsilon$$）

---

