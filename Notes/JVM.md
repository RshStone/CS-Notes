我的目标： 了解内存管理和初步了解内存结构和垃圾回收机制

## 起步准备

学习资料：

​	深入理解Java虚拟机(周志明)

相关知识串联：

​	数组的删除优化处理。

起步学习:

​	编译JDK12，首先去阅读file:///D:/Downloads/jdk12-06222165c35f/doc/building.html

​	Instructions for the Impatient: Mercurial and Cygwin(for Windows)

​		之后涉及到了尝试软件Cygwin, 这个软件的作用。

​			摘自博客: https://www.worldhello.net/gotgit/01-meet-git/050-install-on-windows-cygwin.html

​			*Cygwin是一款伟大的软件，通过一个小小的DLL（cygwin1.dll）建立Linux和Windows系统调用及API之间的转换，实现了Linux下绝大多数软件到Windows的迁移。Cygwin通过cygwin1.dll所建立的中间层和诸如VMWare、VirtualBox等虚拟机软件完全不同，不会对系统资源进行独占。像VMWare等虚拟机，只要启动一个虚拟机（操作系统），即使不在其中执行任何命令，同样会占用大量的系统资源：内存、CPU时间等等。*

*Cygwin还提供了一个强大易用的包管理工具（setup.exe），实现了几千个开源软件包在Cygwin下便捷的安装和升级，Git就是Cygwin下支持的几千个开源软件中的一员。*

*我对Cygwin有着深厚的感情，Cygwin让我在Windows平台能用Linux的方式更有效率的做事，使用Linux风格的控制台替换Windows黑乎乎的、冰冷的、由**cmd.exe**提供的命令行。Cygwin帮助我逐渐摆脱对Windows的依赖，当我完全转换到Linux平台时，没有感到一丝的障碍。*

​		同时也尝试了Mercurial这款软件

​		尝试build openJDK12 

​	    结果和几个月前的内容一样，只是几个月前我没弄明白，为什么这样。没有详细记录

​	参考博客：[Build OpenJDK 12 On Fedora 29 | Dariawan](https://www.dariawan.com/tutorials/java/build-openjdk-12-fedora-29/)

This is because [jtreg](https://openjdk.java.net/jtreg/) framework is not 'installed' in your machine. But this is completely out of this article scope. So, for today... Enjoy your custom build OpenJDK!

```

Creating buildtools/jdk.vm.compiler.serviceprovider.processor.jar
Creating support/modules_libs/java.base/jrt-fs.jar
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
Note: Some input files use or override a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
make[3]: Warning: File '/mnt/d/Downloads/jdk12-06222165c35f/build/linux-x86_64-server-fastdebug/make-support/vardeps/make/gensrc/Gensrc-jdk.hotspot.agent.gmk/jdk.hotspot.agent/VERSION_STRING.vardeps' has modification time 1.9 s in the future
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
Note: Some input files use or override a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
Note: Some input files use unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
make[3]: Warning: File '/mnt/d/Downloads/jdk12-06222165c35f/build/linux-x86_64-server-fastdebug/make-support/vardeps/make/gensrc/Gensrc-java.base.gmk/java.base/VARDEPS_VALUE.vardeps' has modification time 1.8 s in the future
make[3]: Warning: File '/mnt/d/Downloads/jdk12-06222165c35f/build/linux-x86_64-server-fastdebug/make-support/vardeps/make/GensrcModuleInfo.gmk/java.base/ALL_MODULES.vardeps' has modification time 1.9 s in the future
make[3]: Warning: File '/mnt/d/Downloads/jdk12-06222165c35f/build/linux-x86_64-server-fastdebug/buildtools/break_iterator_classes/jdk.localedata/_the.BUILD_BREAKITERATOR_LD.vardeps' has modification time 1.7 s in the future
Compiling 2 files for BUILD_BREAKITERATOR_BASE
Compiling 2 files for BUILD_BREAKITERATOR_LD
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
Compiling 11 properties into resource bundles for java.logging
In file included from /usr/include/string.h:495,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/utilities/globalDefinitions_gcc.hpp:35,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/utilities/globalDefinitions.hpp:32,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/utilities/align.hpp:28,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/runtime/globals.hpp:29,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/memory/allocation.hpp:28,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/classfile/classLoaderData.hpp:28,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/precompiled/precompiled.hpp:34:
In function ‘char* strncpy(char*, const char*, size_t)’,
    inlined from ‘static jint Arguments::parse_each_vm_init_arg(const JavaVMInitArgs*, bool*, JVMFlag::Flags)’ at /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/runtime/arguments.cpp:2472:29:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:106:34: error: ‘char* __builtin_strncpy(char*, const char*, long unsigned int)’ output truncated before terminating nul copying as many bytes from a string as its length [-Werror=stringop-truncation]
  106 |   return __builtin___strncpy_chk (__dest, __src, __len, __bos (__dest));
      |          ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/runtime/arguments.cpp: In static member function ‘static jint Arguments::parse_each_vm_init_arg(const JavaVMInitArgs*, bool*, JVMFlag::Flags)’:
/mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/runtime/arguments.cpp:2471:44: note: length computed here
 2471 |         size_t len = (pos == NULL) ? strlen(tail) : pos - tail;
      |                                      ~~~~~~^~~~~~
cc1plus: all warnings being treated as errors
make[3]: *** [lib/CompileJvm.gmk:174: /mnt/d/Downloads/jdk12-06222165c35f/build/linux-x86_64-server-fastdebug/hotspot/variant-server/libjvm/objs/arguments.o] Error 1
make[3]: *** Waiting for unfinished jobs....
Compiling 11 properties into resource bundles for java.base
Compiling 6 properties into resource bundles for java.base
make[2]: *** [make/Main.gmk:257: hotspot-server-libs] Error 2
make[2]: *** Waiting for unfinished jobs....
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
make[3]: warning:  Clock skew detected.  Your build may be incomplete.

ERROR: Build failed for target 'images' in configuration 'linux-x86_64-server-fastdebug' (exit code 2)
Stopping sjavac server

=== Output from failing command(s) repeated here ===
* For target hotspot_variant-server_libjvm_objs_arguments.o:
In file included from /usr/include/string.h:495,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/utilities/globalDefinitions_gcc.hpp:35,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/utilities/globalDefinitions.hpp:32,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/utilities/align.hpp:28,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/runtime/globals.hpp:29,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/memory/allocation.hpp:28,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/classfile/classLoaderData.hpp:28,
                 from /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/precompiled/precompiled.hpp:34:
In function ‘char* strncpy(char*, const char*, size_t)’,
    inlined from ‘static jint Arguments::parse_each_vm_init_arg(const JavaVMInitArgs*, bool*, JVMFlag::Flags)’ at /mnt/d/Downloads/jdk12-06222165c35f/src/hotspot/share/runtime/arguments.cpp:2472:29:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:106:34: error: ‘char* __builtin_strncpy(char*, const char*, long unsigned int)’ output truncated before terminating nul copying as many bytes from a string as its length [-Werror=stringop-truncation]
  106 |   return __builtin___strncpy_chk (__dest, __src, __len, __bos (__dest));
   ... (rest of output omitted)

* All command lines available in /mnt/d/Downloads/jdk12-06222165c35f/build/linux-x86_64-server-fastdebug/make-support/failure-logs.
=== End of repeated output ===

No indication of failed target found.
Hint: Try searching the build log for '] Error'.
Hint: See doc/building.html#troubleshooting for assistance.

make[1]: *** [/mnt/d/Downloads/jdk12-06222165c35f/make/Init.gmk:310: main] Error 2
make: *** [/mnt/d/Downloads/jdk12-06222165c35f/make/Init.gmk:186: images] Error 2
```

## 自动内存管理

第2章 Java内存区域与内存溢出异常 

第3章 垃圾收集器与内存分配策略 

第4章 虚拟机性能监控、故障处理工具 

第5章 调优案例分析与实战

###  Java内存区域与内存溢出异常 

​	![image-20220316104514459](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220316104514459.png)



## 垃圾回收器与内存分配策略

## 虚拟机性能监控、故障处理工具

## 调优案例分析与实战