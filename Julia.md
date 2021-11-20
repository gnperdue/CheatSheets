
### element-wise assignment

```
tmpd = Dict([1, 2, 3] .=> ["one", "two", "three"])
```

### element-wise function call

```
typeof.([1, 1.0, "one"])
```

### inline latex examples

```
f\_1<tab>
1 \in<tab> [1, 2, 3]
```

### anonymous function

```
x->sin(x)
(x->sin(x))(\pi<tab> / 2)
# call with, e.g. rot(pi/2)([1, 0])
rot(t) = ((x,y),) -> [cos(t)*x + sin(t)*y, -sin(t)*x + cos(t)*y]
# another way, call with `rot(pi/2)([1, 0])`
rot(t) = ((x, y),) -> [cos(t) sin(t); -sin(t) cos(t)]*[x, y]
```

### matrix product conventions

```
[1 2] * [1, 2]   # == 5
```