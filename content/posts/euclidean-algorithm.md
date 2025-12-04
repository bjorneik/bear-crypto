---
title: "Extended Euclidean Algorithm and Modular Inverse"
date: 2024-12-04
categories: ["Mathematics Foundations"]
tags: ["extended euclidean algorithm", "modular inverse", "greatest common divisor", "number theory", "foundations"]
math: true
draft: false
---


## Introduction

The next topic we will cover in mathematics foundations is the Extended Euclidean Algorithm (EEA) and modular inverse. In the topic *Introduction to Modular Arithmetic* we discussed that division is tricky in modular arithmetic. Today we are going to tackle this problem and see how division works and when we can use it. But first, we need to talk about greatest common divisor and the Euclidean Algorithm. So let's take this step-by-step.

## Greatest Common Divisor

The greatest common divisor (GCD) is something we encounter quite early when we start studying mathematics. It's a simple concept: the gcd between two integers is the largest number that divides both integers. Let's see some examples:

The gcd between 6 and 8, $gcd(6,8)$, is 2. That is quite simple and straightforward. 

For some integers we can factorize them. Every integer can be written as a product of prime numbers. But what is a prime number? By definition a prime number is a number larger than 1 that is only divisible by 1 and itself:

$ p \text{ is prime if and only if } p > 1 \text{ and } (a \mid p \implies a \in \{1, p\}) $

Here are some prime numbers: $ \{2, 3, 5, 7, 11, 13, 17, 19, 23, 29, \ldots\} $

As mentioned, when we factorize an integer we write it as the product of prime numbers:

$ 6 = 2 \times 3$

$ 28 = 2 \times 2 \times 7 = 2^2 \times 7 $

If the $gcd(a,b) > 1$ then $gcd(a,b)$ will be the highest common factor when we factorize $a$ and $b$. What is the $gcd(55,121)$?

$ 55 = 5 \times 11 $

$ 121 = 11^2 $

Therefore $gcd(55,121) = 11$

Now, what is $gcd(270, 192)$? We can for sure factorize it, but there is an algorithm that makes finding the $gcd$ much quicker than factorizations (also, remember, factorizing extremely large numbers is a very hard task!).

## The Euclidean Algorithm

The Euclidean Algorithm is an algorithm that allows us to find the $gcd$ between two integers in a quick way! The best way to explain it is with an example, so let's dive in and use EA to find $gcd(270, 192)$

<div style="text-align: center; margin: 2rem 0;">
  <iframe src="/animations/euclidean_algorithm.html" 
          style="border: none; display: block;">
  </iframe>
</div>

As you can see in the animation above, the algorithm repeatedly divides and takes remainders until it reaches the remainder zero. Let's walk through the algorithm.

The first step is to write the biggest integer as a product of the smallest plus a remainder. 

Step 1: $ 270 = 192 \times 1 + 78 $

Then we write the smallest as a product of the remainder plus a new remainder.

Step 2: $ 192 = 78 \times 2 + 36 $

We proceed with the algorithm until we reach a remainder $0$.

Step 3: $ 78 = 36 \times 2 + 6 $

Step 4: $ 36 = 6 \times 6 + 0 $

When we reach a remainder $0$ the remainder of the previous step is the $gcd$! A quick tip: whenever you reach a remainder $1$ in the algorithm, $1$ is the $gcd$ and you don't need to proceed (there will be only one more step where the remainder will be $0$). Let's do one more example to reinforce the algorithm. We will find $gcd(1234,5678)$.

Step 1: $ 5678 = 1234 \times 4 + 742 $

Step 2: $ 1234 = 742 \times 1 + 492 $

Step 3: $ 742 = 492 \times 1 + 250 $

Step 4: $ 492 = 250 \times 1 + 242 $

Step 5: $ 250 = 242 \times 1 + 8 $

Step 6: $ 242 = 8 \times 30 + 2 $

Step 7: $ 8 = 2 \times 4 + 0 $

$ gcd(1234,5678) = 2 $

Now you know how to compute the $gcd$ of any two integers! This will be crucial in several cryptosystems we will study! There's one very important term you should be familiar with that involve the $gcd$. Whenever the $gcd(a,b) = 1$ we say that $a$ and $b$ are *relative primes* or *coprimes*, this is because they don't share any prime numbers in their factorization! Now that you know how to use the EA, we can use it to find more things!

## The Extended Euclidean Algorithm and Bézout Coefficients

We have seen that $gcd(270, 192) = 6$ we can write 6 as linear combination of 270 and 192. In other words $ \exists x, y : 6 = 270 \times x + 192 \times y $. This linear combination is called Bézout's identity (you don't need to remember the name, but what it is!) and the Bézout coefficients are $x$ and $y$ (again, not important to remember that $x$ and $y$ are called Bézout coefficients). We can easily find the Bézout coefficients using the Euclidean Algorithm! We need to work backwards to find $x$ and $y$. I have seen many people confused about this, and I was too when I first had to do this. I had a mathematics professor in middle school that once told us "Everything is difficult until you learn how to do it". When working backwards the Euclidean Algorithm you need to have in mind your goal: write a linear combination of the two integers. We start with the line where we have the $gcd$ as a remainder (that's Step 3 for us), but we rearrange it to isolate the remainder (remember: Bézout's identity is $gcd(a,b) = a \times x + b \times y $)

Step 1: $ 6 = 78 - 2 \times 36 $

Now what we need to do is to use the step before that (Step 2) to rewrite the way we have written $6$. And the secret here is, we're always going to replace what is the remainder in the step before. For example, in Step 2 of EA the remainder is 36, so in our new algorithm we are going to replace 36 by $ 192 - 2 \times 78 $.

Step 2: $ 6 = 78 - 2 \times (192 - 2 \times 78) $

$ 6 = 78 - 2 \times 192 + 4 \times 78 $

$ 6 = 5 \times 78 - 2 \times 192 $

Here's where people start to get confused. I've seen many people now substituting 192! But remember our goal, we want to write 6 as a linear combination of 192 and 270! So we shouldn't get rid of 192! In fact the moment we encounter the integers whose $gcd$ we found, they will always stay! When in doubt, check the remainder in the previous step and you'll know which one you should replace next! In our case it's 78, which will be replaced by $ 270 - 1 \times 192 $ (or simply $ 270 - 192 $).

Step 3: $ 6 = 5 \times (270 - 192) - 2 \times 192 $

$ 6 = 5 \times 270 - 5 \times 192 - 2 \times 192 $

$ 6 = 5 \times 270 - 7 \times 192 $

There! We have an expression for 6 that is a linear combination of 270 and 192. You can always double check the expression to see if it's correct! Indeed $ 5 \times 270 - 7 \times 192 $ is $6$! We have then found Bézout coefficients they are $5$ and $-7$! And the algorithm we used to find them is the Extended Euclidean Algorithm! For practice's sake we can find Bézout coefficients for the identity $gcd(1234,5678) = 1234 \times x + 5678 \times y$ 

Step 1: $ 2 = 242 - 30 \times 8 $

Step 2: $ 2 = 242 - 30 \times (250 - 242) $

$ 2 = 242 - 30 \times 250 + 30 \times 242 $

$ 2 = 31 \times 242 - 30 \times 250 $

Step 3: $ 2 = 31 \times (492 - 250) - 30 \times 250 $

$ 2 = 31 \times 492 - 31 \times 250 - 30 \times 250 $

$ 2 = 31 \times 492 - 61 \times 250 $

Step 4: $ 2 = 31 \times 492 - 61 \times (742 - 492) $

$ 2 = 31 \times 492 - 61 \times 742 + 61 \times 492 $

$ 2 = 92 \times 492 - 61 \times 742 $

Step 5: $ 2 = 92 \times (1234 - 742) - 61 \times 742 $

$ 2 = 92 \times 1234 - 92 \times 742 - 61 \times 742 $

$ 2 = 92 \times 1234 - 153 \times 742 $

Step 6: $ 2 = 92 \times 1234 - 153 \times (5678 - 4 \times 1234) $

$ 2 = 92 \times 1234 - 153 \times 5678 + 612 \times 1234 $

$ 2 = 704 \times 1234 - 153 \times 5678 $

So $x = 704$ and $y = -153$

## Modular Inverse

We have established that division in modular arithmetic is not as trivial as in regular arithmetic. Usually when we want to divide both sides of an equation by a number, we're trying to eliminate that number and isolate our variable. Let's say we have the equation $ 3x = 9 $. If we divide both sides by 3 we then get $ x = 3 $ and we eliminate the 3 in the left side, correct? Not quite! What we did was transform 3 into 1 because $ 3 \div 3 = 1 $. Now if we have $ 3x \equiv 9 \pmod{13} $ we have said that we can't simply divide both sides by 3, like we just did in the regular arithmetic example. However, there is something we can do to transform the 3 multiplying $x$ into 1. In regular arithmetic we multiply by the inverse of the number (dividing by 3 is the same as multiplying by $ \frac{1}{3}$). We just need to find what is the inverse of $3 \pmod{13}$. Let's think modularly (if that's even a word!). We need to find an integer that when we multiply it by 3 will equal 1, correct? Almost. When we work with modular arithmetic we don't usually use equal, $=$, that's because of the nature of modular arithmetic, it's a cycle, with no beginning or end. Unless we are working with some sort of constraint, if a solution exists there will be infinitely many solutions. We need to find an integer that when we multiply by 3 will be **congruent** to $1 \pmod{13}$! Mathematically we can write:

Let $a \in \mathbb{Z}$. If $a \times a^{-1} \equiv 1 \pmod{n}$, we say that $a^{-1}$ is the modular inverse of $a$ modulo $n$.

We are almost done defining modular inverse (sometimes also called multiplicative inverse), there is only one very crucial point to be discussed. Not all integers have a modular inverse. Instead of just giving the condition, let's work together to find it. Let's assume that an integer $a$ **has** a modular inverse $\pmod{n}$. Then

$a \times a^{-1} \equiv 1 \pmod{n}$

Let's recall the definition of congruence

$aa^{-1} - 1 \equiv 0 \pmod{n}$

This means that $n$ divides $aa^{-1} -1$. So there exists an integer $k$ that satisfies the equation

$aa^{-1} - 1 = kn, k \in \mathbb{Z}$

Let's now do some rearranging and isolate $1$

$aa^{-1} - kn = 1$

Does this look familiar? If you thought of Bézout's identity you are absolutely correct! But in order for this equation to be a Bézout's identity we need to check if $gcd(a,n) = 1$, and there it is, that's our condition! As long as $a$ and $n$ are coprimes (or relative primes) $a$ will have a modular inverse $\pmod{n}$. Let's go back to the example $3x \equiv 9 \pmod{13}$. The first thing we need to ask is if 3 and 13 are coprimes. In this case the answer is very straightforward since 3 and 13 are primes and thus share no factors. So we know for a fact that $gcd(3,13) = 1$. Now to find what the modular inverse is we need to use the Extended Euclidean Algorithm, so let's do it!

Step 1: $ 13 = 3 \times 4 + 1$

As I mentioned in the section before whenever we encounter the remainder 1 we don't need to proceed any further (you can do step 2 if you want and see that the remainder will be 0).

Now we just need to rearrange and isolate $1$

$1 = 13 - 4 \times 3$

We have now found our coefficients! If we write $1 = 13x + 3y$ we can assign $x = 1$ and $y = -4$. You can totally work with $y = -4$ but, as I mentioned, it's common to work with the smallest non-negative residue: $-4 \equiv 9 \pmod{13}$, so the modular inverse of $3 \pmod{13}$ is $9$. Now we can proceed and multiply both sides of the congruence by $9$

$3 \times 9 \times x \equiv 9 \times 9 \pmod{13}$

We now know that $3 \times 9 \equiv 1 \pmod{13}$. When we talked about equivalence classes in *Introduction to Modular Arithmetic* we said that in modular arithmetic we can always replace any integer by one another in the same equivalence class. $27$ and $1$ are in the same equivalence class. You can always do this! 

$ x \equiv 81 \pmod{13}$

We already found the solution, or better said the solutions, for $x$! However let's make things better by reducing $81$ to the smallest non-negative residue $\pmod{13}$.

$ 81 \equiv 3 \pmod{13}$

So we can now write that the solution for $3x \equiv 9 \pmod{13}$ is $x \equiv 3 \pmod{13}$. Note that this solution is not one unique solution, but infinitely many solutions! Any number that is in the same equivalence class as $3 \pmod{13}$ is a solution for $3x \equiv 9 \pmod{13}$! 

We can do one more example to solidify everything we learned so far! Let's solve the following equation $148x - 71 \equiv 101 \pmod{475}$

We can rewrite the congruence by adding 71 to both sides

$148x - 71 + 71 \equiv 101 + 71 \pmod{475}$

$148x \equiv 172 \pmod{475}$

Now we check if $gcd(148,475) = 1$ so we know that there exists a modular inverse of $148 \pmod{475}$

$475 = 148 \times 3 + 31$

$148 = 31 \times 4 + 24$

$31 = 24 \times 1 + 7$

$24 = 7 \times 3 + 3$

$7 = 3 \times 2 + 1$

Yes! $gcd(148,475) = 1$ so this means that the modular inverse exists! Since we already did the Euclidean Algorithm we can just use its extended version to find what the modular inverse.

$1 = 7 - 2 \times 3$

$1 = 7 - 2 \times (24 - 3 \times 7)$

$1 = 7 - 2 \times 24 + 6 \times 7$

$1 = 7 \times 7 - 2 \times 24$

$1 = 7 \times (31 - 24) - 2 \times 24$

$1 = 7 \times 31 - 7 \times 24 - 2 \times 24$

$1 = 7 \times 31 - 9 \times 24$

$1 = 7 \times 31 - 9 \times (148 - 4 \times 31)$

$1 = 7 \times 31 - 9 \times 148 + 36 \times 31$

$1 = 43 \times 31 - 9 \times 148$

$1 = 43 \times (475 - 3 \times 148) - 9 \times 148$

$1 = 43 \times 475 - 129 \times 148 - 9 \times 148$

$1 = 43 \times 475 - 138 \times 148$

So the modular inverse of $148 \pmod{475}$ is $-138 \equiv 337 \pmod{475}$. We can now multiply both sides by 337.

$148 \times 337 \times x \equiv 172 \times 337 \pmod{475}$

$x \equiv 57964 \pmod{475}$

$x \equiv 14 \pmod{475}$

Since we are introducing many things I have decided to do the calculations step-by-step. In the future when we apply this knowledge I won't be doing all these calculations (to save us time and space).

## Where is this used?

The Euclidean Algorithm, its extended version, modular inverse and the Bézout's identity are used more frequently than you think in cryptography! They are key concepts that once we start using often they will seem very trivial (it did for me!). The algorithm works exactly the same at all times! Whether to find the $gcd$ of two integers, find a modular inverse, they never change! So save these concepts and in the beginning, whenever you encounter an EEA, do it yourself to start getting confidence and becoming familiar with it! Practice is key in mathematics! We have the knowledge to study some cryptosystems now! We will come back to learning some more mathematical fundamentals whenever they are required! 

Thanks for sticking around! I hope you had fun and learned something!