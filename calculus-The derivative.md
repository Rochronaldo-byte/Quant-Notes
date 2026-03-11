The Derivative
gradients, Jacobians; sensitivity of P&L to params

1. Why Derivatives Matter in Quant Finance
In quant finance, the derivative of a function is not just a calculus exercise — it is the foundation of:

Greeks
hedging
risk management
model calibration
sensitivity analysis
optimization
If limits tell us how a function behaves as we approach something, derivatives tell us how fast it changes at that point.

In a trading desk, this is everything:

Delta tells you how your option price responds to tiny moves in the underlying.
Gamma tells you how Delta itself changes.
Vega tells you how sensitive you are to volatility.
Rho tells you how sensitive you are to interest rates.
No quant can operate without thinking in derivatives.

In this lesson, we build the intuition using both math and finance examples.

2. Intuition: The Derivative as Instantaneous Change
The derivative measures how fast a function changes as its input changes.

The Derivative
Definition
f
′
(
x
)
=
lim
⁡
h
→
0
f
(
x
+
h
)
−
f
(
x
)
h
.
f 
′
 (x)= 
h→0
lim
​
  
h
f(x+h)−f(x)
​
 .
Interpretation:

Look at how much the output changes.
Divide by how much the input changes.
Make that input change infinitely small.
If 
f
′
(
x
)
f 
′
 (x) is large:

tiny changes in input → big output effects
(this means big sensitivity / big risk)
If 
f
′
(
x
)
f 
′
 (x) is small:

tiny changes in input → tiny output effects
(this means stable / low sensitivity)
A geometric picture
The derivative is the slope of the tangent line to the graph of 
f
(
x
)
f(x) at 
x
x.

Positive slope → increasing function
Negative slope → decreasing function
Slope = 0 → flat point (potential minimum/maximum)
This interpretation becomes extremely important for optimization in quant work.

3. Basic Rules of Differentiation
Here are the essential rules every quant must know.

Power rule
d
d
x
x
n
=
n
x
n
−
1
.
dx
d
​
 x 
n
 =nx 
n−1
 .
Constant rule
d
d
x
c
=
0.
dx
d
​
 c=0.
Constant multiple rule
d
d
x
(
c
f
(
x
)
)
=
c
f
′
(
x
)
.
dx
d
​
 (cf(x))=cf 
′
 (x).
Sum rule
d
d
x
(
f
(
x
)
+
g
(
x
)
)
=
f
′
(
x
)
+
g
′
(
x
)
.
dx
d
​
 (f(x)+g(x))=f 
′
 (x)+g 
′
 (x).
Product rule
(
f
g
)
′
=
f
′
g
+
f
g
′
.
(fg) 
′
 =f 
′
 g+fg 
′
 .
Quotient rule
(
f
g
)
′
=
f
′
g
−
f
g
′
g
2
.
( 
g
f
​
 ) 
′
 = 
g 
2
 
f 
′
 g−fg 
′
 
​
 .
Chain rule (extremely important in quant work)
d
d
x
f
(
g
(
x
)
)
=
f
′
(
g
(
x
)
)
⋅
g
′
(
x
)
.
dx
d
​
 f(g(x))=f 
′
 (g(x))⋅g 
′
 (x).
Why Chain Rule Matters in Finance
Intuition
In financial modeling, almost everything is a chain-rule situation:

volatility inside 
d
1
d 
1
​
  inside 
Φ
Φ inside the option price
discount factors inside payoff functions
log transformations inside stochastic models
4. Quant Application 1: Derivative of 
S
2
S 
2
  and a Simple Sensitivity
Derivative of $S^2$
Example
Consider the function

f
(
S
)
=
S
2
.
f(S)=S 
2
 .
Using the limit definition:

f
′
(
S
)
=
lim
⁡
h
→
0
(
S
+
h
)
2
−
S
2
h
=
lim
⁡
h
→
0
2
S
h
+
h
2
h
=
2
S
+
h
→
2
S
.
f 
′
 (S)= 
h→0
lim
​
  
h
(S+h) 
2
 −S 
2
 
​
 = 
h→0
lim
​
  
h
2Sh+h 
2
 
​
 =2S+h→2S.
This means: a 1-unit increase in 
S
S changes 
S
2
S 
2
  by approximately 
2
S
2S units.

This exact logic is how Delta works conceptually:

"How much does my option price change if spot goes up a tiny bit?"

We will revisit this when we discuss Greeks.

5. Quant Application 2: Differentiating the Black–Scholes Price (Delta)
The Black–Scholes call price is:

C
(
S
0
)
=
S
0
Φ
(
d
1
)
−
K
e
−
r
T
Φ
(
d
2
)
.
C(S 
0
​
 )=S 
0
​
 Φ(d 
1
​
 )−Ke 
−rT
 Φ(d 
2
​
 ).
If we take its derivative with respect to spot 
S
0
S 
0
​
  (treating volatility, 
r
r, and 
T
T as constants), we get the Delta:

Δ
=
∂
C
∂
S
0
=
Φ
(
d
1
)
.
Δ= 
∂S 
0
​
 
∂C
​
 =Φ(d 
1
​
 ).
This is one of the most important formulas in all of finance.

Interpretation
If 
Δ
=
0.6
Δ=0.6, then a $1 move in the stock changes the call price by about $0.60.
If 
Δ
=
1
Δ=1, the option behaves like the underlying asset.
If 
Δ
=
0
Δ=0, the option behaves like a worthless lottery ticket.
Chain rule intuition
This derivative comes from:

S
0
S 
0
​
  appears inside 
d
1
d 
1
​
 
d
1
d 
1
​
  appears inside 
Φ
Φ
Φ
Φ appears inside the pricing formula
It is a perfect example of the chain rule in action.

6. Quant Application 3: The Derivative of a Payoff
Take the call payoff:

f
(
S
T
)
=
max
⁡
(
S
T
−
K
,
0
)
.
f(S 
T
​
 )=max(S 
T
​
 −K,0).
For 
S
T
<
K
S 
T
​
 <K:

payoff = 0
slope = 0
For 
S
T
>
K
S 
T
​
 >K:

payoff = 
S
T
−
K
S 
T
​
 −K
slope = 1
At the strike 
S
T
=
K
S 
T
​
 =K:

the left derivative = 0
the right derivative = 1
Since they differ, the derivative does not exist at the strike (there is a kink).

Non-Differentiability at the Strike
Warning
Gamma becomes large near the strike for short maturities.
Hedging becomes unstable near kinks.
Numerical methods struggle at non-smooth points.
7. Higher-Order Derivatives (Gamma)
If Delta is:

Δ
=
∂
C
∂
S
0
,
Δ= 
∂S 
0
​
 
∂C
​
 ,
then Gamma is:

Γ
=
∂
2
C
∂
S
0
2
.
Γ= 
∂S 
0
2
​
 
∂ 
2
 C
​
 .
Interpretation:

Delta = rate of change of price
Gamma = rate of change of Delta
High Gamma means:

your Delta changes rapidly,
small market moves can drastically alter your risk,
hedging requires constant adjustments.
In practical trading:

Deep ITM/OTM options → low Gamma
At-the-money options → high Gamma
Short-dated ATM options → extremely high Gamma
Derivatives help you understand and measure this sensitivity precisely.

8. Worked Example: Derivative of a Discount Factor
Discount Factor Sensitivity
Example
A simple but important object in finance is the discount factor:

D
(
r
)
=
e
−
r
T
.
D(r)=e 
−rT
 .
Differentiate with respect to 
r
r:

D
′
(
r
)
=
d
d
r
e
−
r
T
=
−
T
e
−
r
T
.
D 
′
 (r)= 
dr
d
​
 e 
−rT
 =−Te 
−rT
 .
This tells you:

as interest rates increase, discount factors decrease,
and they decrease at a rate proportional to 
T
T.
Long-maturity cash flows are much more sensitive to interest rate changes than short-maturity ones.

This is another perfect example of sensitivity analysis via derivatives.

9. Summary
Key Takeaways
Takeaway
The derivative measures instantaneous rate of change.
It is the foundation of sensitivities (Greeks) in quant finance.
Key rules: power rule, product rule, chain rule.
Delta is 
Φ
(
d
1
)
Φ(d 
1
​
 ), the derivative of the Black-Scholes call price with respect to spot.
Payoff functions can be non-differentiable at kinks (e.g., strike).
Gamma tells you how fast Delta changes and is highest at the money.
Derivatives let you measure how models react to tiny input changes - essential for hedging and risk control.
This intuition will be crucial when we move into integrals and optimization.
