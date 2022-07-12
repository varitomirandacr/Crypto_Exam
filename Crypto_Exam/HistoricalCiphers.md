
## Shift Cipher
Encryption is performed by replacing each letter by the letter located in a certain number of places further on in the alphabet.
- Caesar cipher
- the secret key k modulo 26
- shift cipher is that the number of keys is too small
```
HELLO = KHOOR
```
How to break shift cipher:
We compute the frequencies of the letters in the ciphertext and compare them with the frequencies obtained from English. Using the statistical distance or total variation distance.
$$ \Delta[X,Y] = \frac{1}{2} \sum_{u \in V} \Big| Pr_{X \leftarrow D_{1}} [X = u]  -  Pr_{Y \leftarrow D_{2}} [Y = u]\Big| $$

### Statistical Distance 
```
wikipedia
the distance between two statistical objects, which can be two random variables, or two probability distributions or samples...
```
Properties:
- Bounded $0 \leq \Delta(X,Y) \leq 1$
- Symmetric $\Delta(X,Y) = \Delta(X,Y)$
- Triangle inequality $\Delta(X,Z) \leq \Delta(X,Y) + \Delta(Y,Z) \leq 1$
<br/>
<hr/>

## Substitution Cipher
To increase the number of keys the substitution cipher was invented. The number of possible keys is equal to the total number of permutations on 26 letters, namely the size of the group S26, which is 
$$ 26! \approx 4.03 * 10^{26} \approx^{88} $$
```
Plaintext alphabet ABCDEFGHIJKLMNOPQRSTUVWXYZ
Ciphertext alphabet GOYDSIPELUAVCRJWXZNHBQFTMK
HELLO = ESVVJ
```

How to break substitution cipher:
The problem with the shift cipher and the substitution cipher was that each plaintext letter always encrypted to the same ciphertext letter.
Can break substitution ciphers using statistics of the underlying plaintext language, just as we did for the shift cipher. Hence underlying statistics of the language could be used to break the cipher.

<br/>
<hr/>

## Vigenère Cipher
Polyalphabetic substitution cipher. Identifies letters with the numbers 0,...,25. The secret key is a short sequence of letters (e.g. a word) which is repeated again and again to form a keystream.Where it generates a key based on the amount of alphabets used. With five alphabets the total key space is
$$ (26!)^{5} \approx 2^{441}$$
but the user only needs to remember the key which is a sequence of
$$ 26·5 = 130$$
Then use the key to generate the encryption, shifting the text.
```
For example we could take 
Plaintext alphabet      ABCDEFGHIJKLMNOPQRSTUVWXYZ
Ciphertext alphabet one TMKGOYDSIPELUAVCRJWXZNHBQF
Ciphertext alphabet two DCBAHGFEMLKJIZYXWVUTSRQPON
```
How to Encrypt:
$$ct_{𝑖} = pt_{𝑖} \oplus 𝑘_{(𝑖\ mod\ 𝑛)}$$
How to break Vigenere Cipher:
Vigen`ere cipher is still easy to break using the underlying statistics of English. Once we have found the length of the keyword, breaking the ciphertext is the same as breaking the shift cipher a number of times.

- Vigenère cipher using a key as long as the plaintext.
- Finding key length:
    - Hamming distance 
    $$ \Delta_{H}(0101,0100) = 1 $$
    - IoC: Index of Coincidence
    $$ IC = \frac{\sum_{i=1}^{n} F_{i}(F_{i}-1)}{N(N-1)} $$

<br/>
<hr/>

## Permutation Cipher
Encrpytion of text based on permutation cipher given a sequence of values which is consider a key and replacing each value by each letter corresponding to its position i.e. $S_{n}$

$$ \sigma = \Big( \frac{1 2 3 4 5}{2 4 1 3 5} \Big) = (1243) \in S_{5}$$

However, breaking a permutation cipher is easy with a chosen plaintext attack, assuming the group of permutations used (i.e. the value of n) is reasonably small. To attack this cipher we mount a chosen plaintext attack, i.e. the attacker selects a plaintext of their choosing and asks for the encryption of it


<br/>
<hr/>

## Caveats
- Historical ciphers are insecure