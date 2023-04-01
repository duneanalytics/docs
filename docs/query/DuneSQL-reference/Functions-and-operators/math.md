---
title: Mathematical functions and operators
---

# Mathematical operators

| Operator | Description                                      |
|----------|--------------------------------------------------|
| `+`      | Addition                                         |
| `-`      | Subtraction                                      |
| `*`      | Multiplication                                   |
| `/`      | Division (integer division performs truncation)  |
| `%`      | Modulus (remainder)                              |

## Mathematical functions

#### abs()
**``abs(x)``** → same as input  
Returns the absolute value of `x`.

#### cbrt()
**``cbrt(x)``** → double  
Returns the cube root of `x`.

#### ceil()
**``ceil(x)``** → same as input  
This is an alias for `ceiling`.

#### ceiling()
**``ceiling(x)``** → same as input  
Returns `x` rounded up to the nearest integer.

#### degrees()
**``degrees(x)``** → double  
Converts angle `x` in radians to degrees.

#### e()
**``e()``** → double  
Returns the constant Euler's number.

#### exp()
**``exp(x)``** → double  
Returns Euler's number raised to the power of `x`.

#### floor()
**``floor(x)``** → same as input  
Returns `x` rounded down to the nearest integer.

#### ln()
**``ln(x)``** → double  
Returns the natural logarithm of `x`.

#### log()
**``log(b, x)``** → double  
Returns the base `b` logarithm of `x`.

#### log2()
**``log2(x)``** → double  
Returns the base 2 logarithm of `x`.

#### log10()
**``log10(x)``** → double  
Returns the base 10 logarithm of `x`.

#### mod()
**``mod(n, m)``** → same as input  
Returns the modulus (remainder) of `n` divided by `m`.

#### pi()
**``pi()``** → double  
Returns the constant Pi.

#### pow()
**``pow(x, p)``** → double  
This is an alias for `power`.

#### power()
**``power(x, p)``** → double  
Returns `x` raised to the power of `p`.

#### radians()
**``radians(x)``** → double  
Converts angle `x` in degrees to radians.

#### round()
**``round(x)``** → same as input  
Returns `x` rounded to the nearest integer.

#### round()
**``round(x, d)``** → same as input  
Returns `x` rounded to `d` decimal places.

#### sign()
**``sign(x)``** → same as input  
Returns the signum function of `x`, that is:
-   0 if the argument is 0,
-   1 if the argument is greater than 0,
-   -1 if the argument is less than 0.
For double arguments, the function additionally returns:
-   NaN if the argument is NaN,
-   1 if the argument is +Infinity,
-   -1 if the argument is -Infinity.

#### sqrt()
**``sqrt(x)``** → double  
Returns the square root of `x`.

#### truncate()
**``truncate(x)``** → double  
Returns `x` rounded to integer by dropping digits after decimal point.

#### width_bucket()
**``width_bucket(x, bound1, bound2, n)``** → bigint  
Returns the bin number of `x` in an equi-width histogram with the specified `bound1` and `bound2` bounds and `n` number of buckets.

#### width_bucket()
**``width_bucket(x, bins)``** → bigint  
Returns the bin number of `x` according to the bins specified by the array `bins`. The `bins` parameter must be an array of doubles and is assumed to be in sorted ascending order.

## Random functions

#### rand()
**``rand()``** → double  
This is an alias for `random()`.

#### random()
**``random()``** → double  
Returns a pseudo-random value in the range 0.0 <= x < 1.0.

#### random()
**``random(n)``** → same as input  
Returns a pseudo-random number between 0 and n (exclusive).

#### random()
**``random(m, n)``** → same as input  
Returns a pseudo-random number between m and n (exclusive).

## Trigonometric functions
All trigonometric function arguments are expressed in radians. See unit conversion functions `degrees` and `radians`.

#### acos()
**``acos(x)``** → double  
Returns the arc cosine of `x`.

#### asin()
**``asin(x)``** → double  
Returns the arc sine of `x`.

#### atan()
**``atan(x)``** → double  
Returns the arc tangent of `x`.

#### atan2()
**``atan2(y, x)``** → double  
Returns the arc tangent of `y / x`.

#### cos()
**``cos(x)``** → double  
Returns the cosine of `x`.

#### cosh()
**``cosh(x)``** → double  
Returns the hyperbolic cosine of `x`.

#### sin()
**``sin(x)``** → double  
Returns the sine of `x`.

#### tan()
**``tan(x)``** → double  
Returns the tangent of `x`.

#### tanh()
**``tanh(x)``** → double  
Returns the hyperbolic tangent of `x`.

## Floating point functions

#### infinity()
**``infinity()``** → double  
Returns the constant representing positive infinity.

#### is_finite()
**``is_finite(x)``** → boolean  
Determine if `x` is finite.

#### is_infinite()
**``is_infinite(x)``** → boolean  
Determine if `x` is infinite.

#### is_nan()
**``is_nan(x)``** → boolean  
Determine if `x` is not-a-number.

#### nan()
**``nan()``** → double  
Returns the constant representing not-a-number.

## Base conversion functions

#### from_base()
**``from_base(string, radix)``** → bigint  
Returns the value of `string` interpreted as a base-`radix` number.

#### to_base()
**``to_base(x, radix)``** → varchar  
Returns the base-`radix` representation of `x`.

## Statistical functions

#### cosine_similarity()
**``cosine_similarity(x, y)``** → double  
Returns the cosine similarity between the sparse vectors `x` and `y`:
    SELECT cosine_similarity(MAP(ARRAY['a'], ARRAY[1.0]), MAP(ARRAY['a'], ARRAY[2.0])); -- 1.0

#### wilson_interval_lower()
**``wilson_interval_lower(successes, trials, z)``** → double  
Returns the lower bound of the Wilson score interval of a Bernoulli
trial process at a confidence specified by the z-score `z`.

#### wilson_interval_upper()
**``wilson_interval_upper(successes, trials, z)``** → double  
Returns the upper bound of the Wilson score interval of a Bernoulli
trial process at a confidence specified by the z-score `z`.

## Cumulative distribution functions

#### beta_cdf()
**``beta_cdf(a, b, v)``** → double  
Compute the Beta cdf with given a, b parameters: P(N < v; a, b). The a,
b parameters must be positive real numbers and value v must be a real
value. The value v must lie on the interval [0, 1].

#### inverse_beta_cdf()
**``inverse_beta_cdf(a, b, p)``** → double  
Compute the inverse of the Beta cdf with given a, b parameters for the
cumulative probability (p): P(N < n). The a, b parameters must be
positive real values. The probability p must lie on the interval [0,
1].

#### inverse_normal_cdf()
**``inverse_normal_cdf(mean, sd, p)``** → double  
Compute the inverse of the Normal cdf with given mean and standard

#### normal_cdf()
**``normal_cdf(mean, sd, v)``** → double  
Compute the Normal cdf with given mean and standard deviation (sd): P(N
< v; mean, sd). The mean and value v must be real values and the
standard deviation must be a real and positive value.

