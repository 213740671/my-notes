# AIStudioToAPI 维护笔记（小白版，路径：/root/aistudio-to-api）

> 适用前提：你是用 Docker Compose 在 VPS 上部署的，并且项目目录就是：
> `/root/aistudio-to-api`

---

## 1) 目录结构你需要知道什么

- **项目目录**：`/root/aistudio-to-api`
- **核心配置文件**：`/root/aistudio-to-api/docker-compose.yml`
- **账号认证文件目录（非常重要）**：`/root/aistudio-to-api/auth/`
  - 里面会有 `auth-0.json`、`auth-1.json`…（你添加账号后自动生成）
  - 这是你登录状态的“凭据”，**建议定期备份**

---

## 2) 常用命令速查（最常用的就这些）

> 先进入目录（建议每次操作前都先 cd）
```bash
cd /root/aistudio-to-api
```

### 2.1 启动服务（后台运行）
```bash
docker compose up -d
```

### 2.2 停止服务（但不删除容器）
```bash
docker compose stop
```

### 2.3 再次启动（针对 stop 之后）
```bash
docker compose start
```

### 2.4 重启服务（最常用）
```bash
docker compose restart
```

### 2.5 查看运行状态
```bash
docker compose ps
```

### 2.6 看日志（排错必用）
- 持续跟踪日志：
```bash
docker compose logs -f
```
- 只看最近 200 行：
```bash
docker compose logs --tail=200
```

---

## 3) 更新（升级到最新版本）怎么做

> 更新就是：**拉新镜像 → 重新创建容器**

```bash
cd /root/aistudio-to-api
docker compose pull
docker compose up -d
docker compose logs --tail=200
```

**如果更新后行为异常：**
- 先看日志：`docker compose logs -f`
- 尝试重启：`docker compose restart`

---

## 4) 卸载（彻底移除）怎么做

> ⚠️ 注意：`down` 会删除容器与网络，但不会删除你本地的 `auth/` 目录（除非你手动删）

### 4.1 删除服务容器（推荐卸载方式）
```bash
cd /root/aistudio-to-api
docker compose down
```

### 4.2 如果你连 auth 凭据也要一起删（危险操作）
> 会导致你下次需要重新登录账号
```bash
rm -rf /root/aistudio-to-api/auth
```

### 4.3 如果你要把整个目录都删掉
```bash
rm -rf /root/aistudio-to-api
```

---

## 5) 修改配置（比如 API_KEYS、代理、时区、端口）怎么做

### 5.1 修改 docker-compose.yml
```bash
cd /root/aistudio-to-api
nano docker-compose.yml
```

常见你可能会改的地方：

- **API_KEYS（强烈建议长随机字符串）**
- **TZ（时区）**
- **HTTP_PROXY / HTTPS_PROXY（只有 VPS 访问 Google 不通才需要）**
- **端口映射**
  - 例如你想把外部端口从 7860 改成 17860：
  - 把 `7860:7860` 改为 `17860:7860`

### 5.2 修改配置后让它生效（重要！）
> 改完配置文件，一般用 up -d 重新创建容器即可
```bash
cd /root/aistudio-to-api
docker compose up -d
```

---

## 6) 备份与迁移（换 VPS / 防翻车）

### 6.1 备份最关键的东西（auth 凭据 + compose 配置）
```bash
cd /root
tar -czvf aistudio-to-api-backup.tar.gz \
  /root/aistudio-to-api/docker-compose.yml \
  /root/aistudio-to-api/auth
```

然后把 `aistudio-to-api-backup.tar.gz` 下载到你本地保存即可。

### 6.2 迁移到新 VPS（简要流程）
1. 新 VPS 安装 Docker + Compose
2. 把备份包传上去
3. 解压到同样路径
4. `cd /root/aistudio-to-api && docker compose up -d`

---

## 7) 开机自动启动（一般你已经满足）

只要满足两点，重启 VPS 后服务通常会自动起来：
1. docker 服务开机自启
```bash
systemctl enable --now docker
```
2. compose 里设置了 `restart: unless-stopped`（多数示例默认有）

---

## 8) 常见问题排查（按这个顺序来）

### 8.1 端口打不开
- 先看容器是否在跑：
```bash
cd /root/aistudio-to-api
docker compose ps
```
- 再看日志：
```bash
docker compose logs --tail=200
```
- VPS 防火墙/安全组是否放行 7860（或你改过的端口）

### 8.2 更新后不正常
- 回看日志：
```bash
docker compose logs -f
```
- 重启：
```bash
docker compose restart
```
- 不行就 down 再 up（不会丢 auth，只要你没删 auth 目录）：
```bash
docker compose down
docker compose up -d
```

### 8.3 账号掉了/不能用
- 先确认 `auth/` 目录下还有 `auth-*.json`
```bash
ls -lah /root/aistudio-to-api/auth
```
- 如果文件没了，就需要重新进 Web 控制台添加账号

---

## 9) 安全提醒（不用 Nginx 时尤其重要）

- **不要使用弱 API_KEYS**（例如 123456 这种）
- 尽量在安全组/防火墙里限制访问来源（只允许你自己的公网 IP 访问 7860）
- `auth/` 目录相当于登录凭据，**别随便分享**

---

## 10) 最推荐的“日常操作模板”（你只要记住这段）

- 更新：
```bash
cd /root/aistudio-to-api && docker compose pull && docker compose up -d
```

- 看日志：
```bash
cd /root/aistudio-to-api && docker compose logs -f
```

- 重启：
```bash
cd /root/aistudio-to-api && docker compose restart
```

- 停止：
```bash
cd /root/aistudio-to-api && docker compose stop
```

- 卸载：
```bash
cd /root/aistudio-to-api && docker compose down
```
