---
layout: post
title: Project Euler 124
categories:
  - Ruby
  - Project Euler
tags:
  - Ruby
  - Project Euler
---

## Problem

### Ordered radicals
#### Problem 124
---

**[problem is here](https://projecteuler.net/problem=124)**

---

## Solution

- bruteforce

- dictionary

You can define rad function by using prime_division method.

And from 1 to 100000, you can get each of rad value.

If a number's rad is not included in cache, create new array of the rad value set.
If it is included, just add on the rad value set

After that, you can easily get E(10000)

```rb

require 'prime'

class Problem124
  def self.find_ans
    cache = {}
    1.upto(10**5) do |i|
      rad = rad(i).to_s
      cache.has_key?(rad) ? cache[rad].push(i) : cache[rad] = [i]
    end
    cache.values.flatten[9999]
  end

  def self.rad(n)
    value = 1
    Prime.prime_division(n).each{ |e| value *= e.first }
    value
  end
end

start = Time.now
p Problem124.find_ans
p Time.now - start
```

## Efficiency

O(n^(3/2))
