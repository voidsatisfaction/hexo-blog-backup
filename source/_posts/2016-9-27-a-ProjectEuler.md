---
layout: post
title: 'Project Euler 121'
categories:
  - Ruby
  - Project Euler
tags:
  - Ruby
  - Project Euler
---

## Problem

### Disc game prize fund
#### Problem 121
---
A bag contains one red disc and one blue disc. In a game of chance a player takes a disc at random and its colour is noted. After each turn the disc is returned to the bag, an extra red disc is added, and another disc is taken at random.

The player pays £1 to play and wins if they have taken more blue discs than red discs at the end of the game.

If the game is played for four turns, the probability of a player winning is exactly 11/120, and so the maximum prize fund the banker should allocate for winning in this game would be £10 before they would expect to incur a loss. Note that any payout will be a whole number of pounds and also includes the original £1 paid to play the game, so in the example given the player actually wins £9.

Find the maximum prize fund that should be allocated to a single game in which fifteen turns are played.

---

## Solution

- Get the all posibilities player lose(using combination)

- Then, get the winning rate of player for this game

- Get maximum prize

```rb
class Problem121
  def self.find_ans
    total_lose = 0
    8.upto(15) do |lose|
      total_lose += (1..15).to_a.combination(lose).to_a.map{ |e| e.reduce(:*) }.reduce(:+)
    end
    winning_rate = 1 - Rational(total_lose,factorial(16))
    prize = (1/winning_rate).floor
  end

  def self.factorial(num)
    result = 1
    num.downto(1) do |i|
      result *= i
    end
    result
  end
end

p Problem121.find_ans
```
