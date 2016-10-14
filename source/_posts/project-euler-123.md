---
layout: post
title: Project Euler 123
categories:
  - Ruby
  - Project Euler
tags:
  - Ruby
  - Project Euler
---

## Problem

### Prime square remainders
#### Problem 123

---

Let pn be the nth prime: 2, 3, 5, 7, 11, ..., and let r be the remainder when (pn−1)n + (pn+1)n is divided by pn2.

For example, when n = 3, p3 = 5, and 43 + 63 = 280 ≡ 5 mod 25.

The least value of n for which the remainder first exceeds 109 is 7037.

Find the least value of n for which the remainder first exceeds 1010.

---

## Analysis

n is the n term of prime. if so,
remainder = (Pn-1)^n + (Pn+1)^n === n*Pn*({1+[-1]^(n-1)} + {1 + [-1]^(n)}) (mod Pn^2)

In this situation, n should be odd since the remainder is 2 if n is even.

Therefore, remainder is 2*n*Pn (n is odd)

Based on this fact, we can get first nth prime that exceeds 10^10 by using bruteforce.

Efficiency O(n^(3/2))
Took 1.8sec

## Solution

```rb
class Problem123
  def self.find_ans
    limit = 10**10 ; i = 3 ; n = 1
    loop do
      if prime?(i)
        if n % 2 === 1
          n += 1
        else
          n += 1
          value = 2*n*i
          return n if value > limit
        end
      end
      i += 2
    end
  end

  def self.prime?(n)
    2.upto(Math.sqrt(n)){ |i| return false if n % i === 0 }
    return true
  end
end

start = Time.now
p Problem123.find_ans
p Time.now - start
```

## Efficiency
O(n^(3/2))

## Afterthoughts
hk's solution on forum was quite interesting.

he used the fact that

> the number of primes less than n tends to n/ln(n)

then, n can be substituted by n/ln(n).
thus, remainder could be substituted by 2*Pn^2/ln(n)

Of course, according to [Prime number theorem - Wikipedia](https://en.wikipedia.org/wiki/Prime_number_theorem),

pi(n) is almost equal to(~) n/ln(n).

> the asymptotic notation meaning, again, that the relative error of this approximation approaches 0 as n increases without bound.
