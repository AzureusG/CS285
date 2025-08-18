# 8.1 应用策略梯度

### (a) 计算策略梯度

在无限视野MDP中，期望回报为：
$$ J(\theta) = \mathbb{E}_{\tau \sim \pi_\theta} [R(\tau)] = \sum_{k=1}^{\infty} k \cdot \theta^{k-1}(1-\theta) $$

策略梯度为：
$$ \nabla_\theta J(\theta) = \nabla_\theta \left( \sum_{k=1}^{\infty} k \theta^{k-1}(1-\theta) \right) $$
$$ = \sum_{k=1}^{\infty} k \left[ (k-1)\theta^{k-2}(1-\theta) - \theta^{k-1} \right] $$
$$ = \sum_{k=1}^{\infty} k(k-1)\theta^{k-2}(1-\theta) - \sum_{k=1}^{\infty} k \theta^{k-1} $$

使用提示中的求和方法：
$$ \sum_{k=1}^{\infty} k \theta^{k-1} = \frac{1}{(1-\theta)^2} $$
$$ \sum_{k=1}^{\infty} k(k-1) \theta^{k-2} = \frac{2}{(1-\theta)^3} $$

因此：
$$ \nabla_\theta J(\theta) = \frac{2(1-\theta)}{(1-\theta)^3} - \frac{1}{(1-\theta)^2} = \frac{1}{(1-\theta)^2} $$

### (b) 验证梯度

直接计算期望回报：
$$ J(\theta) = \frac{1}{1-\theta} $$
其梯度为：
$$ \nabla_\theta J(\theta) = \frac{1}{(1-\theta)^2} $$

与(a)部分结果一致，验证了策略梯度的正确性。

# 8.2 策略梯度方差

### 方差计算

策略梯度的方差为：
$$ \text{Var}[\nabla_\theta \log \pi_\theta(\tau) R(\tau)] = \mathbb{E}[(\nabla_\theta \log \pi_\theta(\tau) R(\tau))^2] - (\mathbb{E}[\nabla_\theta \log \pi_\theta(\tau) R(\tau)])^2 $$

经过计算可得：
$$ \text{Var} = \frac{1+\theta}{(1-\theta)^3} - \frac{1}{(1-\theta)^4} = \frac{\theta(1-\theta)}{(1-\theta)^4} = \frac{\theta}{(1-\theta)^3} $$

### 极值分析

- 当$\theta \to 0$时，方差$\to 0$
- 当$\theta \to 1$时，方差$\to \infty$
- 方差在$\theta \in (0,1)$单调递增

因此：
- 最小方差在$\theta=0$取得（方差=0）
- 最大方差在$\theta \to 1$时趋向无穷大

# 8.3 奖励累计

### (a) 修正策略梯度

奖励累计策略梯度为：
$$ \nabla_\theta J(\theta) = \mathbb{E} \left[ \sum_{t=0}^{\infty} \nabla_\theta \log \pi_\theta(a_t|s_t) \left( \sum_{t'=t}^{\infty} r_{t'} \right) \right] $$

在本题中，由于奖励只在终止时给出，且与动作选择无关，因此奖励累计策略梯度仍为无偏估计。

### (b) 方差比较

奖励累计的方差表达式为：
$$ \text{Var}_{RTG} = \frac{\theta}{(1-\theta)^2} $$

与原始方差比较：
- 原始方差：$\frac{\theta}{(1-\theta)^3}$
- RTG方差：$\frac{\theta}{(1-\theta)^2}$

显然RTG方差更小，因为分母次数降低。

# 8.4 重要性采样

### (a) 重要性采样策略梯度

策略梯度为：
$$ \nabla_\theta J(\theta) = \mathbb{E}_{\tau \sim \pi_{\theta'}} \left[ \prod_{t=0}^{H-1} \frac{\pi_\theta(a_t|s_t)}{\pi_{\theta'}(a_t|s_t)} \nabla_\theta \log \pi_\theta(\tau) R(\tau) \right] $$

### (b) 方差分析

重要性权重为：
$$ w = \prod_{t=0}^{H-1} \frac{\pi_\theta(a_t|s_t)}{\pi_{\theta'}(a_t|s_t)} = \left( \frac{\theta}{\theta'} \right)^{H-1} \left( \frac{1-\theta}{1-\theta'} \right) $$

方差随H指数增长：
$$ \text{Var} \propto \left( \frac{\theta^2}{\theta'^2} \right)^H $$

当H增大时：
- 若$\theta < \theta'$，方差$\to 0$
- 若$\theta > \theta'$，方差$\to \infty$
- 若$\theta = \theta'$，方差保持不变