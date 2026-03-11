Limits & Continuity
Understanding model stability and the foundations of Greeks

You're a junior quant. You've just built a pricing model, and your desk head asks: "What happens to the price if volatility drops to nearly zero?"

You punch in 
σ
=
0.001
σ=0.001 and get a reasonable number. Then 
σ
=
0.0001
σ=0.0001 - still fine. But at 
σ
=
0.00001
σ=0.00001, your model spits out garbage. The price jumps wildly. Your hedge ratios explode.

What went wrong? You didn't think about limits.

What You'll Learn
Takeaway
How to analyze what happens as inputs approach extreme values
Why "small change in input → small change in output" matters for hedging
The connection between limits and the Greeks you'll compute daily
How to spot discontinuities that break models
1. The Core Idea
A limit answers: "What value does a function approach as the input gets closer and closer to some target?"

Consider a function 
f
(
x
)
f(x). As 
x
x approaches some value 
a
a, we watch what 
f
(
x
)
f(x) does:

lim
⁡
x
→
a
f
(
x
)
=
L
x→a
lim
​
 f(x)=L
This means: as 
x
x gets arbitrarily close to 
a
a, the outputs 
f
(
x
)
f(x) get arbitrarily close to 
L
L.

The key insight: We care about what happens near the point, not necessarily at the point. The function might not even be defined at 
a
a - but the limit can still exist.

Think of it numerically. Pick inputs approaching 
a
a:

x
=
2.1
,
2.01
,
2.001
,
2.0001
,
…
x=2.1,2.01,2.001,2.0001,…
If the outputs settle toward a single value, that's the limit.

Try It: Computing Simple Limits
Most limits you'll encounter can be solved with direct substitution - just plug in the value:

Direct Substitution
Example
Find 
lim
⁡
x
→
3
(
2
x
2
−
x
+
1
)
lim 
x→3
​
 (2x 
2
 −x+1)

Solution: Since this is a polynomial (no division by zero issues), we can substitute directly:

lim
⁡
x
→
3
(
2
x
2
−
x
+
1
)
=
2
(
3
)
2
−
3
+
1
=
18
−
3
+
1
=
16
x→3
lim
​
 (2x 
2
 −x+1)=2(3) 
2
 −3+1=18−3+1=16
But what if direct substitution gives you 
0
0
0
0
​
 ? That's a signal to factor and simplify:

The 0/0 Case (Removable Discontinuity)
Example
Find 
lim
⁡
x
→
2
x
2
−
4
x
−
2
lim 
x→2
​
  
x−2
x 
2
 −4
​
 

Why it's tricky: Plugging in 
x
=
2
x=2 gives 
0
0
0
0
​
  - undefined. But the limit still exists!

Solution: Factor the numerator:

x
2
−
4
x
−
2
=
(
x
−
2
)
(
x
+
2
)
x
−
2
=
x
+
2
(for 
x
≠
2
)
x−2
x 
2
 −4
​
 = 
x−2
(x−2)(x+2)
​
 =x+2(for x

=2)
Now take the limit:

lim
⁡
x
→
2
(
x
+
2
)
=
4
x→2
lim
​
 (x+2)=4
The function has a "hole" at 
x
=
2
x=2, but as we approach that hole, the values approach 4.

2. Direction Matters
Sometimes you get different answers depending on which side you approach from:

x
→
a
−
x→a 
−
  means approaching from the left (values less than 
a
a)
x
→
a
+
x→a 
+
  means approaching from the right (values greater than 
a
a)
Two-Sided Limit
Definition
The limit 
lim
⁡
x
→
a
f
(
x
)
=
L
lim 
x→a
​
 f(x)=L exists only if both one-sided limits exist and are equal:

lim
⁡
x
→
a
−
f
(
x
)
=
lim
⁡
x
→
a
+
f
(
x
)
=
L
x→a 
−
 
lim
​
 f(x)= 
x→a 
+
 
lim
​
 f(x)=L
If the left and right limits disagree, the limit does not exist.

Why quants care: Option payoffs often have points where left and right behavior differ. At a strike price 
K
K, a digital option pays $0 from the left and $1 from the right - that's a discontinuity, and it causes hedging nightmares.

3. Continuity = No Surprises
A function is continuous at a point if there are no jumps or gaps.

Continuity
Definition
f
f is continuous at 
a
a if:

f
(
a
)
f(a) is defined
lim
⁡
x
→
a
f
(
x
)
lim 
x→a
​
 f(x) exists
lim
⁡
x
→
a
f
(
x
)
=
f
(
a
)
lim 
x→a
​
 f(x)=f(a)
In plain English: the limit equals the actual value. No surprises when you arrive.

Why this matters for models: If your pricing function is continuous in all its inputs (spot, vol, rates), then small input changes produce small output changes. Your hedges work. Your calibration converges. Your P&L doesn't jump unexpectedly.

If it's not continuous somewhere, you need to know exactly where - because that's where your model will misbehave.

4. Limits Are Hidden Everywhere in Quant Finance
Here's the secret: every Greek you'll ever compute is a limit in disguise.

Delta is defined as:

Δ
=
∂
C
∂
S
=
lim
⁡
h
→
0
C
(
S
+
h
)
−
C
(
S
)
h
Δ= 
∂S
∂C
​
 = 
h→0
lim
​
  
h
C(S+h)−C(S)
​
 
You're asking: "If I nudge the spot price by a tiny amount 
h
h, how much does the option price change, per unit of 
h
h?"

That's a limit. Gamma, Vega, Theta, Rho - all limits.

When the limit behaves nicely:

Your Greeks are stable and meaningful
Numerical estimates converge quickly
Hedging actually works
When the limit misbehaves:

Greeks blow up or oscillate
Small input changes cause huge output swings
Your risk management becomes unreliable
5. Spotting Trouble: Discontinuities in Finance
These Financial Objects Have Built-In Problems
Warning
1. Digital (binary) option payoff

f
(
S
T
)
=
{
1
,
S
T
≥
K
0
,
S
T
<
K
f(S 
T
​
 )={ 
1,
0,
​
  
S 
T
​
 ≥K
S 
T
​
 <K
​
 
Discontinuous at 
K
K. The delta near the strike approaches infinity. Hedging is nearly impossible close to expiry.

2. Vanilla call payoff

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
f(S 
T
​
 )=max(S 
T
​
 −K,0)
Continuous, but has a kink at 
K
K. The derivative doesn't exist there. This affects numerical Greeks.

3. Credit events Bond prices jump discretely when a default happens. No smooth path - just a sudden drop.

4. Dividends Stock prices gap down on ex-dividend dates. Another discontinuity your model must handle.

The pattern: whenever you see a payoff with a "cliff" or "kink," you're looking at a limit problem. These are the spots where naive models fail.

6. Putting It Together
Let's return to the scenario from the intro. Your model blew up as 
σ
→
0
σ→0. Now you can diagnose it:

The question you're really asking:

lim
⁡
σ
→
0
C
(
σ
)
=
?
σ→0
lim
​
 C(σ)=?
For a call option, as volatility vanishes:

If the option is in-the-money, the price should approach the discounted intrinsic value
If it's out-of-the-money, the price should approach zero
If your model gives something wildly different, or if tiny changes in 
σ
σ cause huge swings in price, you've found a stability problem. The limit isn't behaving.

This is how quants think. Before trusting any model, ask: "What happens at the extremes? Do the limits make sense?"

Key Takeaways
Takeaway
Limits tell you what happens as inputs approach a value - essential for understanding model behavior at extremes
Continuity means no jumps - if your pricing function is continuous, small input changes give small output changes
Greeks are limits - every sensitivity you compute is a limit definition in disguise
Discontinuities cause problems - digital payoffs, credit events, dividends all create points where limits fail or misbehave
Always check extremes - before trusting a model, ask what happens as parameters go to 0, infinity, or boundary values
What's Next
You now understand what limits and continuity mean and why they matter. But we've been hand-waving around the actual computation.

In the next lesson, The Derivative, you'll learn:

How to formally compute limits (not just reason about them)
The rules that make derivatives tractable
How to derive Greeks from first principles
The tools you build there are what separate someone who uses a pricing formula from someone who can build and debug one.

