## 安裝

首先請先確定你的 [extra](https://wiki.archlinux.org/index.php/Official_Repositories#.5Bextra.5D) 已啟動，然後安裝 NTFS-3G

 `# pacman -S ntfs-3g` 

## 掛載硬碟

有兩種方式可以用來掛載（mount）你的硬碟：

 `# mount -t ntfs-3g /dev/<your-NTFS-partition> /{mnt,...}/<folder>` 

或是：

 `# ntfs-3g /dev/sda1 /mnt/<mount point>` 

## 自動掛載

自動掛載可以在系統配置文件 [Fstab](/index.php/Fstab "Fstab") 中設定。

把以下內容放置於 /etc/fstab 中

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
<partition>  <mount point>  ntfs-3g  defaults  0 0

```