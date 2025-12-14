---
title: "The Shift Cipher"
date: 2024-12-12
categories: ["Classical Ciphers"]
tags: ["shift cipher", "caesar cipher", "substitution cipher", "classical cryptography", "encryption"]
math: true
draft: false
---


## Introduction

In this post we will cover the shift cipher. Although it's not the first known cryptographic method, it's one that is very well documented and a great entry point to cryptography. This method makes use of modular arithmetic, so we will be able to put to use the knowledge we have so far. If you are not familiarized with modular arithmetic, I strongly recommend reading the post *Introduction to Modular Arithmetic* before proceeding. 

The exact date where this method was created is unknown, however there's a very famous historical figure who is known to have used this cryptographic method: Julius Caesar! The shift cipher works by **shifting** the letters in a message by a certain value. In order to understand it a little better, let's lay down some conventions we are gonna use throughout all cryptosystems we will cover here.


## Doing math with letters

We are going to be using math to encrypt/decrypt messages. To make it easier to do math with letters, we will be transforming letters into numbers. Whenever we need to that, we are going to replace each letter by an associated number. Since the language we are using to communicate is English, we will be using the English alphabet. The letter-number conversion will be done as follows:

![Alphabet to Numbers Mapping](/images/alphabet_numbers.png)

As you can see, the letter **a** is converted to the number **0**, **b** is converted to **1**, and so on until the letter **z**, which is converted to **25**. But why do we start at **0** and not at **1**? Because of modular arithmetic! And why from **0** to **25**? Because the English alphabet has 26 letters, so we will be working modulo 26, and the numbers **0-25** are the residues when we work modulo 26. 

Another convention we will be use is writing plaintext, which is the non-encrypted message, in **lowercase**, whilst the ciphertext, which is the encrypted message, in **uppercase**. This will make it easier to know when we are dealing with an encrypted message or not. The last thing is that when encrypting a message we conventionally ignore spaces and punctuations. We are now ready to dive into how we encrypt using the shift cipher.


## Encryption

As mentioned, when using the shift cipher we encrypt the message by shifting each letter by a specific value, that we will call **key**. 

$ x \mapsto x + k \pmod{26} $ where $x$ is the letter we are encrypting and $k$ is the key in which we're shifting.

In theory the key can assume any value between $0$ and $25$ inclusive, however if we pick the key $k = 0$ we are not really encrypting the message, as the outcome will be exactly as the input! The reason why the keys can only assume values from $0$ to $25$ is because we are working modulo 26, so any value higher than $26$ would fall into one of the equivalence classes and would yield the same result as any other number in the same class.

Julius Caesar used $k = 3$ whenever he needed to encrypt military-related messages. Let's pretend we are Julius Caesar and we are sending a message to an ally. We need to send *weneedhelp*. The first thing we need to do is convert the letters into numbers.

![Converting "weneedhelp" to numbers](/images/weneedhelp_numbers.png)

Now we can encrypt the message. Let's do it one by one.

$ 22 + 3 \equiv 25 \pmod{26} $

$ 4 + 3 \equiv 7 \pmod{26} $

$ 13 + 3 \equiv 16 \pmod{26} $

$ 4 + 3 \equiv 7 \pmod{26} $

$ 4 + 3 \equiv 7 \pmod{26} $

$ 3 + 3 \equiv 6 \pmod{26} $

$ 7 + 3 \equiv 10 \pmod{26} $

$ 4 + 3 \equiv 7 \pmod{26} $

$ 11 + 3 \equiv 14 \pmod{26} $

$ 15 + 3 \equiv 18 \pmod{26} $

We now convert the numbers back to letters.

![Converting encrypted numbers to ciphertext letters](/images/ciphertext_numbers_to_letters.png)

So **weneedhelp** is encrypted to **ZHQHHGKHOS** using shift cipher with key $k = 3$.

The encryption is pretty simple, right? Before we move on to decryption, let's encrypt another message using shift cipher, this time with a key $k = 17$. We will encrypt the message **modulararithmetic**.

$ 12 + 17 \equiv 29 \equiv 3 \pmod{26} \mapsto D  $

$ 14 + 17 \equiv 31 \equiv 5 \pmod{26} \mapsto F $

$ 3 + 17 \equiv 20 \pmod{26} \mapsto U $

$ 20 + 17 \equiv 37 \equiv 11 \pmod{26} \mapsto L $

$ 11 + 17 \equiv 28 \equiv 2 \pmod{26} \mapsto C $

$ 0 + 17 \equiv 17 \pmod{26} \mapsto R $

$ 17 + 17 \equiv 34 \equiv 8 \pmod{26} \mapsto I $

$ 0 + 17 \equiv 17 \pmod{26} \mapsto R $

$ 17 + 17 \equiv 34 \equiv 8 \pmod{26} \mapsto I $

$ 8 + 17 \equiv 25 \pmod{26} \mapsto Z $

$ 19 + 17 \equiv 36 \equiv 10 \pmod{26} \mapsto K $

$ 7 + 17 \equiv 24 \pmod{26} \mapsto Y $

$ 12 + 17 \equiv 29 \equiv 3 \pmod{26} \mapsto D $

$ 4 + 17 \equiv 21 \pmod{26} \mapsto V $

$ 19 + 17 \equiv 36 \equiv 10 \pmod{26} \mapsto K $

$ 8 + 17 \equiv 25 \pmod{26} \mapsto Z $

$ 2 + 17 \equiv 19 \pmod{26} \mapsto T $

So **modulararithmetic** is encrypted to **DFULCRIRIZKYDVKZT** using shift cipher with key $k = 17$. Let's move on to decryption!

## Decryption

The decryption of a message encrypted by a shift cipher is very simple, we just need to shift back the letters using the exact same key used to encrypt the message. Instead of *adding* the key, we *subtract* it.

$ y \mapsto y - k \pmod{26} $

Let's work out an example. The ciphertext *CUGUWLSJNIALUJBYL* was encrypted using shift cipher with key $k = 20$. What was the original message?

$ 2 - 20 \equiv -18 \equiv 8 \pmod{26} \mapsto i  $

$ 20 - 20 \equiv 0 \pmod{26} \mapsto a  $

$ 6 - 20 \equiv -14 \equiv 12 \pmod{26} \mapsto m  $

$ 20 - 20 \equiv 0 \pmod{26} \mapsto a  $

$ 22 - 20 \equiv 2 \pmod{26} \mapsto c  $

$ 11 - 20 \equiv -9 \equiv 17 \pmod{26} \mapsto r  $

$ 18 - 20 \equiv -2 \equiv 24 \pmod{26} \mapsto y  $

$ 9 - 20 \equiv -11 \equiv 15 \pmod{26} \mapsto p  $

$ 13 - 20 \equiv -7 \equiv 19 \pmod{26} \mapsto t  $

$ 8 - 20 \equiv -12 \equiv 14 \pmod{26} \mapsto o  $

$ 0 - 20 \equiv -20 \equiv 6 \pmod{26} \mapsto g  $

$ 11 - 20 \equiv -9 \equiv 17 \pmod{26} \mapsto r  $

$ 20 - 20 \equiv 0 \pmod{26} \mapsto a  $

$ 9 - 20 \equiv -11 \equiv 15 \pmod{26} \mapsto p  $

$ 1 - 20 \equiv -19 \equiv 7 \pmod{26} \mapsto h  $

$ 24 - 20 \equiv 4 \pmod{26} \mapsto e  $

$ 11 - 20 \equiv -9 \equiv 17 \pmod{26} \mapsto r  $

The orignial message, plaintext, was *iamacryptographer*.

## Vulnerabilities

Despite being used for over 2000 years, the shift cipher has several vulnerabilities and with the advances in mathematics it's no longer a valid cipher method. A simple way to break the encryption is by **brute force**, i.e., testing all possible keys one by one. Since only 26 keys are possible (or really 25, since $k=0$ does nothing), trying all of them on a small section of the ciphertext would suffice to figure out which key was used to encrypt the message. 

Another way to break this type of cryptosystem is by making use of statistical analysis. For example, in the English language the letter *e* is the most frequently appearing letter in words. If we have a significant portion of ciphertext, we could perform a frequency analysis and the most frequent letter would probably correspond to *e*. A simple search would then be enough to break the encryption.

The shift cipher teaches us an important lesson: **security through obscurity doesn't work**. A cryptosystem needs to be secure even if the method is known—security should rely on the key, not on keeping the algorithm secret. With only 25 possible keys, the shift cipher fails this test.

## Modern Usage

While the shift cipher is no longer secure for serious encryption, it still has some uses today. **ROT13** (rotate by 13) is a shift cipher with $k = 13$ commonly used on internet forums and discussion boards to hide spoilers, punchlines, or potentially offensive content. ROT13 has an interesting property: since $13 + 13 = 26 \equiv 0 \pmod{26}$, applying ROT13 twice returns the original message. In other words, encryption and decryption use the same operation!

Thank you for sticking around and I hope you learned something!