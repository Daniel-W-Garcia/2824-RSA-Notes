# RSA Notes

## 1. RSA Key Generation

### Public and private keys

$\text{Public key: } n = 5251,\quad e = 3$

$\text{Private key: } n = 5251,\quad d = 3403$

### Factoring $n$

$n = x \cdot y = 5251 = x \cdot y, \qquad x = 59,\quad y = 89$

$\varphi(n) = (x-1)(y-1) = (59-1)(89-1) = 5104$

$\boxed{\varphi(n) = 5104}$

To test whether $5251$ is prime, check prime divisors up to $\sqrt{5251}$:

$\sqrt{5251} \approx 72$

so the prime divisors to test are $\le 72$; $72$ is not prime.

### Divisibility tests

| Prime | Divisible? | Calculation |
|:---:|:---:|:---|
| $1$ | yes (all) | |
| $2$ | no | odd |
| $3$ | no | $5+2+5+1 = 13$, $13/3 \neq 0$ |
| $5$ | no | does not end in $5$ or $0$ |
| $7$ | no | $5251 = 7 \cdot 750 + 1$ |
| $11$ | no | $5251 = 11 \cdot 477 + 4$ |
| $13$ | no | $5251 = 13 \cdot 403 + 12$ |
| $17$ | no | $5251 = 17 \cdot 308 + 15$ |
| $19$ | no | $5251 = 19 \cdot 276 + 7$ |
| $23$ | no | $5251 = 23 \cdot 228 + 7$ |
| $29$ | no | $5251 = 29 \cdot 181 + 2$ |
| $31$ | no | $5251 = 31 \cdot 169 + 12$ |
| $37$ | no | $5251 = 37 \cdot 141 + 34$ |
| $41$ | no | $5251 = 41 \cdot 128 + 3$ |
| $43$ | no | $5251 = 43 \cdot 122 + 5$ |
| $47$ | no | $5251 = 47 \cdot 111 + 34$ |
| $53$ | no | $5251 = 53 \cdot 99 + 4$ |
| $59$ | **YES** | $5251 = 59 \cdot 89$ |

Thus

$\boxed{x = 59,\quad y = 89}$

### Calculating $d$

$d \cdot e \equiv 1 \pmod{\varphi(n)}$

$d \cdot 3 \equiv 1 \pmod{5104}$

Euclidean algorithm:

$\gcd(5104, 3) = 3 \cdot 1701 + 1$

$3 = 1 \cdot 3 + 0$

$\boxed{\gcd(5104,3) = 1}\quad \checkmark \text{ (has to be } 1\text{)}$

Back-substitution:

$5104 = 3 \cdot 1701 + 1$

$1 = 5104 - 3 \cdot 1701$

$1 = 1 \cdot 5104 + (-1701) \cdot 3$

$-1701 + 5104 = 3403$

Therefore

$\boxed{n = 5251,\quad d = 3403,\quad e = 3}$

## 2. Encryption and Decryption

$\text{Encryption} = \text{Ciphertext} = \text{Plaintext}^{\,e} \bmod n$

$C = x^e \bmod 5251$

$\text{Decryption} = \text{Plaintext} = C^d \bmod n$

$C^{3403} \bmod 5251$

$2128^{3403} \bmod 5251 = P = 87$

## 3. Computing Bezout Coefficients

$\gcd(a,b) = c$

$s \cdot a + t \cdot b = c$

Here $s,t$ are the **Bezout coefficients**. In particular, $s$ is the modular inverse of $a$.

### Euclidean algorithm example

Given

$x = 23,\quad y = 101,\quad n = 2323$

$\varphi(n) = 2200,\quad e = 13$

$\gcd(13, 2200) = 1 \quad \text{(co-prime)}$

$d \cdot 13 \equiv 1 \pmod{2200} \quad\equiv\quad 13 \cdot ? \bmod 2200 = 1$

Euclidean algorithm:

$2200 = 13 \cdot 169 + 3 \quad\equiv\quad 3 = 2200 - 13 \cdot 169$

$13 = 3 \cdot 4 + 1$

$3 = 1 \cdot 3 + 0$

We substitute this in for $3$.

### Extended Euclidean algorithm

$1 = 13 - 3 \cdot 4$

$1 = 13 - 4(2200 - 13 \cdot 169) \quad\text{(sub for } 3 \text{ from EA)}$

$1 = 13(-4 \cdot 2200) + (-4 \cdot -13 \cdot 169) \quad\text{(distribute the } -4\text{)}$

$1 = 13 - 4 \cdot 2200 + 4 \cdot 13 \cdot 169 \quad\text{(keep distributing)}$

$1 = 13 - 8800 + 8788 \quad\text{(distribution is done)}$

Since

$8788 = 13 \cdot 676,$

we get

$1 = 13 - 8800 + 13 \cdot 676$

$1 = 13 - 4 \cdot 2200 + 13 \cdot 676$

$1 = 13 + 13 \cdot 676 - 4 \cdot 2200 \quad\text{(associate)}$

$1 = 13 \cdot 677 - 4 \cdot 2200 \qquad (13 + 13 \cdot 676 = 13 \cdot 677)$

$13 \cdot 677 = 4 \cdot 2200 + 1$

$8801 = 8800 + 1 \quad \checkmark$

$\boxed{d = 677}$

Check:

$13 \cdot 677 \bmod 2200 = 1$

So $677$ is the modular inverse of $13$, i.e.

$S(m) \equiv 1 \pmod n$

$13 \cdot 677 \equiv 1 \pmod{2200} \quad \checkmark$

## 4. Bezout's Theorem

$\gcd(m,n) = s(m) + t(n)$

for some $s,t \in \mathbb{Z}$, where $m,n$ are natural numbers and $m,n \ge 1$.

### Linear combinations

$s(m) + t(n), \qquad s,t \in \mathbb{Z}$

Example: $m = 77$, $n = 14$

$\gcd(77,14) = 7$

$77(s) + 14(t), \qquad s,t \text{ are integers}$

Number line of values:

| Value | $s$ | $t$ |
|:---:|:---:|:---:|
| $-77$ | $-1$ | $0$ |
| $-14$ | $0$ | $-1$ |
| $0$ | $0$ | $0$ |
| $7$ | $1$ | $-5$ |
| $14$ | $0$ | $1$ |
| $77$ | $1$ | $0$ |

Indeed,

$77(1) + 14(-5) = 77 - 70 = 7 = \gcd(77,14)$

$\boxed{s = 1,\quad t = -5}\quad\text{(Bezout coefficients)}$

**Co-prime** is a synonym for **relatively prime**.

$\boxed{S(m) \equiv 1 \pmod n}$

Example: $\gcd(3,17) = 1$,

$S(3) \bmod 17 = 1$

so $S = 6$, and

$6 \cdot 3 \bmod 17 = 1$

### Corollary of Bezout's Theorem

Every number $k$ that can be written as a linear combination of $m$ and $n$ is a **multiple** of $\gcd(m,n)$.

## 5. Relatively Prime Numbers

Two natural numbers $m,n$ whose gcd is $1$:

$\gcd(m,n) = 1 \iff \text{relatively prime}$

### Examples

$m = 75 = 5^3$, $n = 121 = 11^2$:

> no common prime factors $\Rightarrow$ relatively prime.

$m = 45 = 5 \times 3^2$, $n = 125 = 5^3$:

> $5$ is a common prime factor $\Rightarrow$ not relatively prime.

If $m,n$ are co-prime, then there exist $s,t$ such that

$m(s) + n(t) = 1$

If $a,b$ are relatively prime and $a \mid bc$, then $a \mid c$.

Example:

$a = 75,\quad b = 121,\quad c = \text{multiple of } a$

$a = 25,\quad b = 44$

**Bezout's coefficient gives the modular inverse.**

## 6. Extended Euclidean Algorithm in Code

### Basic Euclidean algorithm

```text
gcd(m, n):
    m >= n >= 0
    while (n > 0):
        k = m mod n
        m = n
        n = k
    return m
```

Trace for $\gcd(17, 13)$:

> Note: the notes write $117$, but the trace is consistent with $17 \bmod 13 = 4$.

```text
gcd(17, 13)
    m = 17
    n = 13
    while (n > 0):
        k = 17 mod 13
        k = 4
        m = 13, n = 4
        k = 13 mod 4
        k = 1
        m = 4, n = 1
        k = 4 mod 1
        k = 0
        m = 1, n = 0
    return m = 1
```

### Extended Euclidean algorithm with Bezout coefficients

```text
gcd(m, n):
    m >= n >= 0
    m0, n0

    s1, t1 = (1, 0)
    s2, t2 = (0, 1)

    while (n > 0):
        # every iteration this must be satisfied:
        # m = s1*m0 + t1*n0
        # n = s2*m0 + t2*n0      (linear combinations)
        k = m mod n
        q = m // n

        # after loop / update step:
        m = n
        n = k

        (s1, t1) = (s2, t2)
        (s2, t2) = (s1 - q*s2, t1 - q*t2)

    return m, s1, t1
```

Note:

$m^{(p)} = n = S_2 \cdot m_0 + t_2 \cdot n_0$

## 7. Extended Euclidean Algorithm Example

$\gcd(252, 198) = 18$

Let

$A = 252,\quad B = 198$

Then

$252 = 1A + 0B$

$198 = 0A + 1B$

$54 = 1A + (-1)B$

$36 = 198 - 3 \cdot 54$

$36 = B - 3[A + (-1)B] \quad\text{(recipe for } 54\text{; substitute for } 3 \cdot 54\text{)}$

$36 = B - 3A + 3B$

$36 = -3A + 4B$

$18 = 54 - 36 = A + (-1)B - [-3A + 4B]$

$18 = A - B - [-3A + 4B]$

$18 = 4A - 5B$

Check:

$252 \cdot 4 = 1008$

$198 \cdot 5 = 990$

$1008 - 990 = 18$

This looks like Bezout's Theorem.

## 8. Modular Inverse

Example: $a = 2$, $b = ?$, $n = 7$.

Find $b$ such that

$a \cdot b \equiv 1 \pmod 7$

$(a \cdot b \bmod 7) = 1$

$\star$ $b$ is the modular inverse. $\star$

$b = 4: \quad 2 \cdot 4 = 8 \equiv 1 \pmod 7$

- $2$ is the modular inverse of $4 \pmod 7$.
- $4$ is the modular inverse of $2 \pmod 7$.

If $b$ is the modular inverse of $a$, then $a$ is the modular inverse of $b$.

There are sometimes more values for $b$ that work:

$b = 4,\ 11,\ -3,\ 18$

$4 \cdot 2 = 8 \equiv 1 \pmod 7$

$11 \cdot 2 = 22 \equiv 1 \pmod 7$

$-3 \cdot 2 = -6 \equiv 1 \pmod 7$

$18 \cdot 2 = 36 \equiv 1 \pmod 7$

### Definition

Let $a$ and $n$ be two relatively prime numbers. The number $b$ is called the **modular inverse** of $a \pmod n$ if

$a \cdot b \pmod n \equiv 1 \pmod n$

### Theorem

If $a,n$ are relatively prime, there exists $b$ such that

$a \cdot b \equiv 1 \pmod n$

$\boxed{S(a) \equiv 1 \bmod n}$

## 9. Modular Congruence

$a(x) \equiv 1 \pmod 7$

with

$a = 3,\quad n = 7$

Find $x$ such that

$3x \equiv 1 \pmod 7$

$3 \cdot 5 = 15$

$15 \bmod 7 = 1$

$\therefore\quad 3 \cdot 5 \equiv 1 \pmod 7$

So $5$ is the modular inverse of $3 \pmod 7$.

Now solve

$3x \equiv 4 \pmod 7$

Since $5$ is the modular inverse of $3 \pmod 7$, multiplying $3$ by its inverse cancels out the $3$:

$5 \cdot 3x \equiv 5 \cdot 4 \quad\text{(multiply on both sides)}$

$(5 \cdot 3 \bmod 7) \cdot (x \bmod 7) \equiv 5 \cdot 4 \bmod 7$

$15 \bmod 7$

$1 \cdot (x \bmod 7) \qquad 20 \bmod 7$

$\boxed{x \equiv 6 \pmod 7}$

### Formula

$a \cdot x \equiv b \pmod n$

provided $a,n$ are relatively prime.

Let $C$ be the modular inverse of $a \pmod n$. Then

$C \cdot a \cdot x \equiv b \cdot C$

$C \cdot a \equiv 1$

$1 \cdot x \equiv b \cdot C \pmod n$

$\boxed{x \equiv b \cdot C \pmod n}$

## 10. Fermat's Little Theorem

### Theorem

Let $P$ be any prime number and let $a$ be a number between $1$ and $P-1$. Then

$\boxed{a^{P-1} \equiv 1 \pmod P}$

Uses:

1. Cryptography
2. Prime number testing

### Example

Let

$P = 31 \quad\text{(prime)},\quad a = 2$

Then

$2^{30} \equiv 1 \pmod{31}$

Verification:

$2^{30} \bmod 31 = (2^5)^6 \bmod 31$

$= (2^5 \bmod 31)^6 \bmod 31$

$= (32 \bmod 31) \bmod 31$

$= 1$
