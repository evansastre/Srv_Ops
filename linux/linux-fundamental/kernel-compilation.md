# kernel compilation

## Why compile kernel

In order to correctly and correctly set the kernel compilation configuration options, so that only the code of the functions required by the system is compiled, there are generally four main considerations: 

\(1\) Self-customized compiled kernel runs faster \(with less code\) 

\(2\) The system will have more memory \(the kernel part will not be swapped into virtual memory\) 

\(3\) Unwanted functions compiled into the kernel may increase the vulnerability exploited by system attackers 

\(4\) Compiling a function into a module is slower than compiling into the kernel.



The purpose of this type of compilation is mainly to understand the process of compiling the Linux kernel by compiling, familiar with the working principle of the kernel, and even try to make some modifications. Compiling just compiles the source code into a program that does not replace the current system and does not affect the operation of the current system.

Compiling the kernel may be for some kind of requirement, such as the size of the kernel, and removing some of the unused parts of the kernel. This scenario is often an embedded system. Or modify a part of the kernel code yourself, you need to compile and verify the function. When the module is compiled, some functional modules are compiled into .ko. Insmod xxx.ko can be used to write code functions into the system without recompiling the kernel. After compiling the kernel, the current kernel will not be replaced. The compiled new kernel is often in a directory similar to the following, and the names are mostly bzImage. /usr/src/kernels/3.xx.x-.x86\_64/arch/x86/boot/ 

You can then edit the system's grub list to add the latest kernel to use it.

The new kernel integrates new drivers, such as Intel kernel: 

/lib/modules/`uname -r`/kernel/drivers/gpu/drm/i915/i915.ko

A system can install multiple kernels, such as boot files, and the new kernel will not overwrite the old kernel: 

/boot/vmlinuz-VERSION 

/boot/initrd.img-VERSION 

During the installation of the new kernel, some kernel modules need to be recompiled, such as VirtualBox: /lib/modules/`uname -r`/updates/dkms/vboxdrv.ko 

If the new kernel is not working properly, you can select the old kernel boot in the boot GRUB boot. You can also change back to the original kernel: 

Ln -sf /boot/vmlinuz-VERSION /vmlinuz 

Ln -sf /boot/initrd.img-VERSION /initrd.img 

Where VERSION is the version of the original kernel.



## common problem

1. rebooot can not enter the system tip Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block\(0,0\), mostly menu.lst is not set.

Solve: Restart the system, select the unmodified kernel version \(such as Ubuntu 6.06 comes with 2.6.15\) into the system, check the menu.lst file \(can be updated-grub\)

2. The high version of the kernel can not compile the low version of the kernel 

The compilation tool is too new and it is recommended to compile the kernel with the appropriate distribution. Similarly, if the low version cannot compile the high version, you should consider whether you should upgrade the tool.





