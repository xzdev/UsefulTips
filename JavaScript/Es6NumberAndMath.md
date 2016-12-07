## ES6 Number and Math
The following content is a summary of the chapter 5 [New number and Math features](http://exploringjs.com/es6/ch_numbers.html) of the [Exploring ES6](http://exploringjs.com/es6/).

### New Integer Literal
- Binary and octal notation

```
> 0b0011
3
> 0B0010
2
> 0o10
8
> 0O640
416
```

### Convert Numbers to Strings and Vice Versa
- Number method toString(radix) to convert numbers to strings

```
> 255..toString(16)
'ff'
> 4..toString(2)
'100'
> 8..toString(8)
'10'
``` 

- Convert strings to numbers

Number.parseInt(string, radix?),
Number.parseFloat(string)

```
> Number.parseInt('0xFF')
255
> Number.parseInt('0xFF', 0)
255
> Number.parseInt('0xFF', 16)
255

> Number.parseInt('0xFF', 10)
0
> Number.parseInt('0xFF', 17)
0

> Number.parseInt('0b111')
0
> Number.parseInt('0b111', 2)
0
> Number.parseInt('111', 2)
7
> Number.parseInt('0o10')
0
> Number.parseInt('0o10', 8)
0
> Number.parseInt('10', 8)
8

> Number('0b111')
7
> Number('0o10')
8
```

### New Number Properties
- JavaScript numbers are all floating point, stored according to the [IEEE 754 standard](https://en.wikipedia.org/wiki/IEEE_floating_point)

|sign|exponent|fraction|
|----|------|------|
|(1 bit)|(11 bit)|(52 bit)|
|63|62 --  52|51 -- 0|

- Number.EPSILON

Number.EPSILON specifies a reasonable margin of error when comparing floating point numbers.


```
> 0.1 + 0.2 === 0.3 
false
> function epsEqu(x, y) {
    return Math.abs(x - y) < Number.EPSILON;
}
> console.log(epsEqu(0.1+0.2, 0.3)); // true
```
- Number.isInteger(num)

```
> Number.isInteger(1.05)
false
> Number.isInteger(1)
true

> Number.isInteger(-3.1)
false
> Number.isInteger(-3)
true
```
- Number.isSafeInteger(num) In the range (−2^53, 2^53)
- Number.MIN\_SAFE\_INTEGER & Number.MAX\_SAFE\_INTEGER

```
> Math.pow(2, 53)
9007199254740992

> 9007199254740992
9007199254740992
> 9007199254740993
9007199254740992
> 9007199254740994
9007199254740994
> 9007199254740995
9007199254740996
> 9007199254740996
9007199254740996
> 9007199254740997
9007199254740996

> 9007199254740990 + 3
9007199254740992
> Number.isSafeInteger(9007199254740990)
true
> Number.isSafeInteger(3)
true
> Number.isSafeInteger(9007199254740992)
false

> 9007199254740995 - 10
9007199254740986

> Number.isSafeInteger(9007199254740995)
false
> Number.isSafeInteger(10)
true
> Number.isSafeInteger(9007199254740986)
true

isSafeInteger(a) && isSafeInteger(b) && isSafeInteger(a op b)
```
- Number.isNaN(num)

```
> const x = NaN;
> x !== x
true

> const x = NaN;
> isNaN(x)
true

> isNaN('???')
true
> Number.isNaN('???')
false
```
- Number.isFinite

```
> Number.isFinite(Infinity)
false
> Number.isFinite(-Infinity)
false
> Number.isFinite(NaN)
false
> Number.isFinite(123)
true

> Number.isFinite('123')
false
> isFinite('123')
true
```

### New Math methods
- Math.sign(num)

```
> Math.sign(-8)
-1
> Math.sign(0)
0
> Math.sign(3)
1
> Math.sign(NaN)
NaN

> Math.sign(-Infinity)
-1
> Math.sign(Infinity)
1
```
- Math.trunc(num)

```
> Math.trunc(3.1)
3
> Math.trunc(3.9)
3
> Math.trunc(-3.1)
-3
> Math.trunc(-3.9)
-3
```
- Math.cbrt(x)

```
> Math.cbrt(8)
2
```
- Math.expm1(x), Math.log1p(x)
- Math.log10(num)
- Math.fround(x), Math.imul(x, y)
- Math.clz32(x)

```
> Math.clz32(0b01000000000000000000000000000000)
1
> Math.clz32(0b00100000000000000000000000000000)
2
> Math.clz32(2)
30
> Math.clz32(1)
31
```
- Math.sinh(x), Math.cosh(x), Math.tanh(x), Math.asinh(x), Math.acosh(x), Math.atanh(x)
- Math.hypot([value1[, value2[, ...]]])

### How can I use integers beyond JavaScript’s 53 bit range
- Use string for IDs
- Use libraray e.g. [decimal.js](https://github.com/MikeMcl/decimal.js/)