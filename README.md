# Cipher - Message masking with matrices

[![Build Status](https://travis-ci.org/mrlizzard/103cipher_2017.svg?branch=master)](https://travis-ci.org/mrlizzard/103cipher_2017)
[![codecov](https://codecov.io/gh/mrlizzard/103cipher_2017/branch/master/graph/badge.svg)](https://codecov.io/gh/mrlizzard/103cipher_2017)

- **Binary name:** 103cipher
- **Repository name:** 103cipher_2017
- **Repository rigths:** ramassage-tek
- **Language:** C, C++, perl 5, python 3 (>= 3.5), ruby 2 (>= 2.2), php 5.6, bash 4
- **Choosed language:** C
- **Compilation:** via Makefile, including re, clean and fclean rules


# Subject

_Cryptography_ is a very old science, whose goal is to secure communication, so that only its recipient could read it.

There are a lot of methods to encrypt a message, from the simplest (like the 2000-year-old Cesar’s code) to the most complex (like the World War 2 Enigma code) ; they all need both encryption and decryption keys (sometimes identical).
In some cases (such as the Hill cipher), the key is represented by a matrix.

You have to carry out such a matrix-based ciphering software, using the following process to encrypt :
1. transcript the key into numbers using the ASCII table,
2. convert the numbered key into a square matrix, the smallest possible size, and filling the lines first,
3. transcript the clear message into numbers using the ASCII table,
4. convert the numbered message into a matrix ; its number of columns should fit the key matrix size, and its number of lines should be as small as possible,
5. multiply the 2 matrices, and write the answer linearly to get the encrypted message.

> :bulb: During the conversion into matrices, zeros can be added at the end of the message or the key to fit the proper matrix size

The decryption process logically follows from the previous encryption method, using the same key (be careful ! you need to inverse the key matrix, which is not always possible).

> :exclamation: 2-dimension and 3-dimension matrices invertions are rather easy, but inverting bigger matrices is a difficult problem ; it would be considered as a bonus point if you can do that !

## Usage

```
~/B-MAT-100> ./103cipher message key flag
```

- **message:** a message, made of only ASCII characters
- **key:** the encryption key, made of only ASCII characters
- **flag:** 0 for the message to be encrypted, 1 to be decrypted

> :exclamation: The use of library including matrix calculus (such as numpy) is prohibited !

## Bonus

- cryptanalysis of the code, to find the original message without the key
- refining the encryption process

## Examples

```
∼/B-MAT-100> ./103cipher "Just because I don't care doesn't mean I don't understand." "Homer S" 0
Key matrix :
72         111        109
101        114        32
83         0          0

Encrypted message :
26690 21552 11810 19718 16524 13668 25322 22497 14177 28422 26097 16433 12333 11874
5824 27541 23754 14452 17180 17553 7963 26387 22047 13895 18804 14859 12033 27738
23835 15331 21487 16656 13238 21696 15978 6976 20750 23307 14093 16788 11751 8981
22339 24861 15619 21295 16524 13668 26403 23610 15190 29451 25764 16106 26394 23307
14093 3312 5106 5014
```

<img align="right" src="/doc/HomerS-3x3-matrix.gif" alt="" />
<br />

Indeed, "Homer S", transcripted into numbers using the ASCII table, gives the following 3-3-matrix :<br />

Using the ASCII table, the clear message becomes :

```
74 117 115 116 32 98 101 99 97 117 115 101 32 73 32 100 111 110 39 116 32 99 97 114 101 32 100 111 101 115 110 39 116 32 109 101 97 110 32 73 32 100 111 110 39 116 32 117 110 100 101 114 115 116 97 110 100 46
```

<img align="right" src="/doc/HomerS-5x3-matrix1.gif" alt="" />
<br /><br />

Written as a 3-column-matrix :

<img align="right" src="/doc/HomerS-5x3-matrix2.gif" alt="" />
<br /><br />

The product of these matrices is this, which gives the encrypted message. <br /><br /><br />


```
∼
/B-MAT-100> ./103cipher "26690 21552 11810 19718 16524 13668 25322 22497 14177 28422 26097 16433 12333 11874 5824 27541 23754 14452 17180 17553 7963 26387 22047 13895 18804 14859 12033 27738 23835 15331 21487 16656 13238 21696 15978 6976 20750 23307 14093 16788 11751 8981 22339 24861 15619 21295 16524 13668 26403 23610 15190 29451 25764 16106 26394 23307 14093 3312 5106 5014" "Homer S" 1
Key matrix :
0.0        0.0        0.012
-0.004     0.012      -0.012
0.013      -0.013     0.004

Decrypted message :
Just because I don't care doesn't mean I don't understand.
```

> :bulb: Elements of the key matrix are separated by tabulations in the final output 

> :bulb: For decryption, key matrix is given as an indication, but will not be tested ; do not bother having the exact same outuput !