---
title: "The Affine Cipher"
date: 2024-12-18
categories: ["Classical Ciphers"]
tags: ["affine cipher", "substitution cipher", "classical cryptography", "modular inverse", "encryption"]
math: true
draft: false
---


## Introduction

We will now tackle another encryption method called affine cipher. If by reading the word affine made you think of affine functions, you are already on the right track! This method uses an affine function to encrypt messages. Differently from the shift cipher that uses only addition, the affine cipher uses also multiplication, which makes our encryption more complex. If we recall how an affine function looks like, it takes an input $x$, multiply by a coefficient, $a$, and adds to a constant, $b$.

$ f(x) = ax + b $

The affine cipher works pretty similarly, but we need to add something that is very crucial: modular arithmetic. We work modulo 26! Let's see how the encryption works.

## Encryption

Before we start encrypting, we need to convert letters into numbers, just like we did in shift cipher. The number, which is our input, is multiplied by a coefficient, here we will call it $\alpha$, add it to a value, here called $\beta$, and all this working modulo 26.

$ x \mapsto x \times \alpha + \beta \pmod{26} $

The encryption key is the pair $(\alpha,\beta)$. We have seen in the shift cipher that there were 25 valid keys. How many would there be in the affine cipher? Well, $\beta$ has no restrictions and, just like the key in affine cipher, can assume values from 0 to 25. However we need to be more careful with the valid values for $\alpha$, we are gonna see exactly why when we discuss the decryption. For now, let's encrypt the text *affine* using the key $(3,7)$ (this is a valid key!)

$ affine \mapsto 0 5 5 8 13 4 $

$ 0 \mapsto 0 \times 3 + 7 \equiv 7 \pmod{26} \mapsto H $

$ 5 \mapsto 5 \times 3 + 7 \equiv 22 \pmod{26} \mapsto W $

$ 8 \mapsto 8 \times 3 + 7 \equiv 31 \equiv 5 \pmod{26} \mapsto F $

$ 13 \mapsto 13 \times 3 + 7 \equiv 46 \equiv 20 \pmod{26} \mapsto U $

$ 4 \mapsto 4 \times 3 + 7 \equiv 19 \pmod{26} \mapsto T $

So *affine* is encrypted to *HWWFUT* using the affine cipher with key $(3,7)$.

## Decryption

Let's now work on the decryption for the affine cipher. We can work backwards to find out how exactly to decrypt. Let's say the encrypted letter is $y$, the encryption is done as follows:

$ y = x \times \alpha + \beta \pmod{26} $

We need now to find out $x$, because we are decrypting. In other words, we need to isolate x. The first step is to subtract $\beta$ from both sides.

$ y - \beta = x \times \alpha + \beta - \beta \pmod{26} $

$ y - \beta = x \times \alpha \pmod{26} $

Now in order to isolate $x$ we need to get rid of $\alpha$. How can we do that? Multiplicative inverse! Remember, what we do on one side, we have to do on the other as well! We are assuming here that there exists the multiplicative inverse of $\alpha$ modulo 26.

$ (y - \beta) \times \alpha^{-1} = x \times \alpha \times \alpha^{-1} \pmod{26} $ 

Now we know that $\alpha \times \alpha^{-1} \equiv 1 \pmod{26} $

$ (y - \beta) \times \alpha^{-1} = x \pmod{26} $

We have now found out how to decrypt an affine cipher! In the shift cipher the decryption key was essentially the same as the encryption key (just negate it). Here in the affine cipher, we need to compute the modular inverse — the decryption process is more involved. In order to decrypt we need $\beta$ and $\alpha^{-1}$, so the decryption key is $(\alpha^{-1},\beta)$.

There is one very important detail though. $\alpha^{-1}$ NEEDS to exist in order for the decryption to exist. There's only one way that $\alpha^{-1}$ exists and it is if $gcd(\alpha, 26) = 1$. In other words, $\alpha$ and $26$ have to be coprimes! This means that not all values between 0 and 25 are valid to be used for $\alpha$. Remember, two coprimes integers share no common factors. 26 is factorized into $2 \times 13$, so the integers between 0 and 25 that will be coprime with 26 will be the ones that are not multiple of 2 or 13. That means that the valid values for $\alpha$ are:

$ \{1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25\} $

We do not include 0 because that would encrypt all letters to the value of $\beta$. It's also valid to note that if $\alpha = 1$ the affine cipher becomes actually the shift cipher with key $k = \beta$.

How many possible keys are there for an affine cipher? We have 12 possible values for $\alpha$ and 26 possible values for $\beta$. The number of combinations is given by

$ 12 \times 26 = 312 $

We see an increase in the number of possible keys just by introducing one more operation to our encryption! Let's see some example now. Suppose we have the ciphertext *BFFGWFS* encrypted using the key $(7,11)$. Let's figure out what the plaintext was. The first thing to do is compute the decryption key. We need to find the multiplicative inverse of 7 modulo 26. This is the last time I will be computing the multiplicative inverse using the Extended Euclidean Algorithm in full detail—from now on, I'll just state the result!

$ 26 = 7 \times 3 + 5 $

$ 7 = 5 \times 1 + 2 $

$ 5 = 2 \times 2 + 1 $

Working backwards:

$ 1 = 5 - 2 \times 2 $

$ 1 = 5 - 2 \times (7 - 5) $

$ 1 = 5 - 2 \times 7 + 2 \times 5 $

$ 1 = 3 \times 5 - 2 \times 7 $

$ 1 = 3 \times (26 - 3 \times 7) - 2 \times 7 $

$ 1 = 3 \times 26 - 9 \times 7 - 2 \times 7 $

$ 1 = 3 \times 26 - 11 \times 7 $

So the multiplicative inverse of 7 modulo 26 is:

$ -11 \equiv 15 \pmod{26}$

Our decryption key is then $(15,11)$. We can now decrypt the message. We decrypt by computing

$ (y - 11) \times 15 \pmod{26} $

$ BFFGWFS \mapsto 1 5 5 6 22 5 18 $

$ 1 \mapsto (1 - 11) \times 15 \equiv -150 \equiv 6 \pmod{26} \mapsto g $

$ 5 \mapsto (5 - 11) \times 15 \equiv -90 \equiv 14 \pmod{26} \mapsto o $

$ 6 \mapsto (6 - 11) \times 15 \equiv -75 \equiv 3 \pmod{26} \mapsto d $

$ 22 \mapsto (22 - 11) \times 15 \equiv 165 \equiv 9 \pmod{26} \mapsto j $

$ 18 \mapsto (18 - 11) \times 15 \equiv 105 \equiv 1 \pmod{26} \mapsto b $

The plaintext was *goodjob*! 

## Vulnerabilities

The affine cipher is clearly more complex than the shift cipher. There are more possible encryption keys, the decryption is also more complex. However, for modern times affine cipher is still very vulnerable. It's still susceptible to frequency analysis, just like shift cipher, and also brute force. Even though 312 possible keys is higher than 25, a computer could easily try all the 312 keys in a small portion of the ciphertext and the encryption would be broken. Even more concerning, if an attacker knows just **two** plaintext-ciphertext letter pairs, they can completely break the cipher by solving a system of linear equations. Let's see how.

$ wp \mapsto UJ $

$ 22, 15 \mapsto 20, 9 $

$ \begin{cases}
22 \times \alpha + \beta \equiv 20 \\
15 \times \alpha + \beta \equiv 9
\end{cases} \pmod{26} $

Remember, we are still dealing with modular arithmetic! We can perform any operations we normally would do in regular arithmetic, with exception of division. It is completely allowed to use multiplicative inverses to solve this system, however it is more computing involved, as you would have to find the multiplicative inverse, and sometimes it might not even exist! My suggestion is to stick with addition, subtraction and multiplication to solve the system. In our case it's pretty simple—we can eliminate $\beta$ by subtracting the second congruence from the first.

$ 22 \times \alpha + \beta - (15 \times \alpha + \beta) \equiv 20 - 9 \pmod{26} $

$ 22 \times \alpha + \beta - 15 \times \alpha - \beta \equiv 11 \pmod{26} $

$ 7 \times \alpha \equiv 11 \pmod{26} $

We have already previously computed the multiplicative inverse of 7 modulo 26.

$ 7 \times 15 \times \alpha \equiv 11 \times 15 \pmod{26} $

$ \alpha \equiv 165 \equiv 9 \pmod{26} $

Since we know that $\alpha$ ranges from 0 to 25, in this case we have one solution for $\alpha$ and it's $9$. We can now choose any of the previous congruences to find out $\beta$.

$ 15 \times \alpha + \beta \equiv 9 \pmod{26} $

$ 15 \times 9 + \beta \equiv 9 \pmod{26} $

$ 135 + \beta \equiv 9 \pmod{26} $

$ 135 - 135 + \beta \equiv 9 - 135 \pmod{26} $

$ \beta \equiv - 126 \equiv 4 \pmod{26} $

Just like with $\alpha$, $\beta$ ranges from 0 to 25, so there's only one solution for $\beta$.

The encryption key is $(9,4)$. We could now also easily compute the decryption key, we would just need to compute the multiplicative inverse of 9 modulo 26.

You now know one more cryptographic method! In the shift and affine ciphers, we've seen that using a single key for the entire message makes them vulnerable to frequency analysis. Next time, we'll cover a method that defeats this weakness by using **different keys for different positions** in the message—the Vigenère cipher! I hope you enjoyed learning about the affine cipher and seeing how the Extended Euclidean Algorithm becomes essential for decryption!

