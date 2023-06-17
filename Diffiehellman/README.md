# DiffieHellman

In this challenge we are given a personal implementation of the DiffieHellman key exchange.

```
p = getPrime(1024)
a = randbelow(p)
b = randbelow(p)
s = randbelow(p)

#private_key
na = randbelow(p)
nb = randbelow(p)

def f(z):
    return (a * z + b) % p

def compose_f(z , n):
    for _ in range(n):
        z = f(z)
    return z

#public_key
A = compose_f(s, na)
B = compose_f(s, nb)

shared_secret = compose_f(A, nb)
assert compose_f(B, na) == shared_secret

m = bytes_to_long(flag)
hint = (shared_secret * m) % p

```

Our goal is either to fin na or nb given A and B or to find the shared_secret given A and B.

The compose_f function compute : 

$$ f(z,n) = a^{n}z + \sum_{i=0}^{n-1} ba^{i} \mod p $$

and the shared_secret secret is equal to : 

$$ f(A,nb) = a^{nb}z + \sum_{i=0}^{nb-1} ba^{i} \mod p $$

We see that we can fin the shared_secret by using A and B, here is how  : 

![Alt text](img/resolve.jpg?raw=true "Solving")
