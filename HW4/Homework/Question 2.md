## 问题 2.1 解答

**证明 Alternative Simulation Lemma：对于任何策略 $\pi$，有**
Qπ−Q^π=γ(I−γPπ)−1(P−P^)V^π.*Q**π*−*Q*​*π*=*γ*(*I*−*γ**P**π*)−1(*P*−*P*)*V**π*.

**证明过程：**

根据 $Q^{\pi}$ 和 $\widehat{Q}^{\pi}$ 的 Bellman 方程，我们有：
Qπ(s,a)=r(s,a)+γ∑s′P(s′∣s,a)Vπ(s′)*Q**π*(*s*,*a*)=*r*(*s*,*a*)+*γ*∑*s*′​*P*(*s*′∣*s*,*a*)*V**π*(*s*′)
Q^π(s,a)=r(s,a)+γ∑s′P^(s′∣s,a)V^π(s′)*Q*​*π*(*s*,*a*)=*r*(*s*,*a*)+*γ*∑*s*′​*P*(*s*′∣*s*,*a*)*V**π*(*s*′)

将两个等式相减：
Qπ(s,a)−Q^π(s,a)=γ∑s′[P(s′∣s,a)Vπ(s′)−P^(s′∣s,a)V^π(s′)]*Q**π*(*s*,*a*)−*Q*​*π*(*s*,*a*)=*γ*∑*s*′​[*P*(*s*′∣*s*,*a*)*V**π*(*s*′)−*P*(*s*′∣*s*,*a*)*V**π*(*s*′)]

我们通过加减一项 $\gamma \sum_{s'} P(s'|s, a) \widehat{V}^{\pi}(s')$ 来拆分右边的项：

Qπ(s,a)−Q^π(s,a)=γ∑s′[P(s′∣s,a)Vπ(s′)−P(s′∣s,a)V^π(s′)+P(s′∣s,a)V^π(s′)−P^(s′∣s,a)V^π(s′)]=γ∑s′P(s′∣s,a)[Vπ(s′)−V^π(s′)]+γ∑s′[P(s′∣s,a)−P^(s′∣s,a)]V^π(s′)*Q**π*(*s*,*a*)−*Q**π*(*s*,*a*)=*γ**s*′∑[*P*(*s*′∣*s*,*a*)*V**π*(*s*′)−*P*(*s*′∣*s*,*a*)*V**π*(*s*′)+*P*(*s*′∣*s*,*a*)*V**π*(*s*′)−*P*(*s*′∣*s*,*a*)*V**π*(*s*′)]=*γ**s*′∑*P*(*s*′∣*s*,*a*)[*V**π*(*s*′)−*V**π*(*s*′)]+*γ**s*′∑[*P*(*s*′∣*s*,*a*)−*P*(*s*′∣*s*,*a*)]*V**π*(*s*′)

现在，我们用向量/矩阵形式表示整个方程。定义：

- $\mathbf{Q}^{\pi}$, $\mathbf{\widehat{Q}}^{\pi}$: $|\mathcal{S}||\mathcal{A}|$ 维向量
- $\mathbf{V}^{\pi}$, $\mathbf{\widehat{V}}^{\pi}$: $|\mathcal{S}|$ 维向量
- $P$, $\widehat{P}$: $|\mathcal{S}||\mathcal{A}| \times |\mathcal{S}|$ 维矩阵
- $P^{\pi}$: $|\mathcal{S}| \times |\mathcal{S}|$ 维矩阵，其中 $P^{\pi}(s'|s) = \sum_a \pi(a|s) P(s'|s, a)$

上面的逐点方程可以写成矩阵形式：

Qπ−Q^π=γP(Vπ−V^π)+γ(P−P^)V^π**Q***π*−**Q***π*=*γ**P*(**V***π*−**V***π*)+*γ*(*P*−*P*)**V***π*

根据价值函数和状态-动作价值函数的关系 $\mathbf{V}^{\pi} = \mathbb{E}_{a\sim\pi}[\mathbf{Q}^{\pi}]$，可以表示为 $\mathbf{V}^{\pi} = \Pi \mathbf{Q}^{\pi}$，其中 $\Pi$ 是适当的投影矩阵。将其代入上式：

Qπ−Q^π=γPΠ(Qπ−Q^π)+γ(P−P^)V^π**Q***π*−**Q***π*=*γ**P*Π(**Q***π*−**Q***π*)+*γ*(*P*−*P*)**V***π*

将包含 $(\mathbf{Q}^{\pi} - \mathbf{\widehat{Q}}^{\pi})$ 的项移到一边：

(Qπ−Q^π)−γPΠ(Qπ−Q^π)=γ(P−P^)V^π(**Q***π*−**Q***π*)−*γ**P*Π(**Q***π*−**Q***π*)=*γ*(*P*−*P*)**V***π*(I−γPΠ)(Qπ−Q^π)=γ(P−P^)V^π(*I*−*γ**P*Π)(**Q***π*−**Q***π*)=*γ*(*P*−*P*)**V***π*

注意到 $P \Pi = P^{\pi}$（根据 $P^{\pi}$ 的定义）。因此：

(I−γPπ)(Qπ−Q^π)=γ(P−P^)V^π(*I*−*γ**P**π*)(**Q***π*−**Q***π*)=*γ*(*P*−*P*)**V***π*

由于 $I - \gamma P^{\pi}$ 是可逆的（因为 $\gamma \in (0,1)$ 且 $P^{\pi}$ 是概率转移矩阵，其谱半径不超过1），我们在左边乘上它的逆：

Qπ−Q^π=γ(I−γPπ)−1(P−P^)V^π**Q***π*−**Q***π*=*γ*(*I*−*γ**P**π*)−1(*P*−*P*)**V***π*

这正是我们要证明的引理。 $\square$

------

## 问题 2.2 解答

**分析：** 我们需要判断哪些选项正确地使用了 Alternative Simulation Lemma 和 Concentration Inequalities (如 Hoeffding) 来界定 $||(P-\widehat{P})\widehat{V}^{\pi}||_{\infty}$ 或类似项。

关键点在于 Hint 2 和 Hint 3：Hoeffding 不等式要求随机变量是**独立**的且有**界**。当我们试图界定 $(P-\widehat{P})\widehat{V}^{\pi}$ 时，向量 $\widehat{V}^{\pi}$ **依赖于**我们用于构建 $\widehat{P}$ 的数据（因为 $\widehat{V}^{\pi}$ 是在模型 $\widehat{M}$ 中计算得到的），这违反了独立性假设。$\widehat{V}^{*}$ 也有同样的问题。

**判断结果：**

1. **错误。** 第一个不等式 $||(P-\widehat{P}){\widehat{V}}^{\pi}||*{\infty}\leq \max*{s,a}||P(\cdot\mid s,a)-\widehat{P}(\cdot\mid s,a)||*{1}||{\widehat{V}}^{\pi}||*{\infty}$ 是成立的（由 Holder 不等式）。然而，第二个不等式试图用 Hoeffding 和并界来界定 $||P(\cdot\mid s,a)-\widehat{P}(\cdot\mid s,a)||*1$。虽然 $\widehat{P}$ 的每个条目确实可以通过 Hoeffding 来界定，但将其组合成 $L_1$ 范数并乘以 $||{\widehat{V}}^{\pi}||*{\infty}$ 后，最终的界 $\frac{1}{1-\gamma}\sqrt{\frac{4|S|\log(|S||\mathcal{A}|/\delta)}{N}}$ 看起来是标准的形式。**但是，最主要的问题是 $\widehat{V}^{\pi}$ 依赖于数据 $\mathcal{D}$（用于构建 $\widehat{P}$），这使得在应用 Concentration Inequality 时，$X_i = \mathbb{I}_{s'}\cdot \widehat{V}^{\pi}$ 不再是独立的（因为 $\widehat{V}^{\pi}$ 是所有 $(s,a)$ 对数据的函数），因此 Hoeffding 不等式的前提条件不满足。** 此外，$\sqrt{|S|}$ 项也暗示了可能是对 $L_1$ 范数应用了并界，这通常会产生这样的因子。
2. **错误。** 这个选项直接声称对 $||(P-\widehat{P}){\widehat{V}}^{\pi}||_{\infty}$ 应用 Hoeffding 和并界得到了一个不依赖于 $|S|$ 的界。然而，和选项1一样，$\widehat{V}^{\pi}$ 依赖于数据 $\mathcal{D}$，违反了 Hoeffding 不等式要求的独立性假设。此外，要获得无穷范数上的保证，需要对所有 $|\mathcal{S}||\mathcal{A}|$ 个 $(s,a)$ 对应用并界，这通常会引入一个 $\log(|\mathcal{S}||\mathcal{A}|)$ 的因子，但不会引入 $|S|$ inside the square root。**核心错误在于忽略了 $\widehat{V}^{\pi}$ 对数据的依赖性。**
3. **正确。** 这个选项界定的是 $||(P-\widehat{P})V^{*}||_{\infty}$。这里的关键是 $V^{*}$ 是**真实 MDP $M$ 的最优价值函数**。$V^{*}$ **不依赖于**我们用于构建 $\widehat{P}$ 的采样数据 $\mathcal{D}$。因此，对于每个固定的 $(s,a)$ 对，随机变量 $X_i = \mathbb{I}_{s'}\cdot V^{*}$ (如 Hint 3 所定义) 是独立且有界的（因为 $0 \leq V^{*}(s') \leq \frac{1}{1-\gamma}$）。我们可以对每个 $(s,a)$ 应用 Hoeffding 不等式，然后使用并界覆盖所有的 $(s,a)$ 对。最终得到的界 $\frac{1}{1-\gamma}\sqrt{\frac{2\log(2|S||\mathcal{A}|/\delta)}{N}}$ 在形式上是正确的（常数因子可能因不等式版本而异）。
4. **错误。** 这个选项界定的是 $||(P-\widehat{P}){\widehat{V}}^{*}||_{\infty}$。这里的问题是 ${\widehat{V}}^{*}$ 是**基于模型 $\widehat{M}$ 的最优价值函数**。${\widehat{V}}^{*}$ 的计算**依赖于**模型 $\widehat{P}$，而 $\widehat{P}$ 又直接依赖于我们采集的数据 $\mathcal{D}$。因此，${\widehat{V}}^{*}$ 依赖于 $\mathcal{D}$。这使得随机变量 $X_i = \mathbb{I}_{s'}\cdot {\widehat{V}}^{*}$ 不再是独立的（因为 ${\widehat{V}}^{*}$ 是所有 $(s,a)$ 对数据的函数），因此不能直接应用 Hoeffding 不等式。

**结论：唯一正确的陈述是选项 3。**