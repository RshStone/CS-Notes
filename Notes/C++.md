## 刷题使用感受对比

1. `cpp`: `vector<0, 0> (0, 0)`    `new int[0]`  

   `java`: `new int[0]` `Arrays.fill(nums, 0)`; `nums` is an array.

2. `cpp`: `std::min(a, b)`

   `java`: `Math.min(a,b)`

3. `cpp:` `String s` `s[i]`

   `java`: `String s` `s.charAt(i)`   `char[] arr = s.toCharArray()`

4. 

##  刷题简单入门

reference: liuchuo 会C的基础上如何快速入门cpp



## 资源

rthuang https://github.com/huangrt01/CS-Notes/blob/master/Notes/C%2B%2B.md

各种资源

- [大神 Andrei Alexandrescu 的 ppt，讲C语言优化](https://www.slideshare.net/andreialexandrescu1/three-optimization-tips-for-c-15708507)
- https://github.com/miloyip/itoa-benchmark/
- https://www.cplusplus.com/doc/tutorial/

- 《Effective Modern C++》, Scott Meyers

## 简单入门

The storage for variables with *global* or *namespace scope* is allocated for the entire duration of the program. This is known as *static storage*, and it contrasts with the storage for *local variables* (those declared within a block). These use what is known as automatic  storage. The storage for local variables is only available during the  block in which they are declared; after that, that same storage may be  used for a local variable of some other function, or used otherwise.

But there is another substantial difference between variables with *static storage* and variables with *automatic storage*:
 \- Variables with *static storage* (such as global variables) that are not explicitly initialized are automatically initialized to zeroes.
 \- Variables with *automatic storage* (such as local variables) that are not explicitly initialized are left uninitialized, and thus have an undetermined value.

library arrays

CPP刷题性能简直爆表，给很大的反馈和鼓励性。

Confused:

```c++
int x;
      int *       p1 = &x;  // non-const pointer to non-const int
const int *       p2 = &x;  // non-const pointer to const int
      int * const p3 = &x;  // const pointer to non-const int
const int * const p4 = &x;  // const pointer to const int 
```

the *scope operator* (`::`, two colons)

```cpp
// classes and uniform initialization
#include <iostream>
using namespace std;

class Circle {
    double radius;
  public:
    Circle(double r) { radius = r; }
    double circum() {return 2*radius*3.14159265;}
};

int main () {
  Circle foo (10.0);   // functional form
  Circle bar = 20.0;   // assignment init.
  Circle baz {30.0};   // uniform init.
  Circle qux = {40.0}; // POD-like

  cout << "foo's circumference: " << foo.circum() << '\n';
  return 0;
}
```

