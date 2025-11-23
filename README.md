# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC

## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```python
# Simple ECC Example (BEGINNER FRIENDLY)

# Curve: y^2 = x^3 + 2x + 3 (mod 97)
p = 97
a = 2
b = 3

# Point addition
def point_add(P, Q):
    if P == None:
        return Q
    if Q == None:
        return P

    if P[0] == Q[0] and P[1] != Q[1]:
        return None  # point at infinity

    if P == Q:
        # slope = (3x^2 + a) / (2y)
        s = ((3 * P[0] * P[0] + a) * pow(2 * P[1], -1, p)) % p
    else:
        # slope = (y2 - y1) / (x2 - x1)
        s = ((Q[1] - P[1]) * pow(Q[0] - P[0], -1, p)) % p

    xr = (s * s - P[0] - Q[0]) % p
    yr = (s * (P[0] - xr) - P[1]) % p
    return (xr, yr)

# Scalar multiplication: k * P
def mul(k, P):
    R = None
    for i in range(k):
        R = point_add(R, P)
    return R

# Base point
G = (3, 6)

# Private key
priv = 5

# Public key
pub = mul(priv, G)

print("Curve: y^2 = x^3 + 2x + 3 (mod 97)")
print("Base point G =", G)
print("Private Key =", priv)
print("Public Key =", pub)
```
## Output:
<img width="465" height="277" alt="image" src="https://github.com/user-attachments/assets/ab309f47-16d3-4db4-ba2b-ee4a4aaeba25" />

## Result:
The program is executed successfully

