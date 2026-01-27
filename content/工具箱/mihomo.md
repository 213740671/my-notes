# 🚀 Mihomo (Clash.Meta) VPS Docker 运维手册

这份笔记涵盖了你从小白进阶到日常运维所需的全部操作。建议收藏或保存到本地。

---

## 一、 如何切换/更新订阅链接
如果你更换了机场或 token 变了，只需要修改配置文件中的 URL。

1.  **进入目录：**
    ```bash
    cd ~/mihomo
    ```
2.  **修改配置：**
    ```bash
    nano config.yaml
    ```
    找到 `url: "https://..."` 这一行，删掉旧链接，粘贴新链接。
3.  **保存退出：** `Ctrl+O` -> `Enter` -> `Ctrl+X`。
4.  **生效配置：**
    修改完后，建议执行重启命令让内核重新拉取：
    ```bash
    docker compose restart mihomo
    ```

---

## 二、 面板中四个“代理组”的区别
根据你上传的图片（image_4bcfff.png），这四个卡片代表了不同的流量分发逻辑：

| 代理组名称 | 作用说明 | 你的操作建议 |
| :--- | :--- | :--- |
| **Proxy** | **核心节点池**。这是你机场所有节点的集合。 | **主要在这里选节点**。在这里选中的节点会直接影响 Google 和 Final。 |
| **Google** | **专项规则组**。配置文件设定了 `google.com` 的流量走这里。 | 默认指向 `Proxy`。如果你想看 YouTube 用香港，查资料用日本，可以在这里单独分流。 |
| **Final** | **漏网之鱼组**。所有不在规则内（如 Twitter、Telegram 等）的流量走这里。 | 默认指向 `Proxy`。通常保持和 `Proxy` 一致即可。 |
| **GLOBAL** | **全局模式组**。仅当你把左上角的“模式”从 `Rule` 切换为 `Global` 时生效。 | 小白通常不用管，保持 `Rule` (规则) 模式最省心，国内直连国外代理。 |

---

## 三、 镜像更新方法
Mihomo 内核更新很快，建议每个月运行一次以下命令来保持最新版：

```bash
cd ~/mihomo
# 1. 拉取最新镜像
docker compose pull
# 2. 重新启动（会自动替换旧版本，配置不丢失）
docker compose up -d
```

---

## 四、 完全卸载方法
如果你不想用了，想彻底清理 VPS 空间，请按顺序执行：

1.  **停止并删除容器：**
    ```bash
    cd ~/mihomo
    docker compose down
    ```
2.  **删除残留镜像：**
    ```bash
    docker rmi metacubex/mihomo:latest ghcr.io/metacubex/metacubexd
    ```
3.  **删除配置文件目录：**
    ```bash
    cd ~
    rm -rf ~/mihomo
    ```
    *执行完这三步，你的 VPS 就像从没装过 Mihomo 一样干净。*

---

## 五、 日常小技巧
* **查看运行状态：** `docker ps`（看到 `Up` 才是正常）。
* **查看实时报错：** `docker logs -f mihomo`（按 `Ctrl+C` 退出查看）。
* **面板连不上：** 优先检查 VPS 供应商后台的防火墙是否关闭了 `8888` 和 `9090`。

---
**恭喜你！现在你已经完全掌握了 VPS 代理的控制权。**