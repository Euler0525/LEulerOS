# Hello World


```shell
sudo apt install nasm
sudo apt install build-essential
make all
```

修改`/etc/default/grub`中

```shell
GRUB_DEFAULT=0
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=10
```

```shell
sudo update-grub2
```

```shell
df /boot/  # 查看/boot目录挂载的分区

Filesystem     1K-blocks     Used Available Use% Mounted on
/dev/sda3       19946096 14556188   4351368  77% /
```


将下面代码复制到`/boot/grub/grub.cfg`

```shell
# msdos分区
menuentry 'HelloOS' {
    insmod part_msdos      # insmod part_gpt
    insmod ext2
    set root='hd0,msdos3'  # set root='hd0,gpt3'
    multiboot2 /boot/HelloOS.bin
    boot
}
# gpt分区
sudo fdisk -l /dev/sda

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt  # gpt分区
Disk identifier: 6DF5DC0A-B9AA-423D-A884-0AE4BEBA4CF6

Device       Start      End  Sectors  Size Type
/dev/sda1     2048     4095     2048    1M BIOS boot
/dev/sda2     4096  1054719  1050624  513M EFI System
/dev/sda3  1054720 41940991 40886272 19.5G Linux filesystem
```

重启虚拟机，选择HelloOS