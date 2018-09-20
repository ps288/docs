---
keywords: at, backslash, bang, dash, dot, dollar, hash, kdb+, operator, overload, pound, q, query, quote, quote-colon, slash, underscore, unary
---

# Overloaded operators




Many non-alphabetic keyboard characters are overloaded.
Operator overloads are resolved by **rank**, and sometimes by the **type** of argument/s. 


## `@` at

rank | syntax          | semantics
:---:|-----------------|-------------------------------
2    | `l@i`, `@[l;i]` | [Index At](apply.md#index)
2    | `f@y`, `@[f;y]` | [Apply At](apply.md#apply-at-index-at)
3    | `@[f;y;e]`      | [Trap At](apply.md#trap)
3    | `@[d;i;u]`      | [Amend At](amend.md)
4    | `a[d;i;m;my]`   | [Amend At](amend.md)
4    | `a[d;i;:;y]`    | [Replace At](amend.md)


## `\` backslash

rank | syntax                 | semantics
:---:|------------------------|---------------------------------------
n/a  | `\`                    | ends multiline comment
n/a  | `\`                    | abort
1    | `(f\)`, `f\[d]`        | [Converge](progressors.md#converge)
2    | `n f\d`, `f\[n;d]`     | [Repeat](progressors.md#do)
2    | `t f\d`, `f\[t;d]`     | [While](progressors.md#while)
2    | `x g\y`, `g\[x;y;z;…]` | [map-reduce](progressors.md#binary-maps)

```txt
d: data              n: non-negative integer
f: unary map         t: test map
g: map rank>1        x: atom or vector
                     y, z…: conformable atoms or lists
```


## `!` bang

rank | syntax            | semantics
:---:|-------------------|---------------------------------
2    | `x!y`             | [Dict](dict.md): make a dictionary
2    | `i!ts`            | [Enkey](enkey.md): make a simple table keyed
2    | `0!tk`            | [Unkey](enkey.md#unkey): make a keyed table simple
2    | `noasv!iv`        | [Enumeration](enumeration.md) from index
2    | `sv!h`            | [Flip Splayed or Partitioned](flip-splayed.md)
2    | `0N!y`            | [display](display.md) `y` and return it
2    | `-i!y`            | [internal function](../basics/internal.md)
4    | `![t;c;b;a]`      | [Update, Delete](../basics/funsql.md)

```txt
a: select specifications
b: group-by specifications
c: where-specifications
h: handle to a splayed or partitioned table
i: integer >0
i0: integer ≥0
noasv: symbol atom, the name of a symbol vector
sv: symbol vector
t: table
tk: keyed table
ts: simple table
x,y: same-length lists
```


## `-` dash

Syntax: immediately left of a number, indicates its negative.
```q
q)neg[3]~-3
1b
```
Otherwise

rank | example         | semantics
:---:|-----------------|-------------------------------------------
2    | `2-3`           | [Subtract](subtract.md)


## `.` dot

rank | syntax              | semantics
:---:|---------------------|---------------------------------------
2    | `l . i`, `.[l;i]`   | [Index](apply.md#apply-index)
2    | `g . gx`, `.[g;gx]` | [Apply](apply.md#apply-index)
3    | `.[g;gx;e]`         | [Trap](apply.md#trap)
3    | `.[d;i;u]`          | [Amend](amend.md)
4    | `.[d;i;m;my]`       | [Amend](amend.md)
4    | `.[d;i;:;y]`        | [Replace](amend.md)



## `$` dollar

rank | example                               | semantics
:---:|---------------------------------------|---------------------------------------
3    | `$[x>10;y;z]`                         | [Cond](cond.md): conditional evaluation
2    | `"h"$y`, `` `short$y``, `11$y`        | [Cast](cast.md): cast datatype
2    | `"H"$y`, `-11$y`                      | [Tok](tok.md): interpret string as data
2    | `x$y`                                 | [Enumerate](enumerate.md): enumerate `y` from `x`
2    | `10$"abc"`                            | [Pad](pad.md): pad string
2    | `(1 2 3f;4 5 6f)$(7 8f;9 10f;11 12f)` | dot product, matrix multiply, [`mmu`](mmu.md)


## `#` hash

rank | example         | semantics
:---:|-----------------|---------------------------------
2    | `2 3#til 6`     | [Take](take.md)
2    | `s#1 2 3`       | [Set Attribute](set-attribute.md)


## `?` query

rank | example                     | semantics
:---:|-----------------------------|----------------------------------------------------
2    | `"abcdef"?"cab"`            | [Find](find.md) `y` in `x`
2    | `10?1000`, `5?01b`          | [Roll](roll-deal.md#roll)
2    | `-10?1000`, ``-1?`yes`no``  | [Deal](roll-deal.md#deal)
2    | `x?v`                       | extend an enumeration: [Enum Extend](enum-extend.md)
3    | `?[11011b;"black";"frame"]` | [Vector Conditional](vector-conditional.md)
4    | `?[t;b;c;a]`                | [Select](../basics/funsql.md#select), [Exec](../basics/funsql.md#exec)
4    | `?[t;i;x]`                  | [Simple exec](../basics/funsql.md#simple-exec)


## `'` quote

rank | syntax                                    | semantics
:---:|-------------------------------------------|-------------------------------------------
1    | `(f')x`, `f'[x]`, `x ff'y`,  `ff'[x;y;…]` | [Each](distributors.md#each): iterate `ff` itemwise
1    | `'msg`                                    | [Signal](signal.md) an error
1    | `iv'[x;y;…]`                              | [Case](case.md): successive items from lists
2    | `'[ff;f]`                                 | [Compose](compose.md) `ff` with `f`

```txt
f:  unary map         msg: symbol or string
ff: map of rank ≥1    x, y: data
iv: int vector
```


## `':` quote-colon

rank | example  | semantics
:---:|----------|-------------------------------------------------------
1    | `f':`    | [Each Parallel](distributors.md#each-parallel) with unary `f`
1    | `g':`    | [Each Prior](distributors.md#each-prior) with binary `g`


## `/` slash

rank | syntax              | semantics
:---:|---------------------|-----------------------------------------
n/a  | `/a comment`        | comment: ignore rest of line
1    | `(f/)y`, `f/[y]`    | [Converge](progressors.md#converge) 
1    | `n f/ y`, `f/[n;y]` | [Repeat](progressors.md#do) 
1    | `t f/ y`, `f/[t;y]` | [While](progressors.md#while) 
1    | `(ff/)y`, `ff/[y]`  | [map-reduce](progressors.md#binary-maps): reduce a list or lists

```txt
f: unary map       t: test map     
ff: map rank ≥1    y: list
n: int atom ≥0
```

Syntax: a space followed by `/` begins a **trailing comment**. Everything to the right of `/` is ignored. 

```q
q)2+2 / we know this one
4
```

A `/` at the beginning of a line marks a **comment line**. The entire line is ignored. 

```q
q)/nothing in this line is evaluated
```

In a script, a line with a solitary `/` marks the beginning of a **multiline comment**. A multiline comment is terminated by a `\` or the end of the script.

```q
/
A script to add two numbers.
Version 2018.1.19
\
2+2
/
That's all folks.
```


## `_` underscore

rank | example      | semantics
:---:|--------------|-------------------------
2    | `3_ til 10`  | [Cut](cut.md), [Drop](drop.md)

!!! warning "Names can contain underscores"

    Best practice is to use a space to separate names and the Cut and Drop operators.


## Unary forms

Many of the operators tabulated above have unary forms in k. 

<i class="far fa-hand-point-right"></i> [Exposed infrastructure](../basics/exposed-infrastructure.md#unary-forms)

