* 通过模块获取内核信息

file name: zoneinfo.c

```
#include <linux/module.h>
#include <linux/mmzone.h>

MODULE_LICENSE("Dual BSD/GPL");

static int my_init(void)
{
    struct pglist_data *node;
    node = NODE_DATA(0);
    struct zone node_zones;
    int i;
    for(i = 0;i < MAX_NR_ZONES; i++)
    {
    	node_zones = node ->node_zones[i];
        printk(KERN_ALERT "%s\n", node_zones.name);
    }
    return 0;
}
static void my_exit(void)
{
	printk(KERN_ALERT "Module has been uninstalled\n");
}
module_init(my_init);
module_exit(my_exit);

```

file name: Makefile
```
obj-m := zoneinfo.o
```
then, type in terminal
```
$make -C /usr/src/linux-headers-3.16.0-4-amd64/ M=/home/luzhzh/gitpro/mm/ modules
make: Entering directory '/usr/src/linux-headers-3.16.0-4-amd64'
make[1]: Entering directory `/usr/src/linux-headers-3.16.0-4-amd64'
  CC [M]  /home/luzhzh/gitpro/mm//zoneinfo.o
/home/luzhzh/gitpro/mm//zoneinfo.c: In function ‘my_init’:
/home/luzhzh/gitpro/mm//zoneinfo.c:10:5: warning: ISO C90 forbids mixed declarations and code [-Wdeclaration-after-statement]
     struct zone node_zones;
     ^
  Building modules, stage 2.
  MODPOST 1 modules
  CC      /home/luzhzh/gitpro/mm//zoneinfo.mod.o
  LD [M]  /home/luzhzh/gitpro/mm//zoneinfo.ko
make: Leaving directory '/usr/src/linux-headers-3.16.0-4-amd64'

$ls
Makefile        modules.order   sh          zoneinfo.ko     zoneinfo.mod.o
mm_learning.md  Module.symvers  zoneinfo.c  zoneinfo.mod.c  zoneinfo.o

$sudo insmod zoneinfo.ko
$dmesg
...
[ 3006.829751] DMA
[ 3006.829756] DMA32
[ 3006.829757] Normal
[ 3006.829758] Movable

$ sudo rmmod zoneinfo.ko
$dmesg
[ 3182.854165] Module has been uninstalled
```

