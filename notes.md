```
-include/asm-i386/mmzone.h
extern struct pglist_data *node_data[];
#define NODE_DATA(nid)		(node_data[nid])

EXPORT_SYMBOL(node_data);
```

* what is the meaning of EXPORT_SYMBOL? 
It makes a symbol accessible to dynamically loaded modules (provided that said modules add an extern declaration).

* Does __/proc/kallsyms__ have all the symbol of kernel functions? 
As far as I know, if a function does not appear in /proc/kallsyms, it is not possible to call or probe it from a module. However, /proc/kallsyms contains all functions of the kernel, not just the ones exported via EXPORT_SYMBOL/EXPORT_SYMBOL_GPL.

* How to call exported kernel module functions from another module? 
https://stackoverflow.com/questions/12311867/how-to-call-exported-kernel-module-functions-from-another-module

* what does "static" mean in c? 
In the C programming language, static is used with global variables and functions to set their scope to the containing file. In local variables, static is used to store the variable in the statically allocated memory instead of the automatically allocated memory.Feb 21, 2009

* /var/log/message 
dmesg

