# tar压缩包解压
## 压缩【tar -zcvf】
## 解压【tar -zxvf】
```
    # 压缩文件 file1 和目录 dir2 到 test.tar.gz
    tar -zcvf test.tar.gz file1 dir2
    
    # 解压 test.tar.gz（将 c 换成 x 即可）
    tar -zxvf test.tar.gz
    
    # 列出压缩文件的内容
    tar -ztvf test.tar.gz 
```
