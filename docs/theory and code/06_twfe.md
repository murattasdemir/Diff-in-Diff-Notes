---
layout: default
title: TWFE
parent: Theory and code
nav_order: 1
mathjax: true
---

Since you clicked, here is a preview of what is going on behind the scenes:

# The classic 2x2 DiD or the Twoway Fixed Effects Model (TWFE)

Let us start with the classic Twoway Fixed Effects (TWFE) model:

$$ y_{it} = \beta_0 + \beta_1 Treat_i + \beta_2 Post_t + \beta_3 Treat_i Post_t + \epsilon_{it}  $$


where $$ y_{it} $$ is the outcome variable of interest, $$ \alpha_i $$ is the treatment variable, $$ \alpha_t $$ is the post variable, and $$ \beta $$ is the coefficient of interest.

In a very simple form, a two by two (2x2) model can be explained using the following table:



| Post\Treatment | Treatment = 0 | Treatment = 1 | *Difference*  | 
| ----- | ----- | ----- | -----   |
| **Post = 0** |  $$ \beta_0 $$   | $$ \beta_0 + \beta_1 $$    |  $$ \beta_1 $$  |
| **Post = 1** |  $$\beta_0 + \beta_2 $$   |  $$ \beta_0 + \beta_1 + \beta_2 + \beta_3 $$  |  $$ \beta_1 + \beta_3 $$   |
| ** *Difference* ** | $$ \beta_2 $$   |  $$ \beta_2 + \beta_3 $$  | $$ \beta_3 $$   |




# The triple difference estimator (DDD)

The triple difference estimator essential takes two DDs, one with the target unit of analysis with a treated and an untreated group. This is compared to another similar group in the pre and post-treatment period. Fo effectively there are two treatments. One where an actual treatment on the desired group is tested, and a placebo comparison group, on which the same intervention is also applied.

$$ Y_{it} = \beta_0 + \beta_1 P_{i} + \beta_2 C_{j} + \beta_3 T_t + \beta_4 (P_i T_t) + \beta_5 (C_j T_t) + \beta_6 (P_i C_j) + \beta_7 (P_i C_j T_t) + \epsilon_{it} $$



where we have 3x3 combinations: P = {0,1}, T={0,1}, C={0,1}. As is the case with the 2x2 DD, here the coefficient of interest is $$ \beta_7 $$. This can also be broken down in a table form. But rather than create one big table, the results are usually presented for C = 0, or the main treatment group, and for C = 1, or the main comparison group. The difference between the two boils down to $$ \beta_7 $$. Let's see this here:


Main group (C = 0):


|          | T = 0 | T = 1 | Difference  | 
| -------- | ----- | ----- | -----   |
| **P = 0** | $$ \beta_0 $$  | $$ \beta_0 + \beta_3 $$   | $$ \beta_3 $$ |
| **P = 1** | $$ \beta_0 + \beta_1 $$ | $$ \beta_0 + \beta_1 + \beta_3 + \beta_4 $$  | $$ \beta_3 + \beta_4 $$  |
| Difference | $$ \beta_3 $$  | $$ \beta_3 + \beta_4 $$  | $$ \beta_4 $$  |

Comparison group (C = 1):

|          | T = 0 | T = 1 | Difference | 
| -------- | ----- | ----- | -----   |
| **P = 0** | $$ \beta_0 + \beta_2 $$  | $$ \beta_0 + \beta_2 + \beta_3 + \beta_5  $$  | $$ \beta_3 + \beta_5 $$  |
| **P = 1** | $$ \beta_0 + \beta_1 + \beta_2 + \beta_6  $$ | $$ \beta_0 + \beta_1 + \beta_2 + \beta_3 + \beta_4 + \beta_5 + \beta_6 + \beta_7 $$  | $$ \beta_3 + \beta_4 + \beta_5 + \beta_7  $$ |
| Difference | $$ \beta_1 + \beta_6  $$  | $$ \beta_1 + \beta_4 + \beta_6 + \beta_7 $$ | $$ \beta_4 + \beta_7 $$  |


Let's take the difference between the two matrices or (C = 1) - (C = 0):


|          | T = 0 | T = 1 | Difference  | 
| -------- | ----- | ----- | -----   |
| **P = 0** | $$ \beta_2  $$ | $$ \beta_2 + \beta_5 $$   |  $$ \beta_5 $$ |
| **P = 1** | $$ \beta_2 + \beta_6 $$ | $$ \beta_2 + \beta_5 + \beta_6 + \beta_7 $$ | $$ \beta_6 + \beta_7 $$  |
| Difference |  $$ \beta_6 $$   | $$ \beta_6 + \beta_7 $$ | $$ \beta_7 $$   |

where we end up with the main difference of $$ \beta_7 $$. Note that this table logic is also far simpler than having a long list of expectations defined for each combination.

## The generic TWFE functional form:

$$ y_{it} = \alpha_{i} + \alpha_t + \beta D_{it} + \epsilon_{it} $$


## Code

Let us generate a simple 2x2 example in Stata. First step define the panel structure. Since it is a 2x2, we just need two units and two time periods:

```r
clear
local units = 2
local start = 1
local end   = 2

local time = `end' - `start' + 1
local obsv = `units' * `time'
set obs `obsv'

egen id	   = seq(), b(`time')  
egen t 	   = seq(), f(`start') t(`end') 	

sort id t
xtset id t

lab var id "Panel variable"
lab var t  "Time  variable"
```

Next we define the treatment group and a generic TWFE model without adding any variation or error terms:

```r
gen D = id==2 & t==2

gen btrue = cond(D==1, 2, 0) 		
	gen Y = id + 3*t + btrue*D 
```

According to the last line, the treatment effect should have an impact of 3 units on Y in the post group. We can check this by plotting the data:

```r
twoway ///
	(connected Y t if id==1) ///
	(connected Y t if id==2) ///
		,	///
		legend(order(1 "id=1" 2 "id=2")) ///
		xlabel(1 2) ylabel(4(1)10)
```

which gives us:

[](../../assets/images/twfe.png)

<img src="../../assets/images/twfe.png" height="400" title="TWFE">