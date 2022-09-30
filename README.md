# Interest Rate Models

See [Interest Rate Models](Interest%20Rate%20Models.ipynb).

## Basics

### Spot Rates and Forward Rates

Suppose that the zero coupon bond price observed at time t is $P(t,T) \in \mathcal{F}_{t}$. The forward zero coupon bond price observed at time t is $P(t,S,T) = \frac{P(t,T)}{P(t,S)} \in \mathcal{F}_{t}$.

Simply-compounded spot rate $F(t,T)$

$$
\begin{aligned}
& P(t,T) \left( 1+F (t,T) \tau(t,T) \right) = 1 \\
\iff & F(t,T) = \frac{1}{\tau(t,T)} \left( \frac{1}{P(t,T)}-1 \right).
\end{aligned}
$$

Simply-compounded forward rate $F(t;S,T)$

$$
\begin{aligned}
& P(t,S,T) \left( 1+F(t,S,T) \tau(S,T) \right) = 1 \\
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
\iff & Y^{k}(t,T) = \frac{k}{[P(t,T)]^{1 /(k \tau(t,T))}}-k.
\end{aligned}
$$

### Instantaneous Spot Rates and Instantaneous Forward Rates

Instantaneous spot rate (short rate) $r(t)$

$$
\begin{aligned}
r(t) &=\lim_{\Delta t \rightarrow 0^{+}} F(t,t+\Delta t) =\lim_{\Delta t \rightarrow 0^{+}} R(t,t+\Delta t) = \dots \\
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

#### Comments

Suppose $t = 0$ is today.

**LIBOR rates**: LIBOR (spot) rate $L(t,T)$; LIBOR forward rate $L(t,S,T)$; instantaneous $T-S$ LIBOR forward rate $l(t,s)$.
The instantaneous LIBOR forward rate $l(t,s)$ is specific to the tenor $T-S$ of LIBOR as they carry different credits.

**OIS rates**: discount factor $P(t,T) \rightarrow$ OIS (spot) rate $F(t,T)$; forward discount factor $P(t,S,T) \rightarrow$ OIS forward rate $F(t,S,T)$; instantaneous (overnight) OIS forward rate $f(t,s)$.

LIBOR rates are not regarded risk free, but the participating banks have high credit ratings.

Until 2008, it was common practice to use **LIBOR** as both the **discount rate**, i.e. the interest rate used for calculating the discount factors, as well as the **index rate**, i.e. the rate used as the forward rate.

In the wake of the 2008 credit crunch, LIBOR’s credibility as a funding rate was put to question. As a result, OIS rates became increasingly important as benchmark funding rates.

Since **OIS** is a better indicator of the costs of funding, it is used for **discounting**, while **LIBOR** is the **index rate**.

#### Comments

LIBOR rates (prior to December 31, 2021) was calculated (from the quotations provided by the participating banks determined by the ICE Benchmark Administration) for five currencies (USD, GBP, EUR, CHF and JPY) and for seven tenors in respect of each currency (Overnight/1 Day, 1 Week, 1 Month, 2 Months, 3 Months, 6 Months and 12 Months) on each London business day. [Website](https://www.theice.com/iba/libor)

LIBOR based instruments: Eurodollar futures (LIBOR futures, i.e. futures on the 3 Month LIBOR rate), forward rate agreements (FRAs), interest rate swaps (IRSs).

OIS rates - USD: (effective) federal funds rate, GBP: SONIA (sterling overnight index average), EUR: EONIA (euro
overnight index average), CHF: SARON (Swiss average rate overnight).

