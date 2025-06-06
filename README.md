# Interest Rate Models

See [Interest Rate Models](Interest%20Rate%20Models.ipynb).

## Basics

### Spot Rates and Forward Rates

Suppose that the zero coupon bond price observed at time t is $P(t,T) \in \mathcal{F}_ {t}$. The forward zero coupon bond price observed at time t is $P(t,S,T) = \frac{P(t,T)}{P(t,S)} \in \mathcal{F}_ {t}$.

Simply-compounded spot rate $F(t,T)$

$$
\begin{aligned}
& P(t,T) \left( 1+F(t,T) \tau(t,T) \right) = 1 \\
\iff & F(t,T) = \frac{1}{\tau(t,T)} \left( \frac{1}{P(t,T)}-1 \right).
\end{aligned}
$$

Simply-compounded forward rate $F(t;S,T)$

$$
\begin{aligned}
& P(t,S,T) \left( 1+F(t,S,T) \tau(S,T) \right) = 1 \\
\iff & F(t,S,T) = \frac{1}{\tau(S,T)} \left( \frac{P(t,S)}{P(t,T)}-1 \right).
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
\iff & R(t,S,T) = \frac{1}{\tau(S,T)} \left( \ln P(t,S) - \ln P(t,T) \right).
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
&=-\left.\frac{1}{P(t,T)} \frac{\partial P(t,T)}{\partial T}\right|_ {T=t} \\
&=-\left.\frac{\partial P(t,T)}{\partial T}\right|_ {T=t}.
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

$P(t,T) = \exp \left( - \int_t^T f(t,s) ds \right)$

$P(t,S,T) = \exp \left( - \int_S^T f(t,s) ds \right)$

$F(t,S,T) = \frac{1}{\tau(S,T)} \left( \exp \left( \int_S^T f(t,s) ds \right)-1 \right)$

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

**LIBOR** rates (prior to December 31, 2021) were calculated (from the quotations provided by the participating banks determined by the ICE Benchmark Administration) for five currencies (USD, GBP, EUR, CHF and JPY) and for seven tenors in respect of each currency (Overnight/1 Day, 1 Week, 1 Month, 2 Months, 3 Months, 6 Months and 12 Months) on each London business day.
[**LIBOR**](https://www.theice.com/iba/libor)

LIBOR based instruments: [Eurodollar futures](https://www.cmegroup.com/trading/interest-rates/stir/eurodollar_contract_specifications.html) (LIBOR futures, i.e. futures on the 3-Month LIBOR rate), forward rate agreements (FRAs), interest rate swaps (IRSs).

OIS rates - USD: **EFFR** (effective federal funds rate), GBP: **SONIA** (sterling overnight index average), EUR: **EONIA** (euro overnight index average) replaced by **ESTR** (euro short-term rate), CHF: **SARON** (Swiss average rate overnight), JPY: **TONAR** (Tokyo overnight average rate).
[**EFFR** (Ticker: FDFD Index)](https://www.newyorkfed.org/markets/reference-rates/effr)
[**SONIA** (Ticker: SONIO/N Index)](https://www.bankofengland.co.uk/-/media/boe/files/markets/benchmarks/sonia-key-features-and-policies)
[**ESTR** (Ticker: ESTRON Index)](https://www.ecb.europa.eu/stats/financial_markets_and_interest_rates/euro_short-term_rate/html/index.en.html)
[**SARON** (Ticker: SRFXON3 Index)]()
[**TONAR** (Ticker: DYENCALM Index)](http://www3.boj.or.jp/market/en/menu_m.htm)

OIS based instruments: LIBOR/OIS basis swaps, [30-Day Federal Funds futures](https://www.cmegroup.com/trading/interest-rates/stir/30-day-federal-fund_contract_specifications.html).

#### [LIBOR Fallback](IBOR-Fallbacks-Fact-Sheet.pdf)



## Pricing

Suppose $0 \le t \le S \le T$.

### Girsanov’s theorem

Consider a Brownian motion $W_t$ under $\mathbb{P}$, let

$$
D_t = exp\left(\int_0^t \theta_s^{\top} dW_s - \frac{1}{2}\theta_s^{\top}\theta_s ds\right) \quad \text{i.e.}\ \ dD_t = \theta_t^{\top} D_t dW_t
$$

and the Radon-Nikodym derivative

$$
\frac{d \mathbb{Q}}{d \mathbb{P}} = D_T.
$$

Then $\widetilde{W}_ t = W_t - \int_0^t \theta_s ds \quad \text{i.e.}\ \ d \widetilde{W}_ t = dW_t - \theta_t dt$ is a Brownian motion under $\mathbb{Q}$ (assume that Novikov’s condition holds).

### Change of Numeraire

See Shreve StoCal II 5.2. Define the the Radon-Nikodym derivative process

$$
\frac{d \mathbb{Q}}{d \mathbb{P}}(t) = \mathbb{E}(D_T \big| \mathcal{F}_ {t}) = D_t.
$$

$$
\frac{d \mathbb{Q}}{d \mathbb{P}}(t) = \cfrac{\cfrac{\mathcal{N}^Q(t)} {\mathcal{N}^P(t)}} {\cfrac{\mathcal{N}^Q(0)} {\mathcal{N}^P(0)}}.
$$

#### Lemma

Let $X$ be a $\mathcal{F}_ {t}$-measurable random variable. Then

$$
\mathbb{E^Q}(X \big| \mathcal{F}_ {s}) = \frac{1}{D_s} \mathbb{E}(X D_t \big| \mathcal{F}_ {s}) = \cfrac{1} {\cfrac{\mathcal{N}^Q(s)} {\mathcal{N}^P(s)}} \mathbb{E}(X \cfrac{\mathcal{N}^Q(t)} {\mathcal{N}^P(t)} \big| \mathcal{F}_ {s}).
$$

#### Example 1

Black-Scholes Model under Risk Neutral Measure $\mathbb{Q}$ (Money market account: $B(t) = e^{\int_0^t r(s) ds}$ as numeraire).

Under B-S Model,

$$
dS = \mu S dt + \sigma S dW
$$

Let

$$
dD = -\lambda D dW, \quad \frac{d \mathbb{Q}}{d \mathbb{P}} = D.
$$

Then $d \widetilde{W} = dW + \lambda dt$ is a Brownian motion under $\mathbb{Q}$. Since $S^B = \frac{S}{B} = e^{-rt} S$ is a martingale under $\mathbb{Q}$,

$$
dS^B = (\mu-r)S^B dt + \sigma S^B dW = (\mu-r-\sigma \lambda)S^B dt + \sigma S^B d \widetilde{W}
$$

$\implies \lambda = \frac{\mu-r}{\sigma}$ and

$$
dS = (\mu-\sigma \lambda) S dt + \sigma S d \widetilde{W} =  rS dt + \sigma S d \widetilde{W}.
$$

#### Example 2

Black-Scholes Model under Stock Measure $\mathbb{Q}$ (Stock: $S$ as numeraire).

Since $B^S = \frac{B}{S} = e^{rt} S^{-1}$ is a martingale under $\mathbb{Q}$,

$$
dB^S = (r-\mu+\sigma^2)B^S dt - \sigma B^S dW = (r-\mu+\sigma^2+\sigma \lambda)B^S dt - \sigma B^S d \widetilde{W}
$$

$\implies \lambda = \frac{\mu-r-\sigma^2}{\sigma}$ and

$$
dS = (\mu-\sigma \lambda) S dt + \sigma S d \widetilde{W} =  (r+\sigma^2)S dt + \sigma S d \widetilde{W}.
$$

&nbsp;

Suppose that **Funding rate** is $F(t,T)$, with discount factor $P(t,T)$. **Float rate** is LIBOR rate $L(t,T)$.

### FRAs

FRAs PV at payment date $S$ is

$$
\frac{N \tau(S,T) \left( FRA - L(S,S,T) \right)}{1 + \tau(S,T)L(S,S,T)}
$$

$\mathbb{E}^{\mathbb{Q}_ S} \left(\frac{FRA - L(S,S,T)}{1 + \tau(S,T)L(S,S,T)} \right) = 0 \implies$

FRA at time $t$ is $\text{FRA}(t,T) = L(t,S,T) = \mathbb{E}^{\mathbb{Q}_ T} [L(S,S,T) \big| \mathcal{F}_ {t}]$.

### Futures

Futures price at settlement date $S$ is

$$
100(1-L(S,S,T))
$$

Futures price at time $t$ is $\text{Fut}(t,T) = \mathbb{E}^{\mathbb{Q}} [100(1-L(S,S,T)) \big| \mathcal{F}_ {t}]$.

$\text{Fut}(t,T) \le 100(1-L(t,S,T))$. Futures pays $\text{Fut}(t,T) - \text{Fut}(S,T)$ to the exchange over the period $[t,S]$. The corresponding FRA traded at time $t$ pays $100(L(t,S,T) - L(S,S,T))$ at $T$ (in reality FRA payment/settlement date is $S$).

Futures are similar to FRAs: If $\text{Fut}(t,T) = 100(1-L(t,S,T))$, then both contracts make the exact same payment. If LIBOR rises over the period $[t,S]$, FRA would be the better contract to have entered (better to pay later); if LIBOR drops, futures would be the better (better to receive earlier). However, if LIBOR rises, the purchaser of the future will finance the losses paid to the exchange at a higher rate; if LIBOR drops, the purchaser of the future will reinvest the profits received from the exchange at a lower rate.

Standard Credit Support Annexes (CSAs):
- Type of collateral: cash.
- Currency of collateral: locally specific to the product.
- Thresholds: zero, exchange on any liability.
- Frequency of exchange: daily.
- Bilateral or unilateral: bilateral.
- Remuneration: OIS rate.

**Consider FRAs with standard CSAs:**
- If LIBOR rises over the period $[t,S]$, FRA would be the better contract to have entered (the purchaser of the FRA still receives OIS interest on the collateral from the counterparty);
- If LIBOR drops, futures would be the better (the purchaser of the FRA needs to pay back OIS interest on the collateral to the counterparty).

The exact relationship between futures price and FRA depends on the discount curve over the period $[t,S]$:
- When LIBOR goes up the discount curve steepens, the purchaser of the future pays money to the exchange = the purchaser of the FRA pays cash collateral to the counterparty; but the purchaser of the FRA will receive more interest on the collateral from the counterparty, while the purchaser of the future will pay more interest to finance the losses, which leads to an increased advantage to the FRA;
- When LIBOR goes down the discount curve flattens, the purchaser of the future receives money from the exchange = the purchaser of the FRA receives cash collateral from the counterparty; but the purchaser of the FRA will pay less interest on the collateral to the counterparty, while the purchaser of the future will receive less interest on the profits, which reduces the disadvantage to the FRA.

### Bond Futures

**Implied repo rate** for a bond in the delivery basket of the bond futures contract is the rate of return that can be earned by simultaneously selling a bond futures contract and buying the underlying bond for delivery within the delivery window (from first delivery date to last delivery date).

For bonds in the delivery basket of the bond futures contract:

- **Futures Implied Forward Bond (Clean) Price** = Futures Price * Conversion Factor
- **Gross Basis** = Bond Clean Price - Futures Implied Forward Bond (Clean) Price
- Note: Bond Dirty Price = Bond Clean Price + Accrued Interest(*Settlement Date*)
- **Net Basis** = Repo Curve Implied Forward Bond (Clean) Price - Futures Implied Forward Bond (Clean) Price
- Note: Repo Curve Implied Forward Bond (Clean) Price = Bond Dirty Price / Repo Curve Discount Factor(*Settlement Date, Delivery Date*) - Coupon / Repo Curve Discount Factor(*Coupon Payment Date, Delivery Date*) - Accrued Interest(*Delivery Date*) (doesn't depend on futures price)
- Note: Futures Price and Bond Clean Price are market (BBG) quotes. 

#### Cheapest to Deliver

- Bond with highest implied repo rate (depends on delivery date)
- Bond with lowest gross basis / net basis

#### Bond Futures Basis

- **Solve Equation**: Funding Curve + ZSpread + Bond Futures Basis $\Rightarrow$ Bond PV for CashFlows from Delivery Date == Futures Implied Bond PV
- Note: Futures Implied Bond PV = Futures Implied Forward Bond Dirty Price * Repo Curve Discount Factor(*Settlement Date, Delivery Date*)
- Note: Futures Implied Forward Bond Dirty Price = Futures Implied Forward Bond (Clean) Price + Accrued Interest(*Delivery Date*)

### Swaps

### Caps and Floors

T-forward measure $\mathbb{Q}_ T$ (Zero coupon bond which matures at $T$: $P(t,T) = P(t,t,T)$ as numeraire).

Key: OIS forward rate $F(t,S,T) \in \mathcal{F}_ {t}$ is a martingale under $\mathbb{Q}_ T$, (assume that LIBOR/OIS spread is deterministic), LIBOR forward rate $L(t,S,T) \in \mathcal{F}_ {t}$ is a martingale under $\mathbb{Q}_ T$.

[T-forward measure](The%20T-Forward%20Measure.pdf)

### Swaptions

Swap measure $\mathbb{Q}_ {T_0,T}$ (**Spot annuity function/Spot PV01/(Fixed Leg) Spot Ann01** of a forward starting swap which settles at $T_0$ and matures at $T$: $A(t,t,T_0,T)$ as numeraire).

**Forward annuity/Forward PV01/(Fixed Leg) Forward Ann01** at forward date $S$ is $A(t,S,T_0,T) = \sum\limits_{T_j \in [T_0, T]} \tau(T_{j-1},T_j) P(t,S,T_j) = \sum\limits_{T_j \in [T_0, T]} \tau(T_{j-1},T_j) P(t,T_j) / P(t,S) = A(t,t,T_0,T) / P(t,S)$.

Forward premium (%, in percentage of notional) at option expiry date $S$ is $A(t,S,T_0,T) * BreakEven(t)$.

Spot premium (%) at spot date $t$ is $A(t,t,T_0,T) * BreakEven(t)$.

$BreakEven(t) =\mathbb{E}^{\mathbb{Q}_ {T_0,T}} [(K - S(S,T_0,T))^+ \big| \mathcal{F_t}]$ under BlackNormalModel or BlackLogNormalModel.

Key: Forward swap rate (break-even or mid-market forward swap rate) $S(t,T_0,T)$ is a martingale under $\mathbb{Q}_ {T_0,T}$.

### Mid-Curve Swaptions

### Interest Rate Futures Options & Mid-Curve Interest Rate Futures Options

### Convexity Adjustment

The convexity adjustment for **LIBOR-in-arrears swaps** is

$$
\mathbb{E}^{\mathbb{Q}_ S}(L(S,S,T))-L(0,S,T)
$$

Under $\mathbb{Q}_ S$, $P(t,S) = P(t,t,S)$ as numeraire, PV is

$$
\frac{P}{P(0,S)} = \mathbb{E}^{\mathbb{Q}_ S} \left(\frac{L(S,T)}{P(S,S)}\right)
$$

Under $\mathbb{Q}_ T$, $P(t,T) = P(t,t,T)$ as numeraire, PV is

$$
\frac{P}{P(0,T)} = \mathbb{E}^{\mathbb{Q}_ T} \left(\frac{L(S,T)}{P(S,T)}\right)
$$

Thus (or applying change of numeraire),

$$
\mathbb{E}^{\mathbb{Q}_ S}(L(S,S,T)) = \mathbb{E}^{\mathbb{Q}_ T} \left(L(S,S,T) \frac{P(0,S,T)}{P(S,S,T)}\right).
$$

&nbsp;

The convexity adjustment for **futures** is

$$
\mathbb{E}^{\mathbb{Q}}(L(S,S,T))-L(0,S,T)
$$

Under $\mathbb{Q}$, $B(t) = e^{\int_0^t r(s) ds}$ as numeraire,

$$
P(t,T) = \mathbb{E}^{\mathbb{Q}} \left( e^{ - \int_t^T r(s) ds} \big| \mathcal{F}_ {t} \right)
$$

$f(t,T)$ is a martingale under $\mathbb{Q}_ T$:

$$
\begin{aligned}
f(t,T) &=-\frac{1}{P(t,T)} \frac{\partial P(t,T)}{\partial T} \\
&=\frac{1}{P(t,T)} \mathbb{E}^{\mathbb{Q}} \left( r(T) e^{ - \int_t^T r(s) ds} \big| \mathcal{F}_ {t} \right) \\
&=\mathbb{E}^{\mathbb{Q}_ T} \left( r(T) \big| \mathcal{F}_ {t} \right).
\end{aligned}
$$

#### HJM Model under $\mathbb{Q}$:

[Relationships between interest rate dynamics](Interest%20Rate%20Dynamics.pdf)

$$
df(t,T) = \alpha_{t,T} dt + \sigma_{t,T} dW_t
$$

Applying Girsanov’s theorem,

$$
D_t = \frac{d \mathbb{Q}_ T}{d \mathbb{Q}}(t) = \frac{P(t,T) e^{ - \int_0^t r(s) ds}} {P(0,T)}
$$

$d W_t^T = dW_t -  \frac{dD(t)}{D(t)} dW_t$ is a Brownian motion under $\mathbb{Q}_ T$ and

$$
\begin{aligned}
d \ln{P(t,T)} &= d (- \int_t^T f(t,s) ds) \\
&= r(t) dt - \int_t^T df(t,s) ds \\
&= r(t) dt - \left(\int_t^T \alpha_{t,s} ds \right) dt - \left(\int_t^T \sigma_{t,s} ds \right) dW_t \\
&= \left(r(t) - A_{t,T} \right) dt - \Sigma_{t,T} dW_t \\
\
\frac{dP(t,T)}{P(t,T)} &= \left(r(t) - A_{t,T} + \frac{1}{2} \Sigma_{t,T}^2 \right)dt - \Sigma_{t,T} dW_t \\
\\
\frac{dD(t)}{D(t)} &= -r(t) dt + \frac{dP(t,T)}{P(t,T)} \\
&= \left(-A_{t,T} + \frac{1}{2} \Sigma_{t,T}^2 \right)dt - \Sigma_{t,T} dW_t
\end{aligned}
$$

so $d W_t^T = dW_t + \Sigma_{t,T} dt$ is a Brownian motion under $\mathbb{Q}_ T$. Since $df(t,T) = (\alpha_{t,T} - \sigma_{t,T}\Sigma_{t,T})  dt + \sigma_{t,T} dW_t^T$ is a martingale under $\mathbb{Q}_ T$, $\alpha_{t,T} = \sigma_{t,T}\Sigma_{t,T}, A_{t,T} = \frac{1}{2} \Sigma_{t,T}^2$.

Under $\mathbb{Q}_ T$,

$$
\begin{aligned}
df(t,T) &= \sigma_{t,T} dW_t^T \\
d \ln{P(t,T)} &= \left(r(t) + \frac{1}{2} \Sigma_{t,T}^2 \right) dt - \Sigma_{t,T} dW_t^T \\
\frac{dP(t,T)}{P(t,T)} &= \left(r(t) + \Sigma_{t,T}^2 \right) dt - \Sigma_{t,T} dW_t^T.
\end{aligned}
$$

Under $\mathbb{Q}$,

$$
\begin{aligned}
df(t,T) &= \sigma_{t,T}\Sigma_{t,T} dt + \sigma_{t,T} dW_t \\
d \ln{P(t,T)} &= \left(r(t) - \frac{1}{2} \Sigma_{t,T}^2 \right) dt - \Sigma_{t,T} dW_t \\
\frac{dP(t,T)}{P(t,T)} &= r(t) dt - \Sigma_{t,T} dW_t.
\end{aligned}
$$

Special case: Ho-Lee Model and Hull-White Models
