# debruijn-generator


A simple Python implementation to generate De Bruijn sequences.
## What is a De Bruijn Sequence?
A De Bruijn sequence for parameters `k` and `n` is a cyclic sequence in which every possible substring of length `n` over an alphabet of size `k` appears exactly once as a contiguous substring.
For example, the De Bruijn sequence for `k=2` (binary alphabet) and `n=3` is:

00010111

This sequence contains all possible binary strings of length 3: `000`, `001`, `010`, `101`, `011`, `111`, `110`, `100`.

## How it works

This implementation uses a recursive algorithm based on Lyndon words to generate a De Bruijn sequence of order `n` over an alphabet of size `k`.

## Usage

```python
def de_bruijn_sequence(k, n):
    a = [0] * k * n
    sequence = []

    def db(t, p):
        if t > n:
            if n % p == 0:
                for j in range(1, p + 1):
                    sequence.append(a[j])
        else:
            a[t] = a[t - p]
            db(t + 1, p)
            for j in range(a[t - p] + 1, k):
                a[t] = j
                db(t + 1, t)

    db(1, 1)
    return ''.join(str(bit) for bit in sequence) + str(sequence[0]) * (n - 1)

# Example: generate a binary De Bruijn sequence of order 4
result = de_bruijn_sequence(2, 4)
print(result)
```

### Output:

0000100110101111

### Parameters
k: Size of the alphabet (e.g., 2 for binary, 4 for DNA bases)
n: Length of the substrings (order of the sequence)

### Applications
DNA sequence design and analysis
Cryptography
Data compression
Robotics and automated testing
Combinatorics and theoretical computer science

### License
This project is licensed under the MIT License.





