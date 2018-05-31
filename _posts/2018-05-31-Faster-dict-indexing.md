---
layout: post
title:  "Python Optimizations: Are Nested Dict's or Dict's with Tuples for Key's quicker?"
tags: software python speed-test optimization
---

`Dict[Dict[Any, Any]]` vs Dict[Tuple[Any, Any]]

Which is faster in python? A Dict with tuples as keys or a dict of dict's? TLDR: A dict of tuples, but only by a little bit!

The test:

```
from timeit import timeit

def dict_test():
    d = {}
    for i in range(1, 1000):
        d[(i, i*5)] = i
    
    for i in range(1,1000):
        d[(i, i*5)]
        
def dict_test2():
    d = {}
    for i in range(1, 1000):
        if i not in d:
            d[i] = {}
        d[i][i*5] = i
    
    for i in range(1,1000):
        d[i][i*5]

        
print("dict_test took: {}s".format(timeit(dict_test, number=10000)))
print("dict_test2 took: {}s".format(timeit(dict_test2, number=10000)))
```

The result:

```
dict_test took: 3.9785058770678177s
dict_test2 took: 4.405024016745074s
```
