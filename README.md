# BPFS
BPFS是一个可以保证强一致性的文件系统，

1.首先是使用了CPU通过内存总线直接访问NVM，将数据易失性的时间窗口，从原来的内存flush到磁盘的5-30s,减少到cache刷到内存的更短的时间。

2.使用类似于WAFL的数据存储结构，都是树形结构，有三种文件，inode文件，directory文件，data文件，都存在树中，这种结构使得，只修改很少的字节（in-place)，就可以修改很多文件或者目录，而且可以使用copy-on-write，结合有序的写入，保证一致性。

3.保证原子性一致性的除了树形结构特点，还有两个硬件支持，一个是NVM的8字节的原子写，一个是本文提出由软件向硬件发出epoch barrier 来保证写入顺序，从而保证原子性。

我的问题：
关于多核多线程如何保证一致性，我没看懂，需要补些基础知识。

这个文件系统是单机的，能否扩展为分布式的，是否有适合的场景。
