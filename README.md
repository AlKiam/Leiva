# Breeze, the definitive low-level programming language
## Download & Installation
There are not actual releases, since this language is a prototype. 

## How Breeze works
Breeze is written primary in C++ and the Breeze's source code is translated into C and compiled with [gcc](https://github.com/gcc-mirror/gcc) (might port to LLVM in the future). This gives Breeze a powerful typed and the speed and the low-level of C.

Breeze is strongly influenced by Go and C (but mostly Go). But you'll ask... If is based in Go, why you don't use Go instead?

**various reasons:**
* Go only allows, manual memory allocation, but no deallocation. Breeze is focus on embedded systems, so I also want manual deallocation of memory while keeping simple the development.

* Make it more simple by removing not needed keywords such as ```var``` for defining variables. Variable creation would look like this ```t Type``` instead of ```var t Type```

* Improve performamce by using GCC as the backend of the compiler. Also promoting the use of optimization flags: `-O2`, `-Os`, `-s`... for better optimized code than, Go's.

* C is embedded into the language. You could simple call a C function or the C preprocesor with an '@': `@#include <math.h>` or `@sin(90)`

* Inlining. Don't need to call a function if you copy it's code into the source code, directly, whenever is called. This saves, time by avoiding function call overhead. Functions defined like this: `fn Sin(x f64) f64 = @sin(math.Deg(x))` will be inlined

* Built-In basic `print` and `println`. Also supports format by using `string` formatting.

* More...

##### How it works?
**compiler:**
```
Breeze
  └─ front-end
        └─ translation to C
             └─ gcc compiles the C source code
                  └─ executable
```

## Compilation

#### If you want to compile and create an executable of your code use:
```
breeze c <args> -o [executable_name]
```
**NOTE**: the `build` argument, gets all the `.bz` files at the directory, for compiling them.
## Examples
#### Hello World:
```
crate main

import "io"

fn main(args []string) {
  io.Printf("Hello, World!!!")
}
```
#### Structs:
```
crate main

import "io"

Map<K, V> struct {
  keys []K
  values []V
}

fn NewMap<K, V>() Map<K, V> {
  return Map<K, V>{}
}

fn (map Map<K, V>) Insert(key K, value V) error {
  map.keys, err := append(map.keys, key)
  if err != nil {
    map.values, err := append(map.values, value)
    return err
  }
  else {
    return err
  }
}

fn (map Map<K, V>) String() string { // Implicit operator
  str := "map"
  for i := 0; i < len(map.keys); i++ {
    io.Sprintf(str, "{%v, %v}", map.keys[i], map.values[i])
  }
}

fn main() {
  vertices1 := NewMap<string, i32>()
  vertices1.Insert("Triangle", 3)
  vertices1.Insert("Square", 4)
  io.Printf("%v\n", map)
}


```
#### Coroutines:
```
crate main

import "io"

fn fib(n u64, p pie u64) {
  x, y := 0, 1
  for i := 0; i < n; i++ {
    c <- x
    x, y  = y, x + y
  }
  close(p) // removes memory from channel and set it to 'nil'
}

fun main() {
  c := make(pipe u64, 16)
  rout := coroutine fib(16, c)

  for n := range c {
    io.Printf("%d\n", <- c)
  }
  join(rout) // join the routine
}
```
## Leiva by examples:
| Nº            | Tutorial      | Complexity      |
| ------------- |:-------------:|:---------------:|
| 1             | [Hello World!!!](https://github.com/AlKiam/Leiva/tree/master/Examples/Hello%20World) | Easy |
| 2             | [Primitives](https://github.com/AlKiam/Leiva/tree/master/Examples/Primitives) | Easy |
| 3             | [Pointers](https://github.com/AlKiam/Leiva/tree/master/Examples/Pointers) | Medium |
| 4             | [Custom types](https://github.com/AlKiam/Leiva/tree/master/Examples/Custom%20Types) | Easy |

###### Note:
A hipotetical new programming language. Syntax and functions are prototypes.
