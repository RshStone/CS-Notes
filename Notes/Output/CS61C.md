# CS61C:Great Ideas in Computer Architecture

## why I want to learn it and write note

​	In this demo, I want to share with you about my current situation and feelings when I study the course so that you can consider that if you will learn it or if you have the similar ideas with me.

- I have finished Nand2TetrisI on coursera and learn CS according to [Teach yourselfCS-CN](https://github.com/keithnull/TeachYourselfCS-CN/blob/master/TeachYourselfCS-CN.md) .
- I'm not majoring material science in university and I want to learn the basic about CS which makes me lose myself in.
- It is not easy for most students to learn the most famous foreign country's CS course by themselves so I want to record my study note concretely as possible as I can.
- Enjoy study!  

## how to learn this course for me

How long: 24(h)

From my perspective, I want to get an offer maybe in August. I also want to learn some fundamental courses about the computer science. I'm attracted by its beauty. 

So I will look at all the lecture of this course and then pick some lectures to learn. And more time to read the book CSAPP and do some labs.

Happy coding!

## lec01 Course Intro, Number Representation

 preparation the basis you should know about this course 2's complement 进制转换 unsigned

- Six Great Ideas In Computer Architecture
  1. Abstraction
  2. Technology Trends
  3. Principle of Locality/Memory Hierarchy
  4. Parallelism
  5. Performance Measurement & Improvement
  6. Dependability via Redundancy

- Website Textbooks Piazza(discussion)

- Course Assignments and Grading

  12 total Labs(partner)  4-Projects

- Successful Behaviors

  - Practice, practice, practice
  - Find a learning community
  - Avoid comparison, do your best, and judge yourself on your progress alone.

  - You learn best from your mistakes.

- Number Base Examples

  9472ten = 9000 + 400 + 70 + 2

  General Formula

- 2^10 `Kibi` 2^20 `Mebi` 2^30 `GiBi` 2^40 `Tebi` 2^50 `Pebi` 2^60 `Exbi` 2^70 `Zebi` 2^80 `Yobi`

- Bias Notation

  unsigned value + bias  = 'actual' value

## lec02 C:Introduction,Pointer

- Compilation 

  - C - compiled language

  - map C programs into machine code

  - Advantages

    Excellent run-time performance

    fair compilation time

  - Disadvantages

    architecture-specific(CPU type and OS)

    repeat until correct all bugs(Slow procedure)

- Typed Variables in C

  `int` 	signed integer 5,-12

  `short`	`int`(short)

  `long int`

  `char`

  `float`

  `double`

- Characters

  i. Encode characters as numbers

  ii. ASCII

  iii. A char takes 1 bit

- Typecasting in C

  i. weakly typed language

  ii. Can typecast anything(be careful)

- Typed Functions in C

- Structs in C

  i. define compound data types

  ii. group of variables, possibly including other structs

  iii. Structs Alignment and Padding in C(enough space and aligns)	 

  ```c
  //sizeof(struct foo) == 12, 3 unused bytes
  Struct foo {
  int a;
  char b;
  struct foo *c;
  }
  ```

- Unions in C

  i. enough space for the largest element

- operators

  nearly identical

- C Syntax: main

  `int main(int argc, char *argv[])`

  `-argc` argument count contains the number of strings

  `-argv`	argument value is an array

- True or False

  i. No explicit Boolean type	

- Pointers

  - variable that contains an address
  - `void *` can point to anything(be careful !!!)

  - `int *x,y,z`  ! = -- > `int *x,*y,*z` 
  - pass by reference

## lec03 C Arrays,Strings, More Pointers

- Struct Alignment

  ```c
  struct hello {
  int a;
  char b;   // char 填的时候，如果地址非word(4 Bytes)或者half-word,自动填齐
  short c;
  char *d;
  char e; // 最后结果需要是n个Bytes
  };
  sizeof(hello) = 16
  ```

  ![image-20210425143914962](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/CS61C/001.png)

- Arrays 

  - Pitfall: An array in C does not know its own length, and its bounds are not checked!

    (learn how to debug later!!!)

  - better write pattern

    ```c
    //If the code is long, it is really easy to change the length of the array.
    const int ARRAY_SIZE = 10;
    int ar[ARRAY_SIZE];
    for(int i=0; i<ARRAY_SIZE; i++)
    ```

    

  - `ar[i]` is true equals to `*(ar + i)`

    i. An array variable looks like a pointer to the first (0th) element

    ii. To zero an array, the following three ways are equivalent:
    `1)for(i=0; i<SIZE; i++){ar[i] = 0;}`
    `2)for(i=0; i<SIZE; i++){*(ar+i) = 0;}
    3)for(p=ar; p<ar+SIZE; p++){*p = 0;}`

    iii. K&R: “An array's name is not a variable”

    ```c
    //*p:1, p:40, &p:20
    //*a:2, a:24, &a:24(meaningless)
    void foo() {
    int *p, a[4], x;
    p = &x;
    *p = 1; // or p[0]
    printf("*p:%u, p:%u, &p:%u\n",*p,p,&p);
    *a = 2; // or a[0]
    printf("*a:%u, a:%u, &a:%u\n",*a,a,&a);
    }
    ```

    iv. Array size gets lost when passed to a function

    ```c
    int foo(int array[], unsigned int size){
    	printf("%d\n", sizeof(array));
    }
    ```

    v. C String

    ​	`\0` terminator

     `#include <string.h>`: 	

    ​		`int strlen(char *string)` `int strcmp(char *str1, char *str2)` --> the difference between their ASCII

    ​		`char *strcpy(char *dst, char *src)`

  

- More pointers

  - Pointer Arithmetic: pointer ± number

    cautiously, the code is hard to read.

  - Increment and Dereference

    `++*p` `*--p` （右到左）

    `(*p)++` 

  - Pointer `Misc`(杂项)

    传值和传址

## lec04: C:Memory Management and Usage

- C Memory Layout

  stack(LIFO): local variables, grows downward

  ​	Stack pointer(SP): moves up and down with the procedure

  ​	Misuse Example: return local variable from functions

  heap: space requested via malloc() and used with pointers;

  ​	`sizeof()`

  static data: global and static variables, does not grow or shrink	

  code: loaded when program starts, does not change

- Address

  - Endianness

    Little Endian、Big Endian

  - Allocating Memory(should check NULL)

    `malloc`(): continuous blocks, uninitialized, return pointers

    `calloc`(): `void *calloc(size_t nmemb, size_t size)`

    ​	like malloc(), except it initialized all values of 0 

    `realloc`(): `void *realloc(void *ptr, size_t size)`

     	need more or less memory in an array

  - Releasing Memory

    `free`(p), p is pointer

- Memory Errors

  - Segmentation Fault

     attempts to access memory not allocated to it

  -  Bus Error

    “A fatal failure in the execution of a machine language instruction resulting from the processor detecting an anomalous condition on its bus. Such conditions include invalid address alignment (accessing a multi-byte number at an odd address), accessing a physical address that does not correspond to any device, or some other device-specific hardware error.”

  - Common Memory Problem

    1) Using uninitialized values
    2) Using memory that you don’t own
    	–Using NULL or garbage data as a pointer
    	–De-allocated stack or heap variable
    	–Out of bounds reference to stack or heap array
    3) Freeing invalid memory
    4) Memory leaks

## leco5: Floating Points（不会）

- Floating Point

  10进制科学计数法牵引到二进制，二进制的点，左半部分和右半部分

  - Single Precision

    32-bit word into 3 fields

    ![image-20210503164145464](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/CS61C/image-20210503164145464.png)

    ​	

    Biased notation: 

    ​	why use it?

     1. compare numbers easily(保证数组非负线性，补码的一个弊端非线性)

        ​	compare order: Sign --> Exponent --> Significand
    
    The Exponent Field:
    
    ​	1. bias: -127
    
     2. encoding: +127 e.g. 2^1 exp = 1 ==> 128 ==> 10000000two
    
     3. cases
    
        Normalization:
    
        ​	Exponent != 0 || != 255
    
        Denormalization:
    
        ​	all 0
    
        Special cases:	
    
        ​	11111111(255): 
    
        ​				NaN != 0  
    
        ​				infinite: all 0 
  
- Floating Points: special cases

  ​		![image-20210504162159577](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/CS61C/image-20210504162159577.png)	

- Floating Points Limitations

  ​	Assume x is the result

  ​	Overflow:  abs(x) > 2 ^123

  ​	Underflow: 0 < abs(x) < 2^-149

  - Floating Point Gaps: get larger with larger exponent

  - FP addition is NOT associative

    Small + Big + Small != Small + Small + Big

    不是很理解的地方(+一个后面的小练习)

    ​	![image-20210504164706162](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/CS61C/image-20210504164706162.png)

- 

浮点数具体的每部分和历史

当然内容很丰富

## lec06:Introduction to Machine Language: RISC-V architecture(！！！重点来啦)

Assembly Language Program(e.g. RISCV)

比Hack computer(macro assembler的简化)更硬核，现代应用的东东。

## leco7:More RISC-V, RISC-V Functions(更看不懂了)

## lec08:RISC-V Instruction Formats

## leco9:Running a Program: CALLs(写project了)

## leco10:Combinational Logic(这个我会，嘿嘿)

## leco11:Sequential Digital Logic(会，但有点晕，想学可以深入)

 Logisim的使用，虽然之前接触使用过

## leco12:RISC-V CPU Datapath, Control Intro(搞CPU了，可深入)

之前学Nand2Tetris这部分简化了，你直接按照diagram补充一些细节就可以了

## leco13:RISC-V CPU Control, Pipelining(看了下，真TM硬核)

## leco14:RISC-V Pipeline Hazards!

## leco15:Memory Hierarchy, Fully Associative Caches

## leco16:Direct-Mapped and Set Associative Caches(涉及到缓存)

## leco17:Multilevel Caches, Cache Questions(更多的缓存)

## leco18:Operating Systems, Virtual Memory Intro(操作系统)

## leco19:Virtual Memory

## leco20:Input/Output

## leco21:Flynn’s Taxonomy and
Data-level Parallelism(并行，之前没接触)

## leco22:Amdahl’s Law and
Thread Level Parallelism

## leco23:Multithreading Issues, Cache Coherency

## leco24:Warehouse Scale Computers, MapReduce

## leco25:Dependability: Parity, ECC, RAID

## leco26:View from the Top