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

