# In Line Help

## \\  Help

```
\0       data
\+       verbs
\'       adverbs
\_       system verbs and nouns
\.       assign, define, control and debug
\:       i/o, dynamic load and client/server
\`       os commands, dialog boxes
\a       attributes, dependencies and triggers
\g       gui attributes
\l f     load script f.k
\s f     step script f.k
\w       workspace used, allocated, mapped
\c [0|1] console [off|on]
\e [0|1] error flag [off|on]
\b [t|s] break flag [trace|stop|none]
\d [d|^] k directory [go to]
\v [d|^] variables [directory]
\i [v]   invalid [antecedents/dependents]
\p [n]   print precision [digits]
\t [x]   time [x] milliseconds
\r [s]   random seed
\cd [d]  O/S directory [go to]
\[other] O/S execute
\\       exit    \(escape)    ctrl-c(stop)
```

## \\0  data

```
        Scalar  Vector  Empty   Inf     Null
integer 0       1 2     !0      0I      0N
float   0.0     1 2.0   0#0.0   0i      0n
char    " "     "12"    ""              "\0"
symbol  `       `a`b    0#`

lambda  {}
null    _n (_n@i and _n?i are i; _n`v is _n)
list    (x;y;z)  () is empty  ,... is list of one

dict    .((symbol;value;attributes);...)
 !d             symbols
 d[string]      execute
 d[`v]  d[]     values
 d[`v.] d[.]    attributes
 d.v  is  d`v  is  d[`v]  is  d@`v  is  d .,`v
 (also `d)

~`v     attribute handle (`v.)
4:x     type: atom(1 to 7)[ifcsdnx] list(0 to -4)[KIFCS]
5:x     ascii representation
```

## \\+  verbs

```
        Dyad            Monad
+       plus            flip
-       minus           negate
*       times           first
%       divide          reciprocal
&       min/and         where
|       max/or          reverse
<       less            upgrade
>       more            downgrade
=       equal           group
^       power           shape
!       mod/rotate      enumerate
~       match           not
,       join            enlist
#       take/reshape    count
_       drop/cut        floor
$       form/format     format
?       find/invert     unique  invert-guess
@       at              atom    m-amend d-amend
.       dot             value   m-amend d-amend

f[x]    is f .,x        is f@x  is f x
f[x;y]  is f .(x;y)
```

## \\'  adverbs

```
f'      EACH
d\:     EACHLEFT
d/:     EACHRIGHT
d':     EACHPRIOR
d/      OVER    f/[init;...]    RECUR
d\      SCAN    f\[init;...]    TRACE
m/ CONVERGE     n m/ DO         b m/ WHILE
m\ CONVERGE     n m\ DO         b m\ WHILE
f(function) d(dyadic) m(monadic) b(boolean)
scatter selection       matrix'
transitive closure      vector/ vector\
state transition        matrix/ matrix\ matrix':

compose         2+  8$  ~=  ~<  ~>  *|:(first reverse)
project         pv:{[c;t;d]+/c*d^t}  pv[c:.1 .1 1.1;t:1 2 3]d:%1.1
invert          pv[c;t]?.97  pv[c;;d]?.98  pv[;t;d]?.99
modify          @[0 0 0;1 1 0 2 2 0 1 2;+;!8]
iterate         9{+':0,x,0}\1  9(|+\)\1 1.0
converge        (1+%:)\1.0  {x\'!#x}parent:0 0 1 1 0
integrate       +\2 3 4  *\2 3 4
differentiate   -':0 2 5 9  %':1 2 6 24

verbs default to dyad. use(:) for monad, e.g. (<;<:)
```

## \\_  system verbs and nouns

```
Math:   _log _exp _abs _sqr _sqrt _floor _dot _mul _inv
        _sin _cos _tan _asin _acos _atan _sinh _cosh _tanh
        y _lsq A is least squares x for y~+/A*x (i.e. Ax=y)

Rand:   x _draw y (from !y); x _draw -y (deal from !y); x _draw 0 (from (0,1))

Time:   _t is gmt seconds. _lt is local from gmt, e.g. _gtime _lt _t
        _jd yyyymmdd (and _dj) for to and from julian day number (0 is monday)

List:   x _in y is 1 if x is an item of y; 0 otherwise (list: _lin)
        x _bin y is binary search for y in ascending x (list: _binl)
        x _dv y and x _di y to delete by value and index (list: _dvl)
        x _sv v (scalar from vector) and x _vs s (vector from scalar)
        _ci i (character from integer) and _ic c (integer from character)
        x _sm y is string match. y can have *?[^-], e.g. files _sm "*.[kK]"
        x _ss y is string/symbol search for start indices. y can have ?[^-].
        _ssr[x;y;z] is string/symbol search and replace. z can be a function.
        _bd d (bytes from data) and _db b (data from bytes). linear form.
        _getenv v (v _setenv s) gets(sets) environment variable v.
        _host addr; _host name; _size file; _exit code.

Vars:   _d(dir) _v(var) _i(index) _t(second) _f(function) _n(null) _s(space)
        _h(host) _p(port) _w(who) _u(user) _a(address) _k(version) _T(time)
```

## \\.  assign, define, control and debug

```
Dyad            D-Amend         Monad           M-amend
v::y (or v:y)   .[`v;();:;y]
v+:y            .[`v;();+;y]    v-:             .[`v;();-:]
v[i]+:y         .[`v;,i;+;y]    v[i]-:          .[`v;,i;-:]
v[i;j]+:y       .[`v;(i;j);+;y] v[i;j]-:        .[`v;(i;j);-:]

@[v;i;d;y] is .[v;,i;d;y]       @[v;i;m] is .[v;,i;m]

{[a;b;c] ...}   function definition
 x y z          default parameters
 d:...          local variable

control(debug: ctrl-c stop)
 :[c;t;f]       conditional
 if[c; ... ]
 do[n; ... ]
 while[c; ...]
 / ...          comment
 \ ...          trace(escape)
 : ...          return(resume)
 ' ...          signal

trap signals with .[f;(x;y;z);:] and @[f;x;:]
```

## \\:  i/o, dynamic load and client/server

```
!directory      list files(!"" root !"." current)
 0:f    f 0:x   read/write text(` for console)
 1:f    f 1:x   read/write data(default .l)
 6:f    f 6:x   read/write bytes
        f 5:x   append data, e.g. `log 5:,transaction

 (type;[,]delim)0:f     [names+]delimited text( IFCSDTZ)
 (type;width)0:f        fixedwidth text( IFCSDTZ)
 (type;width)1:f        fixedwidth data(cbsijfd IFCSDZMm)
 Blank skips. S strips. f can be (f;index;length).

 client/server, k f -i 2001     Callback(default)
  w:3:(m;port)  open            .m.u users(all)
  w 3:msg       set/asynch      .m.s function(.:)
  w 4:msg       get/synch       .m.g function(.:)
  3:w           close           .m.c expression("")

  .m.s .m.g and .m.c can access _w, _u(trunc to 8) and _a.
  m is `machine(localhost) or "ddd.ddd.ddd.ddd" or _a.
  default msg v, (v;i), (v;i;u) or (v;i;u;d). v can be string.
  can't write or message _fn, \kr fn or fn[;x]

 [f]2:(entry;argcount)  dynamic load
```

## \\`  os commands, dialog boxes

```
`3:string               os set command, e.g. `3:"k bck"
`4:string               os get command, e.g. `4:"dir"

dialog boxes
 f:`4:(`open;type[s][;title]) / (`open;`l`txt)
 f:`4:(`save;type[s][;title]) / (`save;`l`txt)
 x:`4:(`menu;IFS)             / (`menu;`a`b`c)
 b:`4:(`okcancel;line[s][;title])
   `4:(`ok;lines[s][;title])  / (`ok;("extreme";"speed"))
```

## \\a  attributes, dependencies and triggers

```
Attributes              Type

 h      help            string
 t      trigger         expression
 d      dependency      expression
 c      class(display)  symbol
         `data(default) atom, list, dict, list of lists, dict of lists
         `chart          as above where atom is list of y values
         `plot           as above where atom is matrix of (x;y) values
         `check         0 or 1
         `radio         symbol (one of ..o; see below)
         `button        expression or dictionary of expressions
         `form          dictionary of entries of any class(incl. `form)

Triggers neither self-invalidate nor refire.
Dependencies should have no side-effects and cannot loop.
Triggers, dependencies and attributes can access _d _v and _i.
Screen data updates can happen incrementally, i.e. change attrs first.
```

## \\g  gui attributes

```
`show$`v        show variable v
`hide$`v        hide variable v

 Display attributes (for variables that have class).
  x     width           integer(KFONT width)
  y     height          integer(KFONT height)
  a     arrangement     nest of symbols(class `form)
  o     options         list of symbols(class `radio)
  l     label           string
  kl    click label     string (also klr)

  Data-display attributes (for variables that have class `data).
  functions (monadic, constant or array)        default
   e    editable        0 or 1                   1
   f    format          string from data         11$(11.2$)
   g    getdata         data from string         0$ etc.
   u    update          update[old;new]          :
   fg   foreground      integer(rrggbb)          0
   bg   background      integer(rrggbb)         -1(808080)

  expressions/events (strings)
   ins, del, f1 ... f12, ctrl_a ... ctrl_z
   k, kr, kk    click, click right, double click(precludes e)
```
