# Elliptic Curve Cryptography

ECC uses discrete logarithms of elliptic curves to provide its one way function. The ElGamal cryptosystem relies on the difficulty of the discrete log problem which is:
Given xa = b mod p find log_x(b) = a mod p, that is, if we have b, x, and p, can we retrieve a? It turns out this this problem is intractable for sufficiently large values of p. These intractable problems are the basis of all public key cryptography (for RSA the integer factorization problem is the "hard problem").

The ElGamal cryptosystem uses the discrete log problem as its basis. The public key is comprised of (p, x, b) and the private key is a. We also pick a random value k mod p for each message transmission.
Our encrypt function returns a tuple and is defined as:
e_K(x, k) = (y_1, y_2)
where y_1 = xk mod p
and y_2 = x*(bk) mod p
Now we define our decrypt function (which takes a tuple) as: d_K(y_1, y_2) = y_2 * (y_1a)-1 mod p
As you can see, for someone to break this encryption they'd have to solve the discrete log problem.

# ELGAMAL OVERVIEW (OVER ELLIPTIC CURVE)

Now I will draw a parallel between the discrete log problem on the finite Integers and our defined addition operator on points on finite elliptic curves. The discrete log is a function that tells us what power a number was raised to in order to obtain a larger number. Raising a number to a power is just repeated multiplication. The addition analog of this is just multiplication, repeated addition of a point. Define ElGamal on an elliptic curve by replacing multiplication with addition, and exponentiation with multiplication:

The restated discrete log problem is:

Given x * a = b mod p find log_x(b) = a mod p, that is, if we have b, x, and p, can we retrieve a? Where b and a are points on the elliptic curve E.
Our encrypt function returns a tuple and is defined as: 
e_K(x, k) = (y_1, y_2)
where y_1 = x * k mod p
and y_2 = x + (b * k) mod p
Now we define our decrypt function (which takes a tuple) as: d_K(y_1, y_2) = y_2 + (y_1 * a)-1 mod p
Since y_1 * a = x * k * a = b * k we see that d_K reduces to d_K = x + (b * k) + (b * k)-1 = x

This would be easy to reverse if we were operating on a finite group of integers, but since it’s over the points of an elliptic curve, we cannot reverse the operation of repeatedly adding a point to itself.

 # ADVANTAGES AND DISADVANTAGES
There are several procedures out there to cryptanalyze messages using the ElGamal cryptosystem and other discrete log based cryptosystems. In particular, the ElGamal cryptosystem when used on the integers is vulnerable (for small numbers) to an attack called the Index Calculus. When implemented over an elliptic curve, the ElGamal cryptosystem is not vulnerable to Index Calculus attacks, the technique simply does not work.

There are also several fast algorithms for factoring integers that are forcing RSA users to increase the number of bits used. According to an NSA site (listed in citations), 1024 bit RSA is equivalent to 160 bit Elliptic Curve crypto (although they don't specify an algorithm...), equivalent being the amount of security needed to transmit an 80-bit key for AES encryption. So elliptic curves can reduce "cost" there. 

ECC features smaller keys, ciphertexts and signatures, and generates these items relatively fast compared to other methods. The disadvantages of ECC are that it is complex to implement securely. Signing with a broken random number generator compromises the key. Also, 

# IMPLEMENTATION IN C++
I used the provided C++ code to generate the ECC public keys.
