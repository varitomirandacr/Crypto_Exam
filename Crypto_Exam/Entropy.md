
# Entropy
To simplify the key distribution problem we need to turn from perfectly secure encryption algo- rithms to ones which are, we hope, computationally secure. This is the goal of modern cryptography, where one aims to build systems such that:
- one key can be used many times,
- a small key can encrypt a long message.

The entropy in the ciphertext is the amount of uncertainty you have about the underlying plaintext.
$$ H(X), H(X) = 0 \ no, H(X) = 1 \ yes $$

Let $𝑋$ be a random variable which takes a finite set of values $𝑥_{𝑖}$, with $1 ≤ 𝑖 ≤ 𝑛$, and has probability distribution $𝑝_{𝑖} = Pr[𝑋 = 𝑥_{𝑖}]$, where we use the convention that if $𝑝_{𝑖} = 0$ then $𝑝_{𝑖}\ log_{2}\ 𝑝_{𝑖} = 0$. The entropy of $𝑋$ is defined to be:
$$ H(X) = - \sum_{i=1}^{n}p_{i} * \log_{2}p_{i} $$

Properties:
- Non-negativity: $𝐻(𝑋) ≥ 0$ for any random variable $𝑋$
- Lower bound: $𝐻(𝑋) = 0$ if and only if there exists a $𝑝_{𝑖}$ such that $𝑝_{𝑖} = 1$ $p_{j} =0$ when $i \neq j$
- Upper bound: $𝐻(𝑋)=log_{2}𝑛$ if and only if $𝑝_{𝑖} = \frac{1}{n}$ for all $𝑖$

<br/>

- $𝐻(𝑋,𝑌)=𝐻(𝑋 ∣𝑌)+𝐻(𝑌)$
- if and only if 𝑋 and 𝑌 are independent
    - $𝐻(𝑋 ∣ 𝑌) = 𝐻(𝑋)$
    - $𝐻(𝑋, 𝑌) = 𝐻(𝑋) + 𝐻(𝑌)$

<br/>
<hr/>

## Vernam cipher or one-time pad
To send a binary string we need a key, which is a binary string as long as the message. To encrypt a message we exclusive-or each bit of the plaintext with each bit of the key to produce the ciphertext.

- Each key is only allowed to be used once (one time pad)
- the secret key k modulo 26
- shift cipher is that the number of keys is too small

### Vernam Cipher:
$$ c_{i} = m_{i} \oplus k_{i} $$

### One Time Pad
Remark that when XORing a uniformly random keys with a plaintext results in a uniformly random ciphertext!
- A one-time pad is insecure if a key is used more than once
$$ 𝑐_{1} \oplus 𝑐_{2} =(𝑚_{1} \oplus 𝑘) \oplus (𝑚_{2} \oplus 𝑘) = 𝑚_{1} \oplus 𝑚_{2} $$ 

### Perfectly Secure Ciphers:
We have for the random variables of plaintext $𝑃$, keys $𝐾$, and ciphertext $𝐶$,
- $𝐻(𝑃 ∣ 𝐾,𝐶) = 0$
- $𝐻(𝐶 ∣ 𝑃,𝐾) = 0$
- $𝐻(𝑃, 𝐾, 𝐶) = 𝐻(𝑃 ∣ 𝐾, 𝐶) + 𝐻(𝐾, 𝐶) = 𝐻(𝐾, 𝐶)$
- $𝐻(𝑃, 𝐾, 𝐶) = 𝐻(𝐶 ∣ 𝑃, 𝐾) + 𝐻(𝑃, 𝐾) = 𝐻(𝑃, 𝐾) = 𝐻(𝑃) + 𝐻(𝐾)$
- $𝐻(𝐾, 𝐶) = 𝐻(𝑃) + 𝐻(𝐾)$
- $𝐻(𝐾 ∣𝐶)=𝐻(𝐾,𝐶)−𝐻(𝐶)=𝐻(𝑃)+𝐻(𝐾)−𝐻(𝐶)$
- Key equivocation, 𝐻(𝐾 ∣ 𝐶), is the amount of uncertainty left about the key after one ciphertext is revealed.

### Natural Language:
The entropy of a natural language 𝐿 is defined as... where 𝑃^{𝑛} denotes the frequencies of 𝑛-grams (bi-gram, tri-gram), i.e., $𝑃$ denotes the letter frequencies, $𝑃^{2}$ denotes the frequencies of bigrams, $𝑃^{3}$ of trigrams, etc.
- Bi-gram: TH, IN, ST
- Tri-gram: THE, ING, EST
$$ H_{L} = \lim_{n \rightarrow \infty} \frac{H(P^{n})}{n}$$

<br/>
<hr/>

## Joint Entropy
Variables X and Y part of the distribution
$$ 𝑟_{𝑖,𝑗} = Pr[𝑋 = 𝑥_{𝑖}, 𝑌 = 𝑦_{𝑗}] for 1 ≤ 𝑖 ≤ 𝑛 and 1 ≤ 𝑗 ≤ 𝑚 $$

The joint entropy of (𝑋 , 𝑌 ) is defined as
$$ H(X,Y) = - \sum_{i=1}^{n} \sum_{j=1}^{n} r_{ij} \cdot \log_{2} r_{ij} $$

<br/>
<hr/>

## Conditional Entropy
Variables X and Y defined in a group given certain condition:
$$ H(X|Y) = \sum_{y} Pr[Y=y] \cdot H(X|Y=y) $$
where
$$ H(X|Y=y)= - \sum_{x} Pr[X=x | Y=y] \cdot \log_{2} Pr[X=x | Y=y] $$

<br/>
<hr/>

## Information Theoretic Security vs Computational Security
|             | Information-Theoretic                                    | Computational                                         |
|-------------|----------------------------------------------------------|-------------------------------------------------------|
| Security    | Cannot be broken, not even with infinite computing power | Can be broken, but in an infeasible number operations |
| Assumptions | Does not rely on assumptions                             | Requires security assumptions                         |
| Key size    | At least as large as the plaintext                       | Small/practical                                       |
| Examples    | One-time pad, Shamir’s secret sharing scheme             | AES, RSA, ElGamal                                     |
