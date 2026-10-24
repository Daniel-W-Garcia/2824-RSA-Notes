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

## 11. RSA Key Creation

### Key Creation
1. Select two large prime numbers x and y
2. Calculate n = x * y
3. Compute the totient function φ(n) = (x-1)(y-1)
4. Select an integer e such that e is co-prime to φ(n) and 1 < e < φ(n)
   - The pair of numbers (n, e) forms the public key
   - Two integers are co-prime if they only positive integer that divides them is 1
   - Cannot share any prime factors.
5. Calculate d such that d * e ≡ 1 (mod φ(n))
    - d can be found using the Extended Euclidean Algorithm.
    - The pair of numbers (n, d) forms the private key.

## 12. Totient Function and Co-prime

**co-prime:**
```text

Example 6:

6 has prime factors of 2 and 3

Check from 1-n for prime factors of 6
1 does NOT have factors of 2 or 3.
2 HAS factors of 2.
3 HAS factors of 3.
4 HAS factors of 2.
5 does NOT have factors of 2 or 3.
6 HAS factors of 2 and 3.

2 integers without factors of 2 or 3.
So 1 and 5 are co-prime to 6
```
$\varphi(6) = 2$ ***There are 2 co-prime integers in 6***
$\varphi(n)$ where $n$ is a prime number, is always $n - 1$.
$\varphi(5) = 4$

**prime $\cdot$ itself **
$5 \cdot 5 = 25$
$\varphi(25)$

$\begin{aligned}
&1 &&2 &&3 &&4 &&5 \cr
&6 &&7 &&8 &&9 &&10 \cr
&11 &&12 &&13 &&14 &&15 \cr
&16 &&17 &&18 &&19 &&20 \cr
&21 &&22 &&23 &&24 &&25 \cr
\end{aligned}$

***Remove prime and multiples of prime***

$\begin{aligned}
&1 &&2 &&3 &&4 \cr
&6 &&7 &&8 &&9 \cr
&11 &&12 &&13 &&14 \cr
&16 &&17 &&18 &&19 \cr
&21 &&22 &&23 &&24 \cr
\end{aligned}$

$\begin{aligned}
&1 &&2 &&3 &&4 &&(p - 1)\cr
&6 &&7 &&8 &&9 &&p(p - 1)\cr
&11 &&12 &&13 &&14 &&p^2(p - 1) \cr
&16 &&17 &&18 &&19 &&p^3(p - 1) \cr
&21 &&22 &&23 &&24 &&p^4(p - 1) \cr
\end{aligned}$

---

***For different prime numbers:***
$\varphi(pq) = (p - 1)(q - 1)$
$\varphi(pqr) = (p - 1)(q - 1)(r - 1)$ ...etc
$\equiv p^{a-1}(p - 1)$
$\equiv p^{a-1}(p - 1)$
$\therefore &nbsp; \varphi(p^a) = p^{a-1}(p - 1)$

- **ALL PRIMES MUST BE DISTINCT FOR THIS ALGORITHM**

---

***For a mix of prime numbers:***
$\varphi(60)$
Prime factors $= 2 * 2 * 3 * 5$

Set aside the second 2:
$\varphi(60) = (2 - 1)(3 - 1)(5 - 1) = 8$

Now multiply that result by the 2 set aside:
$\varphi(60) = 2 * 8 = 16$

$\varphi(n) = n\left(\frac{p_1 - 1}{p_1}\right)\left(\frac{p_2 - 1}{p_2}\right)\cdots\left(\frac{p_z - 1}{p_z}\right)$
$\equiv\varphi(n) = n\left(1 - \frac{1}{p_1}\right)\left(1 - \frac{1}{p_2}\right)\cdots\left(1 - \frac{1}{p_z}\right)$
$\equiv\varphi(n) = p_1^{k_1 - 1}(p_1 - 1) \cdot p_2^{k_2 - 1}(p_2 - 1) \cdots p_z^{k_z - 1}(p_z - 1)$
where $n = p_1^{k_1}p_2^{k_2}\cdots p_z^{k_z}$ and $p_1, p_2, \ldots, p_z$ are distinct primes and the exponents $k1, k2$ and so on are their exponents..

$\equiv$ "How many integers between 1 and n are co-prime to n?"

## 13. Number Theory Foundations

### The Fundamental Theorem of Arithmatic

***Every integer greater than 1 can be uniquely expressed as a product of prime numbers.***

- Examples:
  - 100 = $2^2 \cdot 5^2$ or $(2 \cdot 2 \cdot 5 \cdot 5)$
  - 641 = 641 (it is prime)
  - 999 = $3^3 \cdot 37$
  - 1024 = $2^{10}$

### Trial Division
- If $n$ is prime, then $n$ thas a prime divisor less than or equal to $\sqrt{n}$.
- Proof:
  - If $n$ is composite, by definition of a composite number, we know that it has a factor $a$ with $1 \lt a \lt n$
    - By definition of a factor of a positive integer, $n = ab$ where $b$ is a positive integer and greater than 1.
    - $(a \leq \sqrt{n}) \lor (b \leq \sqrt{n})$
      - if $(a \geq \sqrt{n}) \land (b \leq \sqrt{n})$ then $a \cdot b \gt (\sqrt{n} \cdot \sqrt{n}) = n$
        - so $(a \lor b) \leq \sqrt{n}$
- Show that 101 is prime:
  - $\sqrt{101} \approx 10$
    - Only primes not exceeding 10 are 2, 3, 5, 7.
    - 101 is not evenly divisible by any of these primes.
  - Every integer has a prime factorization. If $n$ is not divisible by any primes $\le \sqrt{n}$, then $n$ is prime.
- Find Prime factorization of 7007:
  - 2 does not divide 7007.
  - 3 does not divide 7007.
  - 5 does not divide 7007.
  - 7 DOES divide 7007. 7007/7 = 1001
    - Now try to divide 1001 by 7.
      - 1001/7 = 143
      - Now try to divide 143 by 7.
        - It does not divide 143 evenly. So try next prime.
        - 143/11 = 13
        - 13 is prime so 13 is the final prime factor of 7007.
          - 7007 = $7 \cdot 7 \cdot 11 \cdot 13$ or $7^2 \cdot 11 \cdot 13$

### The Sieve of Eratosthenes
- Find all primes less than $n$
- $n = 100$
  - Remove all multiples of 2 except 2
  - Remove all multiples of 3 except 3
  - Remove all multiples of 5 except 5
  - Remove all multiples of 7 except 7
  - Since all composite ints between 0 and 100 are divisble by a prime less than or equal to $\sqrt{100} = 10$
    - anything remaining is prime

### Pairwise Relatively Prime
- Two integers are relatively prime if they have no common factors other than 1.
- 17 and 22 are relatively prime because their only common factor is 1.
  - 22 is not prime but 17 and 22 are relatively prime because their only common factor is 1.

### Greatest Common Divisor
- Using Prime Factorization:
  - $a = p_1^{ai} p_2^{a2}... p_n^{a_n} $  $b = p_1^{bi} p_2^{b2}... p_n^{b_n} $
    - Where each exponent is a non-negative integer, and where all primes occurring in the prime factorization of
    either $a$ or $b$ are included in both factorizations, with zero exponents if necessary.
      - Then gcd$(a,b) = p_1^{min(ai,bi)} p_2^{min(a2,b2)}... p_n^{min(a_n,b_n)}$
      - Example: $gcd(120, 500) =
        - 120 factorization: $2^3 \cdot 3^1 \cdot 5^1$
        - 500 factorization: $2^2 \cdot 5^3$
        - $2^{min(3,2)} \cdot 3^{min(0,1)} \cdot 5^{min(1,2)} = 2^2 \cdot 5^1 = 20$

### Least Common Multiple
- Using Prime Factorization:
  - $lcm(a,b) = p_1^{max (a1, b1)} p_2^{max(a2,b2)}... p_n^{max(a_n,b_n)}$
  - Example: $lcm(2^33^57^2, 2^43^3) = 2^{max(3,4)} \cdot 3^{max(5,3)} \cdot 7^{max(2,0)} = 2^4 \cdot 3^5 \cdot 7^2 =  190512$

### The Euclidean Algorithm
- An efficient way to find the greatest common divisor of two integers.
- $gcd(287, 91)$
  - First divide 287 by 91 to get a quotient of 3 and a remainder of 14.
    - Any divisor of 287 and 91 must also be a divisor of $91 \cdot 3 + 14$
      - Hence the gcd of 287 and 91 is the same as the gcd of 91 and 14.
      - Repeat the above process:
        - $91 = 14 \cdot 6 + 7$
        - Because and common divisor of 91 and 14 must also be a divisor of 7.
        - $gcd(14,7) = 7$
        - Hence $gcd(287,91) = 7$
```c++
int euclidean(int a, int b) {
    x = a;
    y = b;

    while (y != 0) {
        r = x % y;
        x = y;
        y = r;
    }
    return x;
}

```

## 14. Modular Exponentiation

### Square and Mod Chart
$O(n)$
$5\mod 17 = 5$

$\begin{aligned}
5^0\mod 17 = 1 &emsp; &\cr
5^1\mod 17 = 5 &emsp; &\cr
5^2\mod 17 = 8 &emsp; &\equiv (5^1\mod 17) \cdot (5^1\mod 17) \cr
&emsp; &\equiv (5 \cdot 5 \mod 17) \equiv 25 \mod 17 = 8 \cr
5^3\mod 17 = 6 &emsp; &\equiv (5^2\mod 17) \cdot (5^1\mod 17) \cr
&emsp; &\equiv (8 \cdot 5 \mod 17) \equiv 40 \mod 17 = 6 \cr
5^4\mod 17 = 13 &emsp; &\equiv (5^2\mod 17) \cdot (5^2\mod 17) \cr
&emsp; &\equiv (8 \cdot 8 \mod 17) \equiv 64 \mod 17 = 13 \cr
5^5\mod 17 = 14 &emsp; &\equiv (5^4\mod 17) \cdot (5^1\mod 17) \cr
&emsp; &\equiv (13 \cdot 5 \mod 17) \equiv 65 \mod 17 = 14 \cr
5^6\mod 17 = 2 &emsp; &\equiv (5^4\mod 17) \cdot (5^2\mod 17) \cr
&emsp; &\equiv (13 \cdot 8 \mod 17) \equiv 104 \mod 17 = 2 \cr
5^7\mod 17 = 10 &emsp; &\equiv (5^4\mod 17) \cdot (5^3\mod 17) \cr
&emsp; &\equiv (13 \cdot 6 \mod 17) \equiv 78 \mod 17 = 10 \cr
5^8\mod 17 = 16 &emsp; &\equiv (5^4\mod 17) \cdot (5^4\mod 17) \cr
&emsp; &\equiv (13 \cdot 13 \mod 17) = 169 \mod 17 = 16 \cr
5^9\mod 17 = 12 &emsp; &\equiv (5^8\mod 17) \cdot (5^1\mod 17) \cr
&emsp; &\equiv (16 \cdot 5 \mod 17) \equiv 80 \mod 17 = 12 \cr
5^{10}\mod 17 = 9 &emsp; &\equiv (5^8\mod 17) \cdot (5^2\mod 17) \cr
&emsp; &\equiv (16 \cdot 8 \mod 17) \equiv 128 \mod 17 = 9 \cr
5^{11}\mod 17 = 11 &emsp; &\equiv (5^8\mod 17) \cdot (5^3\mod 17) \cr
&emsp; &\equiv (16 \cdot 6 \mod 17) \equiv 96 \mod 17 = 11 \cr
5^{12}\mod 17 = 4 &emsp; &\equiv (5^8\mod 17) \cdot (5^4\mod 17) \cr
&emsp; &\equiv (16 \cdot 13 \mod 17) \equiv 208 \mod 17 = 4 \cr
5^{13}\mod 17 = 3 &emsp; &\equiv (5^8\mod 17) \cdot (5^5\mod 17) \cr
&emsp; &\equiv (16 \cdot 14 \mod 17) \equiv 224 \mod 17 = 3 \cr
5^{14}\mod 17 = 15 &emsp; &\equiv (5^8\mod 17) \cdot (5^6\mod 17) \cr
&emsp; &\equiv (16 \cdot 2 \mod 17) \equiv 32 \mod 17 = 15 \cr
5^{15}\mod 17 = 7 &emsp; &\equiv (5^8\mod 17) \cdot (5^7\mod 17) \cr
&emsp; &\equiv (16 \cdot 10 \mod 17) \equiv 160 \mod 17 = 7 \cr
\end{aligned}$
&nbsp;

```text
All base2 cases divisible by 16 after this point will equal 1
```
 ---
$5^{16}\mod 17 = 1 \equiv (5^8\mod 17) &nbsp; \cdot &nbsp; (5^8\mod 17)$
$(16 \cdot 16 \mod 17) = 256 \mod 17 = 1$
$(17 \cdot 15 = 255 + 1 = 256)$

$5^{32}\mod 17 = 1$
$5^{n\mod 16 &nbsp; = &nbsp; 0}\mod 17 \equiv 5^{16} \equiv 1$

---
### Congruencies
- Things that are equal when they share the same remainder when divided by k
- Theorem: if $a \equiv b\mod k \to a-b$ is divisible by k


$a \equiv b\mod k$
($\to$) $a\mod k \equiv b\mod k$
$ a = 22 \mod 17 = 5 &nbsp; &nbsp;\equiv &nbsp; b = 15\mod 17 \equiv 1$

$(12 \equiv 19) \mod 7$

---
### Notation
- Modulo operations are a function. Takes and int and returns an int
- Congruences are a relation. Like a boolean (true of false/yes or no)

---
### Arithmetic
$(a+b)\mod k = ((a\mod k) &nbsp;+&nbsp; (b\mod k))\mod k$
$a+b \equiv (a\mod k) + (b\mod k)$

---

$(a \cdot b)\mod k \equiv ((a\mod k) &nbsp; \cdot (b\mod k))\mod k$
$2^{20}\mod 5 \equiv ((2^{10} \mod 5)&nbsp; \cdot (2^{10} \mod 5))\mod 5$
$((1024\mod 5) \cdot (1024\mod 5)) \mod 5$
$4 \cdot 4 \mod 5 = 16 \mod 5 = 1$
$2^{50}\mod 5 \equiv ((2^{10} \mod 5) &nbsp; (2^{10} \mod 5) &nbsp; (2^{10} \mod 5) &nbsp; (2^{10} \mod 5) &nbsp;(2^{10} \mod 5)) \mod 5$
$((1024\mod 5) \cdot (1024\mod 5)\cdot(1024\mod 5) \cdot (1024\mod 5)\cdot(1024\mod 5))\mod 5$
$(4 \cdot 4 \cdot 4 \cdot 4 \cdot 4) \mod 5$
$((16\mod 5) \cdot (16\mod 5) \cdot 4)\mod 5$
$((1 \cdot 1 \cdot 1 \cdot 1) \cdot 4)) \mod 5 = 4$

## 15. Square-and-Mod Chart

Square-and-Mod Chart for a = 4 and b = 19

$$
\begin{array}{c|l|c}
\text{Power} & \text{Calculation} & \text{Remainder mod }19\\
\hline
4^1 & 4 & 4\\
4^2 & 4\cdot4=16 & 16\\
4^4 & (4^2)^2\equiv16^2=256=19\cdot13+9 & 9\\
4^8 & (4^4)^2\equiv9^2=81=19\cdot4+5 & 5\\
4^{16} & (4^8)^2\equiv5^2=25=19\cdot1+6 & 6\\
4^{32} & (4^{16})^2\equiv6^2=36=19\cdot1+17 & 17\\
4^{64} & (4^{32})^2\equiv17^2=289=19\cdot15+4 & 4\\
4^{128} & (4^{64})^2\equiv4^2=16 & 16\\
4^{256} & (4^{128})^2\equiv16^2=256=19\cdot13+9 & 9
\end{array}
$$

To find 4^321 mod 19, first write:

$$
321=256+64+1
$$

Then use the corresponding values from the chart:

$$
\begin{aligned}
4^{321}
&=4^{256+64+1}\\
&\equiv4^{256}\cdot4^{64}\cdot4^1 \pmod{19}\\
&\equiv9\cdot4\cdot4\\
&=144\\
&=19\cdot7+11.
\end{aligned}
$$

$$
\boxed{4^{321}\equiv11\pmod{19}}
$$
