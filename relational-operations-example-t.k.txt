/ relational operations - sa 2002.11.16

table:{[f;n;m]@[_n;f;{:[@y;n _draw y;y n _draw#y]};m]}

rows:{[t;i]@[t;_n;@[;i]]}
cols:{[t;f;g]@[_n;f;:;t g]}

group:{[t;k;f;o].+(k,{`$($x),"_",$y}'[o;f];,/(k;f){(. z)[t y]. x}[i t k]''`last,,o)}
 i:{[d](#?i;i:(?i)?/:i:(#:'u)_sv(u:?:'d)?/:'d)}
 count:{[d;n;i]@[&n;i;+;1]}
 sum:{[d;n;i]@[n#*0#d;i;+;d]}
 last:{[d;n;i]@[n#*0#d;i;:;d]}
 avg:{[d;n;i]sum[d;n;i]%count[d;n;i]}
 list:{[d;n;i]@[n#,();i;,;d]}

order:where:{[t;f;o]{x y z x}/[_n;o;t f]}
 desc:>:
 asc:<:

insert:{[t;d]@[t;_n;,;d]}
update:{[t;f;i;d].[t;(f;i);:;d]}
delete:{[t;i]@[t;_n;_di[;i]]}

\t t:table[`f`g`h`i`j;1000000;(`a`b`c`d`e;7;0;0;0)]
\t t:insert[t;(`a`b`b`a;3 5 6 2;.1*!4;.2*!4;.3*!4)]
\t u:rows[t;where[t;`f`g;({&x _lin`a`b};&5=)]]
\t v:rows[u;order[u;`g`f;`desc`asc]]
\t w:group[t;`f`g;`h`h`h`i;`count`sum`avg`sum]
\t x:rows[w;order[w;`g`f;`desc`asc]]

`show$'`t`u`v`w`x;

\

table[f;n;m] returns a table of cardinality n with cols f whose values are drawn from m
insert[t;d] returns t with d appended
update[t;f;i;d] returns t with cols f updated at i with d
delete[t;i] returns t with rows i deleted
rows[t;i] returns t restricted to rows i
cols[t;f;g] returns t with cols g of t projected to f
group[t;k;f;o] returns t with keys k and aggregations o[1]f[1] ... o[n]f[n]
where[t;f;o] returns indices of rows where o[1]f[1] and ... and o[n]f[n]
order[t;f;o] returns indices of rows sorted by o[1]f[1] within ... within o[n]f[n]

4 x slower:

group:{[t;k;f;o]@[_n;k,name'[f;o];:;(+?+t k),o@''t[f;=+t k]]}
 name:{[f;o]`$($o),"_",$f}
 avg:{(+/x)%#x}
 sum:+/
 count:#:
 list:(::)
