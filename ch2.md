# Category Theory for Programmers Challenge Questions

## Chapter 2 - Types and Functions (Part One, Section 2)

#### 1. Define a higher-order function (or a function object) memoize in your favorite language. This function takes a pure function f as an argument and returns a function that behaves almost exactly like f, except that it only calls the original function once for every argument, stores the result internally, and subsequently returns this stored result every time it’s called with the same argument. You can tell the memoized function from the original by watching its performance. For instance, try to memoize a function that takes a long time to evaluate. You’ll have to wait for the result the first time you call it, but on subsequent calls, with the same argument, you should get the result immediately.
```python
def memoize(f):
    def f_memoized(*args):
        print("memoized call being made to ", f.__name__)
        if args not in f_memoized.cache:
            print("first time seeing args")
            f_memoized.cache[args] = f(*args)
        else:
            print("seen this before")
        return f_memoized.cache[args]
    f_memoized.cache = {}
    return f_memoized
```

#### 2. Try to memoize a function from your standard library that you normally use to produce random numbers. Does it work?
All the memoized calls return the same (non-random) number, so no, it no longer works as a random number generator.

#### 3. Most random number generators can be initialized with a seed. Implement a function that takes a seed, calls the random number generator with that seed, and returns the result. Memoize that function. Does it work?
The function always returns the same "random" number, so no, it doesn't work as a random number generator.

#### 4. Which of these C++ functions are pure? Try to memoize them and observe what happens when you call them multiple times: memoized and not.

##### 4(a)
```c++
int fact(int n) {
    int i;
    int result = 1;
    for (i = 2; i <= n; ++i)
        result *= i;
    return result;
}
```
Functionally pure (memoizing works fine). The "result" variable is mutated in the function, but since the overall function is still pure.

##### 4(b) 

```c++
std::getchar()
```
Not functionally pure, since the input is "unit" and the return type could be any character. Can't be memoized, since memoizing will just cause the return of the first character ever seen by getchar() for all subsequent calls.

##### 4(c)

```c++
bool f() { 
    std::cout << "Hello!" << std::endl;
    return true; 
}
```
Not functionally pure, since printing "Hello!" is a side-effect. Can't be memoized successfully; the memoized version would only print "Hello!" once and then simply return true on subsequent calls.

##### 4(d)

```c++
int f(int x)
{
    static int y = 0;
    y += x;
    return y;
}
```
This function is not pure since the value of y is preserved on subsequent calls by the "static" keyword. Memoizing this function will not work.

#### 5.  How many different functions are there from Bool to Bool ? Can you implement them all?
Two input states times two output states equals four possibilities.
```python
def bool_id(b):
    return b

def bool_invert(b):
    return not b

def bool_always(b):
    return True

def bool_never(b):
    return False
```
#### 6.  Draw a picture of a category whose only objects are the types Void , () (unit), and Bool ; with arrows corresponding to all possible functions between these types. Label the arrows with the names of the functions.
(drawing coming later)
Graphviz was overlapping the four self-loops on Bool, so I just labeled one self-loop with four names. They are really separate.
[(link to the graphviz code](misc/ch2question6.gv)
