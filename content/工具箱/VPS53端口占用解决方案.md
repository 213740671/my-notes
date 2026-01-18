从你提供的截图和命令输出 (`systemd-resolve`) 来看，你的 53 端口目前被 Ubuntu/Debian 系统自带的 **`systemd-resolved`** 服务占用了。这是现代 Linux 发行版（特别是 Ubuntu）的标准行为，它会在本地运行一个 DNS 缓存存根。

为了释放 53 端口（通常是为了安装 AdGuard Home、Pi-hole 或其他 DNS 服务），同时**保证 VPS 自身能正常联网**，你需要停用该服务并手动指定 DNS 服务器。

请按照以下步骤操作：

### 第一步：停止并禁用 systemd-resolved 服务

首先，我们需要停止占用端口的服务，并防止它开机自启。

```bash
# 停止 systemd-resolved 服务
sudo systemctl stop systemd-resolved

# 禁用开机自启
sudo systemctl disable systemd-resolved
```

### 第二步：修改 DNS 配置文件 (关键步骤)

`systemd-resolved` 停止后，原来的 `/etc/resolv.conf`（通常是一个软链接）将失效，导致 VPS 无法解析域名（无法联网）。我们需要删除软链并创建一个新的静态文件。

1.  **删除原有的软链接：**

    ```bash
    sudo rm /etc/resolv.conf
    ```

2.  **创建新的 `/etc/resolv.conf` 并写入公共 DNS：**
    使用你喜欢的编辑器（如 nano 或 vim），或者直接使用以下命令写入 Google 和 Cloudflare 的 DNS：

    ```bash
    sudo sh -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
    sudo sh -c 'echo "nameserver 1.1.1.1" >> /etc/resolv.conf'
    ```

    > **解释：** 这一步告诉系统：“不要去问本地的 127.0.0.53 了，直接去问公网的 8.8.8.8”。这样既释放了本地端口，又保证了联网。

### 第三步：防止配置文件被覆盖 (可选但推荐)

有些云服务商的 VPS 会在重启后通过 cloud-init 或 DHCP 强制重置 `/etc/resolv.conf`。为了防止你的修改失效，可以使用 `chattr` 命令锁定该文件：

```bash
# 锁定文件，禁止修改
sudo chattr +i /etc/resolv.conf
```

*(注意：如果你以后想修改 DNS，需要先执行 `sudo chattr -i /etc/resolv.conf` 解锁)*

### 第四步：验证结果

1.  **检查 53 端口是否释放：**
    再次运行你之前的命令，应该看不到 `systemd-resolve` 了：

    ```bash
    sudo ss -lntup | grep -E ':(53)\b'
    ```

    *(如果此时没有输出，或者只有你新安装的软件在运行，说明成功释放)*

2.  **检查是否能正常联网：**
    尝试 ping 一个域名：

    ```bash
    ping -c 4 google.com
    ```

    如果能 ping 通，说明 DNS 解析正常，VPS 联网不受影响。

-----

### 替代方案：仅关闭监听而不停止服务

如果你不想完全停止 `systemd-resolved`，只想让它不要占 53 端口（只作为后台客户端运行），可以修改其配置文件：

1.  编辑 `/etc/systemd/resolved.conf`。
2.  找到 `#DNSStubListener=yes`，将其改为 `DNSStubListener=no`。
3.  保存并重启服务：`sudo systemctl restart systemd-resolved`。
4.  同样需要按照**第二步**处理 `/etc/resolv.conf`，将其指向 127.0.0.53 以外的地址（因为 StubListener 关闭后 127.0.0.53 就不通了）。

**总结：** 最推荐的方法是**第一种（彻底停止服务并手动设置 DNS）**，因为它最彻底，也是在 Linux Do 等社区搭建 AdGuard Home 等服务时的标准操作。

**我可以帮你生成验证端口和联网状态的一键检查命令吗？**