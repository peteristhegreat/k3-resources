# SELECTION
```
d @ i          Index (At)
                 Returns i with atoms replaced by values drawn from d,
                 a list, directory or dictionary, according to i, indices or
                 symbols as appropriate.
d . i          Index (Of)
                 Returns items from d, a list, directory or dictionary. A
                 vector i returns one item-at-depth; otherwise results
                 are cross-sectional. A null value means “all”.
d[i]           Select items.
d[j;k;…]       Select items at depth.
```
# STRUCTURAL
```
@ x            Atom    Is x an atom?
# x            Count   Number of items.
^ x            Shape   Extent of rectangularity.
x # y          Reshape Make rectangles of atoms or lists.
, x            Enlist  Form list.
x _ y          Drop    Drops x items from an end of y.
               Cut     Break y into pieces at indices x.
* x            First   First item.
+ x            Flip    Transpose top two levels of x.
x ! y          Rotate  Move x items from one end of y to
                       the other.
| x            Reverse Reverse order of items.
x , y          Join    Join atoms or lists together.
```
# ARITHMETIC
```
x + y          Plus    x plus y.
x - y          Minus   x minus y.
- x            Negate
x * y          Times   x times y.
x % y          Divide  x divided by y. Note 0 % 0 is 0.
% x            Reciprocal
                       Reciprocal of x.
x ^ y          Power   x to the power y.
x ! y          Mod     y residue of x.
_ x            Floor   Largest integer not greater than x.
x < y          Less    Is x less than y?
x > y          More    Is x greater than y?
x | y          Max     Larger atom (boolean OR).
x & y          Min     Smaller atom (boolean AND).
~ x            Not     0 = x for numeric x.
```
# COMPARISON
```
x = y          Equal   Are atoms of x and y tolerantly equal?
x ~ y          Match   Does x match y?
x ? y          Find    First location of y among items of x.
```
# FUNCTION APPLICATION
```
f @ x          Apply   Monadic
               Applies monadic function to value. e.g. {x^2}@3
f.x            Apply
               Applies function of any valence to appropriate value.
                 e.g.          f0._n f5.(a;b;c;d;e)
                 Related forms:
                               f[j;k;…] f[]
f ? y          Inverse
?[f;y;xinit]   Finds roots of y = f [x] using secant method optionally
                 starting at xinit.
.[f;x;:]       Trap          Traps errors when f is applied to x.
@[f;x;:]                     (0;result)       or
                             (1;error text)
:[c;expr;f]    Conditional : [c1;e1;c2;e2;… cn;en;f]
                             do[n;e1;…;en]
                             if[c;e1;e2;…;en]
                             while[c;e1;e2;…;en]
```
