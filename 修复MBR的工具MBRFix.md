修复MBR的工具MBRFix

安装过linux系统的朋友，有过这样的经历，安装Ｇrub的时候，把硬盘的MBR修改了，但是删除ＬＩＮＵＸ的时候，却连原来的ＷＩＮＤＯＷＳ系统也启动不了，怎么办？

写入MBR的方法，有两种比较简单

第1种方法：就是将Windows的安装盘放入计算机以后，重启计算机，进入Windows安装程序，随后，进入恢复控制台，输入命令fixmbr即可。
   第2种方法是为没有Windows安装盘的朋友准备的，就是使用MBRFix工具进行修复。
   MBRFix工具修复MBR很方便，先进入cmd命令窗口，然后进入mbrfix工具所在的目录（用cd命令），然后输入命令 MbrFix /drive 0 fixmbr ，再确认一下即可。重启以后你会发现，没有了Linux，直接可以进入Windows了。
