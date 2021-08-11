rthuang https://github.com/huangrt01/CS-Notes/blob/master/Notes/C%2B%2B.md

[toc]

各种资源

- [大神 Andrei Alexandrescu 的 ppt，讲C语言优化](https://www.slideshare.net/andreialexandrescu1/three-optimization-tips-for-c-15708507)
- https://github.com/miloyip/itoa-benchmark/

### 《Effective Modern C++》, Scott Meyers

**Intro**

- lvalue: 和地址密切联系，all parameters are lvalues
- function object可以是定义了operator ()的object，只要有function-calling syntax就行
- deprecated feature: `std::auto_ptr -> std::unique_ptr`
- Undefined behavior: 数组越界、dereferencing an uninitialized iterator、engaging in a data race