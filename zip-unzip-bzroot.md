# 解压/打包bzroot
打开`ubuntu Terminal`
```bash
# 进入root模式
sudo -i 

# 提取bzmicrcode
dd if=/home/lele/ws/bzroot bs=512 count=$(cpio -ivt -H newc < /home/lele/ws/bzroot 2>&1 > /dev/null | awk '{print $1}') of=/home/lele/ws/bzmicrocode


# 解压文件
dd if=/home/lele/ws/bzroot bs=512 skip=$(cpio -ivt -H newc < /home/lele/ws/bzroot 2>&1 > /dev/null | awk '{print $1}') | xzcat | cpio -i -d -H newc --no-absolute-filenames

## 压缩打包
cp /home/lele/ws/bzmicrocode /home/lele/ws/out/bzroot
find . | cpio -o -H newc | xz --format=lzma >> /home/lele/ws/out/bzroot
```

参考帖子：https://forums.unraid.net/topic/36780-how-to-unzip-and-zip-bzroot/?tab=comments#comment-750644

注意：我直接在unraid下进行解压/打包时，发现生成的bzroot不能使用，因此选择了在Ubuntu进行。
