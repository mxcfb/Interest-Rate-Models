# Interest Rate Models

## Basics

### Spot Rates and Forward Rates

Suppose that the zero coupon bond price observed at time t is $P(t,T) \in \mathcal{F}_{t}$. The forward zero coupon bond price observed at time t is $P(t,S,T) = \frac{P(t,T)}{P(t,S)} \in \mathcal{F}_{t}$.

Simply-compounded spot rate $F(t,T)$

$$
\begin{aligned}
& P(t,T) (1+F (t,T) \tau(t,T)) = 1 \\
\iff & F(t,T) = \frac{1}{\tau(t,T)} \left( \frac{1}{P(t,T)}-1 \right).
\end{aligned}
$$

Simply-compounded forward rate $F(t;S,T)$

$$
\begin{aligned}
& P(t,S,T) (1+F(t,S,T) \tau(S,T) = 1 \\
\iff & F(t,S,T) = \frac{1}{\tau(t,T)} \left( \frac{P(t,S)}{P(t,T)}-1 \right).
\end{aligned}
$$

Continuously-compounded spot rate $R(t,T)$

$$
\begin{aligned}
& P(t,T) e^{R(t,T) \tau(t,T)} = 1 \\
\iff & R(t,T) = -\frac{\ln P(t,T)}{\tau(t,T)}.
\end{aligned}
$$

Continuously-compounded forward rate $R(t;S,T)$

$$
\begin{aligned}
& P(t,S,T) e^{R(t,S,T) \tau(S,T)} = 1 \\
\iff & R(t,S,T) = \frac{1}{\tau(t,T)} \left( \ln P(t,S) - \ln P(t,T) \right).
\end{aligned}
$$

Annually-compounded spot rate $Y(t,T)$

$$
\begin{aligned}
& P(t,T)(1+Y(t,T))^{\tau(t,T)} = 1 \\
\iff & Y(t,T) = \frac{1}{[P(t,T)]^{1 / \tau(t,T)}}-1.
\end{aligned}
$$

k-times-per-year compounded spot rate $Y^k(t,T)$

$$
\begin{aligned}
& P(t,T)\left(1+\frac{Y^{k}(t,T)}{k}\right)^{k \tau(t,T)} = 1 \\
\iff & Y^{k}(t,T) = \frac{k}{[P(t,T)]^{1 /(k \tau(t,T))}-k}.
\end{aligned}
$$

### Instantaneous Spot Rates and Instantaneous Forward Rates

Instantaneous spot rate (short rate) $r(t)$

$$
\begin{aligned}
r(t) &=\lim_{\Delta t \rightarrow 0^{+}} F(t,t+\Delta t) =\lim_{\Delta t \rightarrow 0^{+}} R(t,t+\Delta t) =\lim_{\Delta t \rightarrow 0^{+}} Y(t,t+\Delta t) =\lim_{\Delta t \rightarrow 0^{+}} Y^{k}(t,t+\Delta t) \text { for each } k \\
&=-\left.\frac{1}{P(t,T)} \frac{\partial P(t,T)}{\partial T}\right|_{T=t} \\
&=-\left.\frac{\partial P(t,T)}{\partial T}\right|_{T=t}.
\end{aligned}
$$

Instantaneous forward rate $f(t,T)$

$$
\begin{aligned}
f(t,T) &=\lim_{\Delta t \rightarrow 0^{+}} F(t;T,T+\Delta t) =\lim_{\Delta t \rightarrow 0^{+}} R(t;T,T+\Delta t) = \dots \\
&=-\frac{1}{P(t,T)} \frac{\partial P(t,T)}{\partial T} \\
&=-\frac{\partial \ln P(t,T)}{\partial T}.
\end{aligned}
$$

$r(t) = f(t,t)$
$P(t,T) = \exp \left( - \int_t^T f(t,s) \,ds \right)$
$P(t,S,T) = \exp \left( - \int_S^T f(t,s) \,ds \right)$
$F(t,S,T) = \frac{1}{\tau(S,T)} \left( \exp \left( \int_S^T f(t,s) \,ds \right)-1 \right)$
