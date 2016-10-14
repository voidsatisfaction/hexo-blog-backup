---
layout: post
title: Project Euler 131
categories:
  - Ruby
  - Project Euler
tags:
  - Ruby
  - Project Euler
---

## Problem

### Prime cube partnership
---

There are some prime values, p, for which there exists a positive integer, n, such that the expression n3 + n2p is a perfect cube.

For example, when p = 19, 83 + 82×19 = 123.

What is perhaps most surprising is that for each prime with this property the value of n is unique, and there are only four such primes below one-hundred.

How many primes below one million have this remarkable property?

---

## Analysis

  let n^3 + n^2*p = (n+k)^3
  make it simple, n^2*p = 3*k*n^2 + 3*k^2*n + k**3

  if n <= k, as n, p, k is all integers, k = n*l
  n^2*p = 3*l*n^3 + 3*l^2*n^3 + l^3*n^3
  p = nl(3 + 3*l + l^2)
  as p is a prime n and l should be a 1
  n = k = 1
  p = 7

  if n > k, n = k*l
  k^2l^2p = 3k(kl)^2 + 3k^2(kl) + k^3
  l^2p = 3kl^2 + 3kl + k
  Therefore, p = 3k + 3k/l + k/l^2
  as p is a prime, k = a*l^2, p = 3al^2 + 3al + a = a(3l^2 + 3l + 1)
  so, a = 1 p = 3l^2 + 3l + 1

  Based on this fact, we can find all primes satisfing 3l^2 +3l + 1 under one million including p = 7

  Took 0.004sec

## Solution

```rb

require 'prime'

class Problem131
  def self.find_ans
    i = 1; cache = []
    loop do
      value = 3*i**2 + i*3 + 1
      break if value > 10**6
      cache.push(value) if value.prime?
      i += 1
    end
    cache.length
  end
end

start = Time.now
p Problem131.find_ans
p Time.now - start

```

## Efficiency

O(n)

## Afterthoughts

Other solution.

from umu

What a beautiful nice little problem. Same as most of you, I guess. If n=ap, then n³+n²p=(a³+a²)p³, then a³+a² must be a cube, what is impossible, as next cube after a³ is a³+3a²+3a+1. So n and p are coprime, so are n² and n+p. So if n³+n²p=n²(n+p) is a cube, so n² and n+p are cubes, so n and n+p are cubes. (n+a)³-n³=3a+3a²+a³ is never prime for a>1. So n and n+p are consecutive cubes. So it's enough to check all differences between consecutive cubes for being prime.

정수론은 어렵지만 다가기는 생각보다 쉽고 흥미롭다.
