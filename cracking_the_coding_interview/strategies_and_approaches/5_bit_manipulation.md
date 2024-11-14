# Bit Manipulation

- used in a variety of problems
- the question sometimes explicitly calls for bit manipulation
- other times, its just a useful technique that can optimize your code


Bit Facts and Tricks:
The following expressions are useful in bit manipulation. Don't just memorize them, though; think deeply
about why each of these is true. We use "1 s" and "Os" to indicate a sequence of 1 s or Os, respectively.

`x ^ 0s = x`
`x ^ 1s = ~x`
`x ^ x = 0`
`x & 0s = 0`
`x & 1s = x`
`x & x = x`
`x | 0s = x`
`x | 1s = 1s`
`x | x = x`

- recall that operations occur bit-by-bit
- what's happening on one bit is never impacting other bits
- if one of the above statements is true for a single bit, then it's tree for a sequence of bits

- notes about two's complement and negative numbers in relation to bit manipulation

- notes on arithmetic vs logical right shifts

- common bit tasks: get, set, clear, update bit