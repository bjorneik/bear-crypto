---
title: "Introduction to Modular Arithmetic"
date: 2024-12-03
categories: ["Mathematics Foundations"]
tags: ["modular arithmetic", "number theory", "foundations"]
math: true
draft: false
---


## Introduction

The best way to introduce the concept of modular arithmetic is with the clock analogy. We know a day has 24 hours (on Earth!). If now is 10:00 and someone says "Let's meet in 30 hours" you don't write down "Meeting at 40:00", you would write down "Meeting at 16:00". You just performed a modular arithmetic calculation! The easiest way I found to understand the concept of modular arithmetic was associating it with cycles. Anything we count in cycles (hours, days, weeks, and so on) is done using modular arithmetic! Modular arithmetic is used in many different cryptosystems, including modern ones still in use! We will move now to the formal definition that forms the basis of modular arithmetic.

## Formal Definition

In mathematics, we write $a \equiv b \pmod{n}$ and say "$a$ is congruent to $b$ modulo $n$" when $n$ divides $(a-b)$. We can also write as $n \mid (a-b)$. When we write $x \pmod{y}$, we mean the remainder $z$ when $x$ is divided by $y$. This remainder satisfies $x = y \times q + z \text{ where } 0 \leq z < y \text{ and } x, y, z, q \in \mathbb{Z}$.

Examples:

$ 4 \equiv 30 \pmod{13}$ 

$ 65 \equiv 209 \pmod{12}$

The definition of congruence is very important and used in several proofs in mathematics.


## Operations

We will now briefly cover some operations in modular arithmetic, starting with addition.

### Addition

Let $ a, b, n \in \mathbb{Z} $

$(a + b) \pmod{n} = ((a \pmod{n} + b \pmod{n})) \pmod{n} $

It's very important that we don't forget the final modulos! 

$(a + b) \pmod{n} \neq a \pmod{n} + b \pmod{n} $

We can see this better with an example! Let's say we want to calculate $ (8 + 9) \pmod{5} $.

This is a short and easy computation that we can directly compute:

 $ (8 + 9) = 17 \equiv 2 \pmod{5} $
 
  But let's apply the property we just saw above: 
  
  $ (8 + 9) \pmod{5} = (8 \pmod{5} + 9\pmod{5}) \pmod{5} = 3 + 4 \equiv 7 \equiv 2 \pmod{5} $

Now notice what happens if we don't write the final modulos:

$ (8 + 9) \pmod{5} = 8 \pmod{5} + 9 \pmod{5} = 3 + 4 = 7 $

Clearly $2 \neq 7 $! 

### Subtraction

Subtraction works exactly like addition! 

Let $ a, b, n \in \mathbb{Z} $

$(a - b) \pmod{n} = ((a \pmod{n} - b \pmod{n})) \pmod{n} $

Example: 

$ (67 - 14) \pmod{6} = (67 \pmod{6} - 14 \pmod{6}) \pmod{6} = 1 - 2 \equiv -1 \equiv 5 \pmod{6} $

It's common to express the result of a modulo $n$ operation with the smallest positive integer, which in all cases will be an integer between $0$ and $ n - 1$ (we will see why very shortly!).

### Multiplication

Multiplication works in the exact same way as addition and subtraction, let's see:

Let $ a, b, n \in \mathbb{Z} $

$(a \times b) \pmod{n} = (a \pmod{n} \times b \pmod{n}) \pmod{n} $

Example:

$ (86544 \times 73261) \pmod{9} $

The property can be even more useful in some cases. In the example above we know that $86544$ is divisible by $9$ (this can be easily checked by adding all the digits: $ 8 + 6 + 5 + 4 + 4 = 27 $ which is divisible by $9$.). This means that $ 86544 \equiv 0 \pmod{9} $. We don't even need to know $ 73261 \pmod{9} $ to know the result of $ (86544 \times 73261) \pmod{9} $.

$ (86544 \times 73261) \pmod{9} = (86544 \pmod{9}) \times (73261 \pmod{9}) \pmod{9} \equiv 0 \times (73261 \pmod{9}) \equiv 0 \pmod{9} $

### Other Operations

For now we're stopping with these three operations. As we progress with the content, we'll come back and add more to our fundamentals! For example, RSA, a cryptosystem still in use, requires modular exponentiation! 

## The Division Problem in Modular Arithmetic 

Division is one of the basic operations in regular arithmetic, however in modular arithmetic it's not as simple. First, in modular arithmetic we are dealing with integers, therefore the result of a division should be an integer as well. Let's say we have $a, b, c $ and $ n \in \mathbb{Z}$ such that $ a \times b \equiv a \times c \pmod{n}$. Can we say that $b \equiv c \pmod{n}$? In normal division, as long as $ a \neq 0 $, yes, that holds. However the same doesn't apply for modular arithmetic. We can see that with an example.

$20 \equiv 2 \pmod{6}$

That congruence is true: $20 = 6 \times 3 + 2$

What if we divide both sides by $2$? Then we have

$ 10 \equiv 1 \pmod{6} $

However, $ 10 \equiv 4 \not \equiv 1 \pmod{6} $

There is a general formula we can use for division in modular arithmetic. 

Let $a, b, c $ and $ n \in \mathbb{Z}$

If $ a \times c \equiv b \times c \pmod{n} $ then

$ a \equiv b \pmod{\frac{n}{gcd(n,c)}}$

If it happens that $gcd(c,n) = 1$ then it's as if we performed a normal division. In the example we saw above we can rewrite $ 20 \equiv 2 \pmod{6} $ as

$ 10 \times 2 \equiv 1 \times 2 \pmod{6} $

We know that $gcd(6,2) = 2$. If we apply the general formula above

$ 10 \equiv 1 \pmod{\frac{6}{gcd(6,2)}} $

$ 10 \equiv 1 \pmod{\frac{6}{2}} $

$ 10 \equiv 1 \pmod{3} $

There is another way to perform "division" in modular arithmetic that will be presented in the next post about *Extended Euclidean Algorithm and Inverse Multiplicative*.


## Equivalence classes and residues 

As I mentioned before, I like to think of modular arithmetic as a cycle, and a cycle is nothing but a repetition of patterns. A bit of philosophy: does a cycle have a beginning or end? I like to think no, and that was very useful to me when I started to grasp how modular arithmetic works. We have seen so far some properties and, most importantly, the definition of congruency. 

If we say that a certain number $x \equiv 2 \pmod{7}$ how many solutions do we have? The answer is: infinite solutions, because a cycle has no beginning nor end! Obviously $ x = 2 $ satisfies the congruency. But so does $ x = -5 $ or $x = 16 $ or even $ x = 1649706 $. If you scroll up a bit you will see the definition of congruency. To say that $x \equiv 2 \pmod{7}$ is the same to say that $ n \mid (x -2)$. This means that there exits an integer, $q$, such that when we multiply it by $7$ we get $ (x-2)$. Mathematically we write:

$ \exists  q \in \mathbb{Z} : x -2 = 7 \times q $

We can therefore write $x$ as

$ x = 7 \times q + 2 $

Notice that $x$ can be either positive or negative! 

We call the smallest non-negative integer less than the modulo a residue. When working modulo $7$ for example, we have $7$ different residues: $0, 1, 2, 3, 4, 5$ and $6$. That's because when we divide any integer by $7$ we get $ m = 7 \times q + r$ where $m$ is a random integer and $q \in \mathbb{Z}$ and $r \in \mathbb{N}$. Remember in the *Operations* section when I said it's common to represent the result as the smallest positive integer? That's because the residue is the smallest positive number that will satisfy any congruence (given that there is a solution!). Mathematically speaking it is valid to use ANY integer as long as it satisfies the congruence, but we will see in the future how using the residue simplifies things a lot (and we like that)! Why do residues range from $0$ to $n -1$? By the division algorithm, any integer $m$ can be written as $ m = nq + r \text{ where } 0 \leq r < n$. The remainder $r$ must be non-negative and strictly less than $n$, giving us exactly $n$ possible residues.

With the definition of residue, we have also implicitly defined equivalence classes! 

Before we formally define what an equivalence class is, let me show you a visual representation of modular arithmetic! We will continue working modulo $7$ (7 is my favorite number!). We already defined that the residues vary from $0$ to $6$. For any number higher than $6$ we just place them in the same category as one of the residues. For example $7$ is in the same category as $0$, $27$ in the same category as $6$ and so on. We can then build a wheel with $7$ different sectors, one for each residue, and allocate any number in one of those $7$ sectors! Here's a visual representation:

<div style="text-align: center; margin: 2rem 0;">
  <iframe src="/animations/mod7_wheel.html" width="820" height="820" frameborder="0" style="border: none; border-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);"></iframe>
</div>

As we can see all integers that satisfy $ x \equiv 0 \pmod{7} $ are in the red sector, all that satisfy $x \equiv 1 \pmod{7} $ are in the teal sector, and so on. Notice how the wheel repeates every 7 numbers - this is the cyclic nature of modular arithmetic. All numbers in the the sectors can be interchanged with one another, that's the beauty in modular arithmetic! Take a look at the wheel. Can you quickly answer what is $x \equiv 29 \times 33 \pmod{7}$? The answer is $5$ and you don't need to know how much $29 \times 33$ is! We know $29 \equiv 1 \pmod{7}$ and $33 \equiv 5 \pmod{7}$, we can then easily replace $29$ by $1$ and $33$ by $5$. Therefore $x \equiv 1 \times 5 \equiv 5 \pmod{7}$.

There are several useful properties we can take from equivalence classes, but they will not be covered here.

## Where is this used?

We are basically done with this post! Before we finish I just want to quickly mention where this is used. Modular arithmetic is the mathematical foundation of several cryptosystems, most of them not in use anymore, but as we explore the evolution of cryptosystems throughout the years we will see that nearly all initial cryptosystems used modular arithmetic. In fact, one of the cryptosystems still in use, RSA, uses modular arithmetic! We will see further that the security of cryptosystems that use modular arithmetic comes from the difficulty of factorizing large numbers. It takes a really long time for a normal computer to factor a very large number (and when I say long I mean YEARS!!). However quantum computing can easily factorize large numbers, thus posing a huge threat to cryptosystems that use modular arithmetic. This is not a problem for us for now, but we will come back to this in the future!

Before we wrap this chapter, here's a fun exercise. Let's say Froggy's birthday is on August 7th. In 2025 Froggy celebrated her birthday on a Thursday. Can we know which day of the week Froggy will celebrate her birthday in 2042 without looking at the calendar? With modular arithmetic YES! 

First we need to find out how many days will have passed between August 7th 2025 and August 7th 2042. We know regular years have 365 days and leap years 366. The next leap years are 2028, 2032, 2036 and 2040. The remaining years are regular years. 

$\text{Total days} = 4 \times 366 + 13 \times 365 = 6209  \text{ days} $

Now, how do we use modular arithmetic to find out the day of the week? We work modulo 7, since that's how the days of the week cycle!

$ 6209 \equiv 0 \pmod{7}$

In our example Thursday was the starting day. If when 6209 days have passed is congruent to 0 mod 7, that means that August 7th 2042 is also a Thursday! If we had gotten a different number we would just have to count. Any number congruent 1 would be Friday, congruent 2 Saturday and so on! See how useful (and fun) modular arithmetic is?

I hope you enjoyed reading it and that you learned something! I will see you in the next post!
