# float_32 to binary conversion

## For example:

The size of `union` is the size of one of the largest member element

```cpp
union point_t {
    int i;
    char c;
    float f;
};
    :
    :
point_t point;
point.i = 65;
std::cout << "i: " << point.i << std::endl;
std::cout << "c: " << point.c << std::endl;
std::cout << "f: " << point.f << std::endl;
    :
    :
```

### Output:

```shell
i: 65
c: A
f: 9.10844e-44

# `f` value looks like garbage
# The big one in `point_t` is float. So, the sizeof(point_t) = 32
```

### `float_32` memory layout

:material-checkbox-blank-badge-outline:
:material-checkbox-blank::material-checkbox-blank::material-checkbox-blank::material-checkbox-blank:
:material-checkbox-blank::material-checkbox-blank::material-checkbox-blank::material-checkbox-blank:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline::material-checkbox-blank-outline:
:material-checkbox-blank-outline::material-checkbox-blank-outline:

[//]: # (@formatter:off)
!!! info
    :material-checkbox-blank-badge-outline: `1 bit -> Sign`

    :material-checkbox-blank: `8 bits -> Int part (Exponent)`

    :material-checkbox-blank-outline: `23 bits -> Decimal part (Significand/Mantissa)`
[//]: # (@formatter:on)

## Math time

Converting (+98.569)~10~ to (xxxx)~2~

```shell
 Bit
 Position
      ---
       32: 0 # positive number
[31 - 24]: 01100010 # 98 binary
       23: 0.569 * 2 = 1.138
       22: 0.138 * 2 = 0.276
       21: 0.276 * 2 = 0.552
       20: 0.552 * 2 = 1.104
       19: 0.104 * 2 = 0.208
       18: 0.416 * 2 = 0.832
       17: 0.832 * 2 = 1.664
       16: 0.664 * 2 = 1.328
       15: 0.328 * 2 = 0.656
       14: 0.656 * 2 = 1.312
       13: 0.312 * 2 = 0.624
       12: 0.624 * 2 = 1.248
       11: 0.248 * 2 = 0.496
       10: 0.496 * 2 = 0.992
       09: 0.992 * 2 = 1.984
       08: 0.984 * 2 = 1.968
       07: 0.968 * 2 = 1.936
       06: 0.936 * 2 = 1.872
       05: 0.872 * 2 = 1.744
       04: 0.744 * 2 = 1.488
       03: 0.488 * 2 = 0.976
       02: 0.976 * 2 = 0.952
       00: 0.952 * 2 = 1.904
# No more bits
```

```
Collect all exponents (1 and 0) from multiplication

        .569 = 10010011010100111111001

Final Binary = 0|01100010|10010011010100111111001
```
