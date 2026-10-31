# Appendix A: Anticipatory Feedback and the Von Foerster Singularity

*A mathematical formalization within Proteronomy*

**R.G. Guysayko** · ORCID: [0009-0007-8361-9683](https://orcid.org/0009-0007-8361-9683)

This appendix is part of *Proteronomy*, preprint v1.2. The PDF version is archived on Zenodo (all-versions DOI: [10.5281/zenodo.23445534](https://doi.org/10.5281/zenodo.23445534)).

---

## A.1 Purpose and scope

In 1960, von Foerster, Mora and Amiot fitted the history of world population to a curve that grows without bound and reaches infinity on Friday, 13 November 2026 [1]. This appendix uses that forecast as a case study. The question is: what must be added to a growth model so that a system's awareness of a projected end date can change the path leading to it? We propose one minimal answer, the **Proteronomic precedence kernel**, and state precisely what it does and does not guarantee. This is a toy model, not a demographic forecast: the sensitivity parameter $\alpha$ has not been estimated from data.

> **In plain words:** In the classical model, growth feeds on itself faster and faster until the curve shoots to infinity. Real populations notice where a curve is heading and change course (fewer births, new technology, new policy). We model that "noticing" as a dimmer switch $P$ that is fully on when the date is far away and slides smoothly to off as the date gets close.

---

## A.2 The classical model

Let $N(t)$ be the population at time $t$, with initial value $N_0 > 0$ at time $t_0$. The classical hyperbolic law is:

```math
\frac{dN}{dt} = k\,N^{p}, \qquad N(t_0) = N_0, \qquad k > 0,\ p > 1 \qquad \text{(1)}
```

Separating variables gives the solution:

```math
N(t) = \left[(p-1)\,k\,(t_c - t)\right]^{-\beta} = \frac{C}{(t_c - t)^{\beta}} \qquad \text{(2)}
```

where $\beta = 1/(p-1)$, $C = [(p-1)k]^{-\beta}$, and $t_c = t_0 + N_0^{1-p}/\big((p-1)k\big)$ is the finite-time singularity: $N(t) \to \infty$ as $t \to t_c^-$.

Throughout, $T = t_c - t_0$, and $t_c$ denotes the blow-up time of the classical model (1). The von Foerster fit, with exponent $\beta \approx 0.99$, corresponds to $p \approx 2$.

---

## A.3 The Proteronomic precedence kernel

Define the kernel:

```math
P(t, t_c) =
\begin{cases}
\exp\!\left(-\dfrac{\alpha}{t_c - t}\right), & t < t_c \\[2mm]
0, & t \ge t_c
\end{cases}
\qquad \text{(3)}
```

where $\alpha > 0$ is the anticipatory sensitivity, measured in units of time. Its properties are:

1. **Range and monotonicity:** $0 < P < 1$ for $t < t_c$, and $P$ is strictly decreasing in $t$.
2. **Smoothness:** $P \to 0$ as $t \to t_c^-$, and so do all of its derivatives, so the switch-off is perfectly smooth (no kink).
3. **Far-horizon behavior:** $P \ge 1 - \alpha/(t_c - t)$. When the horizon is far away, $t_c - t$ is much larger than $\alpha$, so $P \approx 1$ and the classical model is recovered.
4. **Half-way point:** $P = \tfrac{1}{2}$ when $t_c - t = \alpha/\ln 2 \approx 1.44\,\alpha$. So a larger $\alpha$ means the system starts reacting earlier.

---

## A.4 The modified equation and its guarantees

Including the kernel and a separate adaptation term $\Omega$, the rate equation becomes:

```math
\frac{dN}{dt} = k\,N^{p}\,P(t, t_c) - \Omega(N, t), \qquad N(t_0) = N_0 \qquad \text{(4)}
```

Here $\Omega(N, t) \ge 0$ is a continuous adaptation function for all other responses (cultural shifts, technological efficiency, policy changes). We consider times while $N$ remains positive.

### Proposition 1 ($\Omega = 0$)

Let $I_\infty$ be the total area under the kernel:

```math
I_\infty = \int_{t_0}^{t_c} P(s, t_c)\,ds = T\,e^{-\alpha/T} - \alpha\,E_1\!\left(\frac{\alpha}{T}\right)
```

where $E_1$ is the exponential integral. Then:

```math
N(t)^{1-p} = N_0^{1-p} - (p-1)\,k \int_{t_0}^{t} P(s, t_c)\,ds \qquad \text{(5)}
```

and $N(t)$ stays finite on $[t_0, t_c)$, with a finite limit as $t \to t_c^-$, **if and only if**:

```math
(p-1)\,k\,I_\infty < N_0^{1-p} \qquad \text{(6)}
```

*Proof.* Separate variables: $N^{-p}\,dN = k\,P\,dt$, and integrate to get (5). $N$ blows up exactly when the right-hand side of (5) reaches zero. That side decreases with $t$ and has the finite value $N_0^{1-p} - (p-1)\,k\,I_\infty$ at $t_c$, so it stays positive up to and including $t_c$ exactly when (6) holds. The closed form of $I_\infty$ follows by substituting $u = t_c - s$ and integrating by parts. Q.E.D.

### Corollary 1 (the Proteronomic result)

Since $t_c$ is the classical blow-up time, $(p-1)\,k\,T\,N_0^{p-1} = 1$, so condition (6) is equivalent to $I_\infty < T$. Because $P < 1$, we always have $I_\infty = T - \int_{t_0}^{t_c} (1-P)\,ds < T$. Hence **for every $\alpha > 0$ the singularity at $t_c$ is prevented**, and the population approaches the finite value:

```math
N_c = \left[(p-1)\,k\,(T - I_\infty)\right]^{-\beta} \qquad \text{(7)}
```

Two limits confirm the formula:

- As $\alpha \to 0$, $I_\infty \to T$ and $N_c \to \infty$: the classical singularity is recovered.
- As $\alpha \to \infty$, $I_\infty \to 0$ and $N_c \to N_0$: growth is fully suppressed.

A numerical integration of (4) with $\Omega = 0$, $p = 2$, $\alpha = 0.3$ agrees with (7) to nine digits.

### Corollary 2 (adaptation)

With $\Omega \ge 0$, equation (4) gives $dN/dt \le k\,N^{p}\,P$, so by the standard comparison principle $N(t)$ never exceeds the $\Omega = 0$ solution. Adaptation can therefore only lower the ceiling: $N(t) \le N_c$ on $[t_0, t_c)$.

> **What happens after $t_c$:** For $t \ge t_c$ the kernel is zero and (4) reduces to $dN/dt = -\Omega$: the growth term is switched off and the later path is set entirely by $\Omega$. So $N_c$ is a finite ceiling at the end of the growth phase, *not* a logistic-type carrying capacity, and this appendix makes no claim about long-run equilibrium.

---

## A.5 Axiom of Anticipatory Precedence (conditional form)

> **Axiom.** If an open, complex, information-processing system can form a representation of a projected boundary $t_c$ and act on it, then its transition operator depends on $t_c$ through a precedence factor $P(t, t_c)$ for all $t < t_c$. Consequently, a forecast of $t_c$ that assumes the transition operator is independent of $t_c$ is not self-consistent for such a system.

**Scope.** The axiom applies only to systems that detect and respond to the projection. It says nothing about systems that cannot or do not respond (for example, a population never exposed to the forecast, or one that ignores it). Whether a real system meets the condition is an empirical question.

---

## A.6 Limitations and relation to prior work

- **The guarantee is easy to obtain.** Corollary 1 holds for any damping factor with $0 \le P \le 1$ that is below 1 over some stretch of time. The exponential form is chosen for smoothness, not necessity. The scientific content therefore lies in justifying a particular $P$ and measuring $\alpha$, which this appendix does not do.
- **$t_c$ is taken as given.** In a real system the projected date itself moves as the system responds. Treating this as a fixed-point problem is left to future work.
- **No empirical validation.** World population growth has already slowed relative to the hyperbolic curve since the 1960s, so the model should be tested against data rather than assumed.
- **Related ideas.** Anticipatory systems [2]; self-fulfilling and self-defeating predictions [3, 4]; the Lucas critique [5]; finite-time singularities in complex systems [6]; hyperbolic population models [7]. What is added here is an explicit feedback factor from the projected boundary inside a hyperbolic growth law, with exact conditions for when blow-up is avoided.

---

## References

1. von Foerster, H., Mora, P. M., & Amiot, L. W. (1960). Doomsday: Friday, 13 November, A.D. 2026. *Science*, 132(3436), 1291–1295.
2. Rosen, R. (1985). *Anticipatory Systems*. Pergamon Press.
3. Merton, R. K. (1948). The self-fulfilling prophecy. *The Antioch Review*, 8(2), 193–210.
4. Grunberg, E., & Modigliani, F. (1954). The predictability of social events. *Journal of Political Economy*, 62(6), 465–478.
5. Lucas, R. E. (1976). Econometric policy evaluation: a critique. *Carnegie-Rochester Conference Series on Public Policy*, 1, 19–46.
6. Sornette, D. (2003). *Why Stock Markets Crash*. Princeton University Press.
7. Kapitza, S. P. (1996). The phenomenological theory of world population growth. *Physics-Uspekhi*, 39(1), 57–71.
