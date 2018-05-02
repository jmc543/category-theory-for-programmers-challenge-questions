# Category Theory for Programmers Challenge Questions

## Chapter Two - Types and Functions (Part One, Section Two)

#### 1. Define a higher-order function (or a function object) memoize in your favorite language. This function takes a pure function f as an argument and returns a function that behaves almost exactly like f, except that it only calls the original function once for every argument, stores the result internally, and subsequently returns this stored result every time it’s called with the same argument. You can tell the memoized function from the original by watching its performance. For instance, try to memoize a function that takes a long time to evaluate. You’ll have to wait for the result the first time you call it, but on subsequent calls, with the same argument, you should get the result immediately.
```python
def memoize(f):
    def f_memoized(*args):
        print("memoized call being made")
        if args not in f_memoized.cache:
            print("first time seeing args")
            f_memoized.cache[args] = f(*args)
        else:
            print("seen this before")
        return f_memoized.cache[args]
    f_memoized.cache = {}
    return f_memoized
```
