# Bitwise Operations
- integers are represented as a string of bits (binary digits)
- can be big endian (left digit is most significant bit) or little endian (right digit is the most significant bit)
    - i.e three hundred twenty one - 321 (big endian) or 123 (little endian)
- representation space for unsigned integers is 2^n, where n is the width of the integer (i.e 256 bit integer has 2^256 possible values)
- signed integers, most common way of finding representation is 2's complement
    - invert all the bits then add 1
    - provides 1 representation of 0 (instead of a positive and negative representation)
    - with 2's complement, a signed int with n bits represents numbers from -2^(n-1) to 2^(n-1) - 1 (8 bits encodes -128 to 127)
- Java supports the 2's complement signed primitives
    - byte - 8 bits
    - short - 16 bits
    - int - 32 bits
    - long - 64 bits
    - note: char is a unsigned 16 bits
- Python supports 4 numeric types [link](https://docs.python.org/2/library/stdtypes.html)
    - int - implemented using C's long, giving atleast 32 bits of precisions
    - float - implemented using C's double, number of bits is machine dependent
    - long - unlimited precision, expands to the limit of the available memory
    - complex - have a real and imaginary part, both of them float
    - fractions - hold rational numbers
    - decimal - hold floating point numbers with user defined precision

### Arithmetic
- adding - normal, just remember to carry the 1
- subtraction - easiest to treat it as negative addition
- multiplication - treaat it as left bitshifts.  Multiply by 2 is the same as adding a 0 to the end of the digit.  Can break down any multiplication into multiplaction with powers of 2
- division - right bitshifts, but only really handles it as integer division, so rounding will be done implicitly

### Bitwise Operations
- & - AND (1&1 = 1, 0&1 = 0, 0&0 = 0)
- | - inclusive OR (1|1 = 1, 0|1 = 1, 0|0 = 0)
- ^ - XOR (1^1 = 0, 0^1 = 1, 0^0 = 0)
- x << n - left shift x by n places, appeneding 0s to the end (equivalent to x * 2^n)
- x >> n - right shifts x by n places using sign extensions (equivalent to x / 2^n, integer division)
    - in Python, right shift zero fills
- ~ - flips bits, not operation

#### Bit facts and Tricks
- since operations are bitwsie (occur bit by bit), these are all equivalent to their series-equivalents
- XOR
    - x ^ 0 = x
    - x ^ 1 = ~x
    - x ^ x = 0
- AND
    - x & 0 = 0
    - x & 1 = 1
    - x & x = x
- OR
    - x | 0 = x
    - x | 1 = 1
    - x | x = x
- swap two values without using a temporary variable
    - a = a ^ b
    - b = a ^ b
    - a = a ^ b 


### Common (and Uncommon) Bit Tasks
- return the ith bit
    - first, left shift 1 by i to create a bit mask (a number where everything is 0 except for 1 in the ith spot, 00010000)
    - AND the mask with the number.  If the value is not 1, then bit i is 1, else its 0
- set the ith bit to 1
    - left shift 1 by i to create a bit mask
    - OR the mask with the input number, forcing the ith bit to 1
- clear the ith bit (set it to 0)
    - left shift 1 by i, then invert it to create mask like (11101111)
    - AND the mask with the input number.  The ith spot will be the only zero and will be zeroed out, everying else will remaint
- update the ith bit with v (set ith bit to v)
    - do a combination of the previous 2.  First clear out the ith bit, then shift v to the ith bit and and it.
- clear the rightmost bit
    - number & (number - 1)
    - this concept forms the basis of parity
- calculate parity - return true if the number of 1s is odd, 0 otherwise
    - boils down to counting the number of 1s
    - naive method:  set parity to false (even), keep clearing the rightmost bit until the result is 0.  Everytime you clear, flip the parity
    - time complexity is O(s) where s is the number of set bits
    ```python
        def countOnes(int n):
            count = 0
            while n != 0:
                n = n & (n-1)
                count += 1
            return count
    ```
    - can do a better by using a look up table.  Can store parities for values 0 to 15 (16 bit).  To find parity for a bigger number then, can just OR with 16 1s and look up in table
- calculate the Hamming Distance
    - the Hamming Distance between two integers is the number of positions that the bits are different
    ```python
    def hammingDistance(x, y):
        z = x ^ y   # 1 in every space where they are different
        return countOnes(z) # then its just counting 1s again