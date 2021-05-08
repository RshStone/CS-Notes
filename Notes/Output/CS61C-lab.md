## lab0

​	课程基本注意事项（自学者没有homework账号）

​	git 一些基本命令(我写在了自己的笔记里)

​	至少学会一种`text editor` Vim/Emacs/Nano

## lab1

### Exercise 2: Catch those bugs! && Exercise 1: See what you can C

- `-c`,GCC会编译并汇编该代码

-  `-o`, which is used to specify the name of the executable file that `gcc` creates

  `$ gcc -o program program.c
  $ ./program`

- `-g` flag , which stores information in the executable program for `gdb` to make sense of it. 

  `gcc -g -o hello hello.c`  

  `gdb hello`

- `gdb`卡片，基本debug的操作

  GDB card: [CS 61C](https://cs61c.org/resources/pdf?file=gdb5-refcard.pdf)

  1. *set the arguments*
  2.  create a breakpoint
  3. execute the next line of C code in the program after stopping at a breakpoint?
  4. debug the code inside the function
  5. continue the program after stopping at a breakpoint?
  6.  print the value of a variable 
  7. displays the value of a variable after every step
  8. show a list of all variables and their values
  9. quit

### Exercise 3: Debugging w/ YOU

​	注意`gcc`版本问题使用`redirection`需要`gcc` 8.0 以上版本

​	`./a.out < fileName.txt`

### Exercise 4: Valgrind’ing away

盲点知识：

```c
struct Point {
int x;
int y;
struct Point *p;
};
struct Point *ptaddr;
/* arrow notation */  (箭头和.不同的表示)
int h = ptaddr->x;
int h = (*ptaddr).x;
```

​	bohrbugs:  they manifest reliably under a well-defined, but possibly unknown, set of conditions(编译器能检测到)

​	heisenbugs: often due to mis-managed memory(检测不到)

practice: tortoise and hare(龟兔赛跑)

​	对于一个`Node` *hard，`hare.next`指的是下一个节点而不是`(*hare).next`

```c
    (*(*hare).next).next EQUALS hare->next->next 但是第二种更简单
```

## lab2

- ​	Exercise 0: `Makefiles`(不太会，稍微看了下)

  `Makefile` Tutorial : [Makefile Tutorial By Example](https://makefiletutorial.com/#why-do-makefiles-exist-)

  1. Which target is part of a rule that deletes all the compiled programs?
  2. Which target is part of a rule that makes all the compiled programs?
  3. Which compiler is currently being used?
  4. What C standard are we currently using?
  5. How would we reference a variable FOO in a makefile?
  6. What operating system does the term “Darwin” represent?
  7. What line creates the lfsr program from its object files? (Give its line number.)

- Exercise 1: Bit Operations

  - 貌似在某个bit 取`v`时，其实也可以采用 `0|v`方式

  - 对 `xor`的理解

    ```c
    //多用于多bit数字的场景。以单bit运算为基本出发点，固定其中一位为0，发现最后的结果就是另外一个数字等价位上的值；同理，固定其中一位为1，结果为另一个数字等价位值的取反。
    if(bitStatus == 1)*x &= ~(1 << n);
    else if(bitStatus == 0){
        *x |= (1 << n);
    }
    ```

- Exercise 2: Linear Feedback Shift Register

  - 对于大端法和小端法，最高位所在位置不同，这里的最高位是最左边（大端法最高位在低地址，这里是大端法）

  - 位运算的对象是数字而非指针，如果要得到某一位，只需要把第n位移到最低位和1取&即可

  - 疑惑：为什么会有65536种正整数结果

- Exercise 3: Linked Lists
  - easy

- Exercise 4: Memory Management
  - `make vector_test`没成功使用 `gcc -o vector vector.c vector_test.c`测试成功
  - `make vector-memcheck`没成功
  - make理解不到位