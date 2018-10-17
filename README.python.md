# Math-as-code

---

This is a reference to ease developers into mathematical notation by showing comparisons with Python code.

Motivation: Acedemic papers can be intimidation for younger people and this helps people to learn the syntax within a language. This is also becuase I saw another version for JavaScript and people were asking for a Python Version.

This guide it not yet finished. If you see errors or want to contribute please *OPEN A TICKET* or send a PR.

#Foreword


Mathematical symbols can mean different things depending on the author, context and the field of study (linear algebra, set theory, etc). This guide may not cover *all* uses of a symbol. In some cases, real-world references (blog posts, publications, etc) will be cited to demonstrate how a symbol might appear in the wild.

For a more complete list, refer to [Wikipedia - List of Mathematical Symbols](https://en.wikipedia.org/wiki/List_of_mathematical_symbols).

For simplicity, many of the code examples here operate on floating point values and are not numerically robust. For more details on why this may be a problem, see [Robust Arithmetic Notes](https://github.com/mikolalysenko/robust-arithmetic-notes) by Mikola Lysenko.

# Contents

---



## Equals Symbols

There are a number of symbols resembling the equals sign `=`. Here are a few common examples.

- `=` is for equality (values are the same)
- `≠` is for inequality (value are not the same)
- `=` is for definition (A is defined as B)

In Python:

```python
# equality
2==3

# ineqiality
2!=3
```

For example, the following defines x to be another name for 2kj

`x=2kj`

In Python, we might use this to *define* and provide aliases:

```python
x = 2 * k * j
```

However, this is mutable, and only takes a snapshot of the values at that time. Some languages have pre-processor, for example JavaScript but unfortunately not python.

## Square Root and Complex Numbers

A square root operation is on the form:

(√x)^2^ = x

In programming we use the sqrt function, like so:

```python
import math
x = 9
math.sqrt(x)
```

## Dot & Cross

The `•` and `x` symbols have different uses depending on context.

They might seem obvious, but it's important to understand the subtle differences before we continue into other sections.

#### Scalar Multiplication

Both symbols can represent simple multiplication of scalars. The following are equivalent.

$5•4=5\times4$

In programming languages we tend to use asterisk for multiplication:

```python
result = 5*4
```

Often the multiplication sign is only used to avoid ambiguity (e.g. between two numbers). Here, we can omit it entirely.

`skj`

If these variables represent scalars, the code would be:

```python
result = 3*k*j
```

#### Vector Multiplication

To denote multiplication of one vector with a scalar, or element-wise multiplication of a vector with another vector, we typically do not use the dot `·` or cross `×` symbols. These have different meanings in linear algebra, discussed shortly.

Let's take our earlier example but apply it to vectors. For element-wise vector multiplication, you might see an open dot `∘`to represent the [Hadamard product](https://en.wikipedia.org/wiki/Hadamard_product_%28matrices%29).[^2^](http://buzzard.ups.edu/courses/2007spring/projects/million-paper.pdf) 

`3k∘j`

In other instances, the author might explicitly define a different notation, such as a circled dot `⊙` or a filled circle `●`.[^3^](https://www.math.washington.edu/~morrow/464_12/fft.pdf)

Here is how it would look in code, using arrays `[x, y]` to represent the 2D vectors.

```python
s = 3
k = [ 1, 2 ]
j = [ 2, 3 ]

tmp = multiply(k, j)
result = multiplyScalar(tmp, s)
# => [ 6, 18 ]
```

Our `multiply` and `multiplyScalar` functions look like this:

```python
def multiply(a, b):
    return [ a[0] * b[0], a[1] * b[1] ]

def multiplyScalar(a, scalar):
    return [ a[0] * scalar, a[1] * scalar ]
```

Similarly, matrix multiplication typically does not use the dot `·` or cross symbol `×`. Matrix multiplication will be covered in a later section.

#### Dot Product

The dot symbol `·` can be used to denote the [*dot product*](https://en.wikipedia.org/wiki/Dot_product) of two vectors. Sometimes this is called the *scalar product* since it evaluates to a scalar.

`k · j`

It is a very common feature of linear algebra, and with a 3D vector it might look like this:

```python
k = [ 0, 1, 0 ]
j = [ 1, 0, 0 ]

d = dot(k, j)
# => 0
```

The result `0` tells us our vectors are perpendicular. Here is a `dot` function for 3-component vectors:

```python
def dot(a, b) {
  return a[0] * b[0] + a[1] * b[1] + a[2] * b[2]
}
```

#### Cross Product

The cross symbol `×` can be used to denote the [*cross product*](https://en.wikipedia.org/wiki/Cross_product) of two vectors.

`k × j`

In code, it would look like this:

```python
k = [ 0, 1, 0 ]
j = [ 1, 0, 0 ]

result = cross(k, j)
# => [ 0, 0, -1 ]
```

Here, we get `[ 0, 0, -1 ]`, which is perpendicular to both **k** and **j**.

Our `cross` function:

```python
def cross(a, b):
  ax = a[0], ay = a[1], az = a[2],
  bx = b[0], by = b[1], bz = b[2]
    
  var rx = ay * bz - az * by
  var ry = az * bx - ax * bz
  var rz = ax * by - ay * bx
  return [ rx, ry, rz ]
```

## Sigma

The big Greek `Σ` (Sigma) is for [Summation](https://en.wikipedia.org/wiki/Summation). In other words: summing up some numbers.

[![sigma](https://camo.githubusercontent.com/1f31963cf5b15c15b983a1f18167656ebb4481d9/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f25354373756d5f253742692533443125374425354525374231303025374469)](https://camo.githubusercontent.com/1f31963cf5b15c15b983a1f18167656ebb4481d9/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f25354373756d5f253742692533443125374425354525374231303025374469)

Here, `i=1` says to start at `1` and end at the number above the Sigma, `100`. These are the lower and upper bounds, respectively. The *i* to the right of the "E" tells us what we are summing. In code:

```python
sum = 0
for (var i = 1; i <= 100; i++):
  sum += i
```

The result of `sum` is `5050`.

**Tip:** With whole numbers, this particular pattern can be optimized to the following:

```python
n = 100 // upper bound
sum = (n * (n + 1)) / 2
```

Here is another example where the *i*, or the "what to sum," is different:

[![sum2](https://camo.githubusercontent.com/3f45ea96c7b91c06fb1debd738cdf4de058f1fbf/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f25354373756d5f253742692533443125374425354525374231303025374425323832692b31253239)](https://camo.githubusercontent.com/3f45ea96c7b91c06fb1debd738cdf4de058f1fbf/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f25354373756d5f253742692533443125374425354525374231303025374425323832692b31253239)

In code:

```python
sum = 0
for (var i = 1; i <= 100; i++):
  sum += (2 * i + 1)
```

The result of `sum` is `10200`.

The notation can be nested, which is much like nesting a `for` loop. You should evaluate the right-most sigma first, unless the author has enclosed them in parentheses to alter the order. However, in the following case, since we are dealing with finite sums, the order does not matter.

[![sigma3](https://camo.githubusercontent.com/35ce9ca0da4e41f198815955792e5ea810fa0ab0/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f25354373756d5f25374269253344312537442535452537423225374425354373756d5f2537426a253344342537442535452537423625374425323833696a253239)](https://camo.githubusercontent.com/35ce9ca0da4e41f198815955792e5ea810fa0ab0/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f25354373756d5f25374269253344312537442535452537423225374425354373756d5f2537426a253344342537442535452537423625374425323833696a253239)

In code:

```python
sum = 0
for (var i = 1; i <= 2; i++):
  for (var j = 4; j <= 6; j++):
    sum += (3 * i * j)
```

Here, `sum` will be `135`

##Element


In set theory, the "element of" symbol `∈` and `∋` can be used to describe whether something is an element of a *set*. For example:

[![element1](https://camo.githubusercontent.com/df30d572f400919114971f14906157ede36e2bb8/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412533442535436c65667425323025354325374233253243392532433134253744253742253230253543726967687425323025354325374425324325323033253230253543696e25323041)](https://camo.githubusercontent.com/df30d572f400919114971f14906157ede36e2bb8/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412533442535436c65667425323025354325374233253243392532433134253744253742253230253543726967687425323025354325374425324325323033253230253543696e25323041)

Here we have a set of numbers *A* `{ 3, 9, 14 }` and we are saying `3` is an "element of" that set.

A simple implementation in ES5 might look like this:

```python
A = [3, 9, 14]
A.indexOf(3) >= 0 
# => true
```

The backwards `∋` is the same, but the order changes:

[![element2](https://camo.githubusercontent.com/0c1fd27b7998b4fc2e759a856d682248818149f2/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412533442535436c656674253230253543253742332532433925324331342537442537422532302535437269676874253230253543253744253243253230412532302535436e6925323033)](https://camo.githubusercontent.com/0c1fd27b7998b4fc2e759a856d682248818149f2/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412533442535436c656674253230253543253742332532433925324331342537442537422532302535437269676874253230253543253744253243253230412532302535436e6925323033)

You can also use the "not an element of" symbols `∉` and `∌` like so:

[![element3](https://camo.githubusercontent.com/c8abe8ab40f2d01448dfb30abce84c5be4d245e9/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412533442535436c656674253230253543253742332532433925324331342537442537422532302535437269676874253230253543253744253243253230362532302535436e6f74696e25323041)](https://camo.githubusercontent.com/c8abe8ab40f2d01448dfb30abce84c5be4d245e9/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412533442535436c656674253230253543253742332532433925324331342537442537422532302535437269676874253230253543253744253243253230362532302535436e6f74696e25323041)

## Function

[
Functions](https://en.wikipedia.org/wiki/Function_%28mathematics%29) are fundamental features of mathematics, and the concept is fairly easy to translate into code.

A function relates an input to an output value. For example, the following is a function:

[![function1](https://camo.githubusercontent.com/c52513cc6407e17d240da46e57b229877da1725f/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f7825354525374232253744)](https://camo.githubusercontent.com/c52513cc6407e17d240da46e57b229877da1725f/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f7825354525374232253744)

We can give this function a *name*. Commonly, we use `ƒ` to describe a function, but it could be named `A(x)` or anything else.

In code, we might name it `square` and write it like this:

```python
square (x):
    return Math.pow(x, 2)
```

Sometimes a function is not named, and instead the output is written.

[![function3](https://camo.githubusercontent.com/49c605174699789f9c4782be6c84598b7fb15e9e/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f792532302533442532307825354525374232253744)](https://camo.githubusercontent.com/49c605174699789f9c4782be6c84598b7fb15e9e/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f792532302533442532307825354525374232253744)

In the above example, *x* is the input, the relationship is *squaring*, and *y* is the output.

Functions can also have multiple parameters, like in a programming language. These are known as *arguments* in mathematics, and the number of arguments a function takes is known as the *arity* of the function.

[![function4](https://camo.githubusercontent.com/c9b6aec0512e7ffeb2875355321cb0eee2fb2790/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6625323878253243792532392532302533442532302535437371727425374278253545322532302b2532307925354532253744)](https://camo.githubusercontent.com/c9b6aec0512e7ffeb2875355321cb0eee2fb2790/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6625323878253243792532392532302533442532302535437371727425374278253545322532302b2532307925354532253744)

In code:

```python
length(x, y):
    return Math.sqrt(x*x+y*y)
```

## Piecewise Function

Some functions will use different relationships depending on the input value, x.

### piecewise function

Some functions will use different relationships depending on the input value, *x*.

The following function *ƒ* chooses between two "sub functions" depending on the input value.

[![piecewise1](https://camo.githubusercontent.com/4d711083ee78682680776bb81b1d434deb13a852/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6625323878253239253344253230253543626567696e25374263617365732537442532302535436672616325374278253545322d7825374425374278253744253243253236253230253543746578742537426966253230253744253230782535436765712532303125354325354325323030253243253230253236253230253543746578742537426f7468657277697365253744253230253543656e642537426361736573253744)](https://camo.githubusercontent.com/4d711083ee78682680776bb81b1d434deb13a852/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6625323878253239253344253230253543626567696e25374263617365732537442532302535436672616325374278253545322d7825374425374278253744253243253236253230253543746578742537426966253230253744253230782535436765712532303125354325354325323030253243253230253236253230253543746578742537426f7468657277697365253744253230253543656e642537426361736573253744)

This is very similar to `if` / `else` in code. The right-side conditions are often written as **"for x < 0"** or **"if x = 0"**. If the condition is true, the function to the left is used.

In piecewise functions, **"otherwise"** and **"elsewhere"** are analogous to the `else` statement in code.

```python
def f (x):
  if (x >= 1):
    return (Math.pow(x, 2) - x) / x
  else:
    return 0
```

### common functions

There are some function names that are ubiquitous in mathematics. For a programmer, these might be analogous to functions "built-in" to the language (like `parseInt` in JavaScript).

One such example is the *sgn* function. This is the *signum* or *sign* function. Let's use [piecewise function](https://github.com/Jam3/math-as-code/blob/master/README.md#piecewise-function) notation to describe it:

[![sgn](https://camo.githubusercontent.com/bde33189e233da8d14caff29cd37b753acfee716/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f73676e25323878253239253230253341253344253230253543626567696e25374263617365732537442532302d312532362532302535437465787425374269662532302537442532307825323025334325323030253543253543253230302532432532302532362532302535437465787425374269662532302537442532302537427825323025334425323030253744253543253543253230312532432532302532362532302535437465787425374269662532302537442532307825323025334525323030253543253543253230253543656e642537426361736573253744)](https://camo.githubusercontent.com/bde33189e233da8d14caff29cd37b753acfee716/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f73676e25323878253239253230253341253344253230253543626567696e25374263617365732537442532302d312532362532302535437465787425374269662532302537442532307825323025334325323030253543253543253230302532432532302532362532302535437465787425374269662532302537442532302537427825323025334425323030253744253543253543253230312532432532302532362532302535437465787425374269662532302537442532307825323025334525323030253543253543253230253543656e642537426361736573253744)

In code, it might look like this:

```python
def sgn(x):
    if (x < 0): 
        return -1
	if(x > 0):
        return 1
    return 0
```

See [signum](https://github.com/scijs/signum) for this function as a module.

Other examples of such functions: *sin*, *cos*, *tan*.

## prime

The prime symbol (`′`) is often used in variable names to describe things which are similar, without giving it a different name altogether. It can describe the "next value" after some transformation.

For example, if we take a 2D point *(x, y)* and rotate it, you might name the result *(x′, y′)*. Or, the *transpose* of matrix **M**might be named **M′**.

In code, we typically just assign the variable a more descriptive name, like `transformedPosition`.

For a mathematical [function](https://github.com/Jam3/math-as-code/blob/master/README.md#function), the prime symbol often describes the *derivative* of that function. Derivatives will be explained in a future section. Let's take our earlier function:

[![function2](https://camo.githubusercontent.com/3a3cf66b5b499217fb372164cfff5f329a4ccc83/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f662535436c6566742532302532387825323025354372696768742532302532392532302533442532307825354525374232253744)](https://camo.githubusercontent.com/3a3cf66b5b499217fb372164cfff5f329a4ccc83/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f662535436c6566742532302532387825323025354372696768742532302532392532302533442532307825354525374232253744)

Its derivative could be written with a prime `′` symbol:

[![prime1](https://camo.githubusercontent.com/8c232c6f8f62f1053a286e239e5cff6311f79582/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f66253237253238782532392532302533442532303278)](https://camo.githubusercontent.com/8c232c6f8f62f1053a286e239e5cff6311f79582/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f66253237253238782532392532302533442532303278)

In code:

```python
def f(x):
    return Math.pow(x, 2)
def fPrime(x):
    return 2*x
```

Muliple prime symbols can be used to describe the second derivative *ƒ′′* and third derivative *ƒ′′′*. After this, authors typically express higher orders with roman numerals *ƒ*IV or superscript numbers *ƒ*(n).

## Floor & Ceiling


The special brackets `⌊x⌋` and `⌈x⌉` represent the *floor* and *ceil* functions, respectively.

[![floor](https://camo.githubusercontent.com/1944854fb34d626c8382c000efc7f1d7b2dc00c6/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f666c6f6f72253238782532392532302533442532302535436c666c6f6f722532307825323025354372666c6f6f72)](https://camo.githubusercontent.com/1944854fb34d626c8382c000efc7f1d7b2dc00c6/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f666c6f6f72253238782532392532302533442532302535436c666c6f6f722532307825323025354372666c6f6f72)

[![ceil](https://camo.githubusercontent.com/69dab24d14e0f917388c199b79068d63406c071f/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6365696c253238782532392532302533442532302535436c6365696c25323078253230253543726365696c)](https://camo.githubusercontent.com/69dab24d14e0f917388c199b79068d63406c071f/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6365696c253238782532392532302533442532302535436c6365696c25323078253230253543726365696c)

In code:

```python
Math.floor(x)
Math.ceil(x)
```

When the two symbols are mixed `⌊x⌉`, it typically represents a function that rounds to the nearest integer:

[![round](https://camo.githubusercontent.com/41315bd2407284c586fe41fcb881fdfe55136b21/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f726f756e64253238782532392532302533442532302535436c666c6f6f7225323078253230253543726365696c)](https://camo.githubusercontent.com/41315bd2407284c586fe41fcb881fdfe55136b21/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f726f756e64253238782532392532302533442532302535436c666c6f6f7225323078253230253543726365696c)

In code:

```python
Math.round(x)
```

## Arrows

Arrows are often used in [function notation](https://github.com/Jam3/math-as-code/blob/master/README.md#function-notation). Here are a few other areas you might see them.

#### Material Implication

Arrows like `⇒` and `→` are sometimes used in logic for *material implication.* That is, if A is true, then B is also true.

[![material1](https://camo.githubusercontent.com/9ab50b0638996aa9caa0958ec65d5968abc4e8d0/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f4125323025354352696768746172726f7725323042)](https://camo.githubusercontent.com/9ab50b0638996aa9caa0958ec65d5968abc4e8d0/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f4125323025354352696768746172726f7725323042)

Interpreting this as code might look like this:

```python
if (A==true):
    print(B==true)
```

The arrows can go in either direction `⇐` `⇒`, or both `⇔`. When *A ⇒ B* and *B ⇒ A*, they are said to be equivalent:

[![material-equiv](https://camo.githubusercontent.com/0e4bacbe2ba0163121b1e2bd4d9d1bf479bc4506/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412532302535434c65667472696768746172726f7725323042)](https://camo.githubusercontent.com/0e4bacbe2ba0163121b1e2bd4d9d1bf479bc4506/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412532302535434c65667472696768746172726f7725323042)

#### Equality

In math, the `<` `>` `≤` and `≥` are typically used in the same way we use them in code: *less than*, *greater than*, *less than or equal to* and *greater than or equal to*, respectively.

```python
50 > 2 == true
2 < 10 == true
3 <= 4 == true
4 >= 4 == true
```

On rare occasions you might see a slash through these symbols, to describe *not*. As in, *k* is "not greater than" *j*.

[![ngt](https://camo.githubusercontent.com/92d366f4dbdc8df291a2bc0d54a0fdd0b4d70572/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6b2532302535436e6774722532306a)](https://camo.githubusercontent.com/92d366f4dbdc8df291a2bc0d54a0fdd0b4d70572/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6b2532302535436e6774722532306a)

The `≪` and `≫` are sometimes used to represent *significant* inequality. That is, *k* is an [order of magnitude](https://en.wikipedia.org/wiki/Order_of_magnitude) larger than *j*.

[![orderofmag](https://camo.githubusercontent.com/28fbdb2ec8403248545f618a6225b04edd5206c6/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6b25323025354367672532306a)](https://camo.githubusercontent.com/28fbdb2ec8403248545f618a6225b04edd5206c6/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6b25323025354367672532306a)

In mathematics, *order of magnitude* is rather specific; it is not just a "really big difference." A simple example of the above:

```python
orderOfMagnitude(k) > orderOfMagnitude(j)
```

And below is our `orderOfMagnitude` function, using [Math.trunc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/trunc) (ES6)

```python
def log10(n):
  # logarithm in base 10
  return Math.log(n) / Math.LN10

def orderOfMagnitude (n):
  return Math.trunc(log10(n))
```

*Note:* This is not numerically robust.

See [math-trunc](https://www.npmjs.com/package/math-trunc) for a ponyfill in ES5.

#### conjunction & disjunction

Another use of arrows in logic is conjunction `∧` and disjunction `∨`. They are analogous to a programmer's `AND` and `OR`operators, respectively.

The following shows conjunction `∧`, the logical `AND`.

[![and](https://camo.githubusercontent.com/46d6409a084320e86eca19f5213f0fa915dc47d5/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6b253230253345253230322532302535436c616e642532306b253230253343253230342532302535434c65667472696768746172726f772532306b25323025334425323033)](https://camo.githubusercontent.com/46d6409a084320e86eca19f5213f0fa915dc47d5/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f6b253230253345253230322532302535436c616e642532306b253230253343253230342532302535434c65667472696768746172726f772532306b25323025334425323033)

In JavaScript, we use `&&`. Assuming *k* is a natural number, the logic implies that *k* is 3:

```python
if (k > 2 && k < 4):
    print(k == 3)
```

Scince both sides are  `⇔`, it also implies the following:

```python
if (k==3):
    print(k > 2 and k < 4)
```

The down arrow `∨` is logical disjunction, like the OR operator.

[![logic-or](https://camo.githubusercontent.com/9cde27f24db029b4b65c5bf6337755f48b1f847e/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412532302535436c6f7225323042)](https://camo.githubusercontent.com/9cde27f24db029b4b65c5bf6337755f48b1f847e/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f412532302535436c6f7225323042)

In code:

```python
A || B
```

## Logical Negation

Occasionally, the `!` symbols are used to represent logical `NOT`. For example, *!A* is only true if A is false.

Here is a simple example using the *not* symbol:

[![negation](https://camo.githubusercontent.com/d22497c85ed75b9aa2c7ad456fab364eb3fc5de5/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f782532302535436e6571253230792532302535434c65667472696768746172726f772532302535436c6e6f742532387825323025334425323079253239)](https://camo.githubusercontent.com/d22497c85ed75b9aa2c7ad456fab364eb3fc5de5/687474703a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f782532302535436e6571253230792532302535434c65667472696768746172726f772532302535436c6e6f742532387825323025334425323079253239)

An example of how we might interpret this in code:

```python
if (x != y):
    print(!(x==y))
```

*Note:* The tilde `~` has many different meanings depending on context. For example, *row equivalence* (matrix theory) or *same order of magnitude* (discussed in [equality](https://github.com/Jam3/math-as-code/blob/master/README.md#equality)).

##More...

Like this guide? Suggest some [more features](https://github.com/bubcool1/math-as-code/issues/1) or send us a Pull Request!

## ##Contributing

For details on how to contribute, see [COMTRIBUTING.md](https://github.com/Bubcool1/math-as-code/blob/master/CONTRIBUTING.md)

##Licence

MIT, see [LICENSE.md](http://github.com/Jam3/math-as-code/blob/master/LICENSE.md) for details.