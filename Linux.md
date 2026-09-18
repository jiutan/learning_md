# Linux 日常操作

### Linux 目录路径

```
/  (根目录，整个大楼的最底座)
├── opt/          <--- 看这里！opt 在大楼的一层公共区域，由系统管理！
├── etc/          <--- 系统的各种配置文件
├── usr/          <--- 系统自带软件库
└── home/         <--- 住宅区
    └── jiutan/   <--- 这就是你的 ~ (你的私人房间！)
        ├── 桌面
        ├── 下载
        └── 文档
```

注意：

- **/（根目录）**：就是这栋**大楼的地基/大堂**（最顶层入口）。

- **~（家目录）**：只是这栋大楼里的**某一个私人房间**（全名其实是 /home/jiutan）。



### Linux Shell

#### （1）Shell 翻墙：

- 配置：

  ```bash
  cat >> ~/.bashrc << 'EOF'
  
  # --- 终端代理一键开关 ---
  alias setproxy="export http_proxy=http://127.0.0.1:7890 https_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890; echo '终端代理已开启 🚀'"
  alias unsetproxy="unset http_proxy https_proxy all_proxy; echo '终端代理已关闭 ❌'"
  alias checkproxy="curl -i https://www.google.com 2>/dev/null | head -n 1"
  EOF
  
  # 立即刷新配置生效
  source ~/.bashrc
  
  # （可选）删除 清华大学镜像源
  pip config unset global.index-url
  ```

- 开启 与 关闭：

  - 开启：`setproxy`
  - 关闭：`unsetproxy`

- 安装软件的写法：`-E`

  ```bash
  # -E 参数代表“保留当前用户的环境变量与代理配置”
  sudo -E apt update
  ```

- Git 代理：

  ```bash
  git config --global http.proxy http://127.0.0.1:7890
  git config --global https.proxy http://127.0.0.1:7890
  ```



### Linux 解压文件：

#### 常见压缩格式解压命令：

- **`.zip` 文件**：

  ```bash
  unzip 文件名.zip
  ```

- **`.tar.gz` 或 `.tgz` 文件**：

  ```bash
  tar -xzvf 文件名.tar.gz
  ```

- **`.tar.bz2` 文件**：

  ```bash
  tar -xjvf 文件名.tar.bz2
  ```

- **`.tar.xz` 文件**：

  ```bash
  tar -xJvf 文件名.tar.xz
  ```

- **`.7z` 文件**：

  ```bash
  7z x 文件名.7z
  ```

- **`.rar` 文件**：

  ```bash
  unrar x 文件名.rar
  ```

#### 解压常用参数说明：

- **`-x`**：解压（extract）
- **`-z`**：处理 gzip 压缩（对应 `.gz`）
- **`-j`**：处理 bzip2 压缩（对应 `.bz2`）
- **`-J`**：处理 xz 压缩（对应 `.xz`）
- **`-v`**：显示解压过程（verbose）
- **`-f`**：指定文件名（file）



### Linux 安装软件

1. 位置：`/opt/软件名`

2. 操作：

   ```bash
   # 如果你的下载文件夹是中文“下载”：(<> 表示 需要替换)
   sudo mv ~/下载/<软件文件夹名>* /opt/<软件名>
   
   # 如果上面提示找不到，试这个（英文 Downloads）：
   sudo mv ~/Downloads/<软件文件夹名>* /opt/<软件名>
   ```

   

3. 

### Linux 云盘挂载

#### 百度网盘

目前的本地盘为：`~/文档/BaiduSync`

百度网盘的挂载盘为：`Linux_BaiduSync`

使用的挂载工具为：`alist`

- 同步命令：在本地盘存入文件后，输入命令进行同步

  ```
  rclone bisync ~/文档/BaiduSync alist:/Baidu/Linux_BaiduSync --compare size -v
  ```

  

- 自动同步方法：（已实现）

  ```c++
  // 1. 创建 systemd 用户服务
  mkdir -p ~/.config/systemd/user
  mkdir -p ~/.cache
  
  //// 创建服务文件：
  nano ~/.config/systemd/user/baidu-bisync.service
  
  //// 写入： 保存退出。   
  [Unit]
  Description=Baidu Netdisk bisync via rclone
  
  [Service]
  Type=oneshot
  ExecStart=/usr/local/bin/rclone bisync %h/文档/BaiduSync alist:/Baidu/Linux_BaiduSync --compare size --log-file=%h/.cache/baidu-bisync.log --log-level INFO
  
  // 2. 创建定时器
  nano ~/.config/systemd/user/baidu-bisync.timer
      
  //// 写入：
  [Unit]
  Description=Run Baidu Netdisk bisync every 5 minutes
  
  [Timer]
  OnBootSec=2min
  OnUnitActiveSec=5min
  Persistent=true
  
  [Install]
  WantedBy=timers.target
      
  // 3. 启用自动同步：每 5 分钟自动同步一次
  systemctl --user daemon-reload
  systemctl --user enable --now baidu-bisync.timer
      
  //// 查看状态：
  systemctl --user status baidu-bisync.timer    
  
  //// 查看同步日志：
  tail -f ~/.cache/baidu-bisync.log
      
  // 4. 如果希望关掉终端/注销后也继续同步
  sudo loginctl enable-linger $USER    
  ```

  
