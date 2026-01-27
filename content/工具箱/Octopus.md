# 🐙 Octopus 更新指南 (Docker Compose)

> 适用于使用 Docker Compose 部署的 Octopus 服务。

## ⚠️ 重要注意事项：数据安全
Octopus 会将统计数据（Token消耗、费用等）缓存在内存中。
**更新过程中，Docker 会自动发送停止信号。请耐心等待容器停止，不要强制杀死进程（不要手动执行 `kill -9`），以确保内存数据能写入数据库。**

---

## 🚀 更新步骤

### 1. 进入项目目录
进入你存放 `docker-compose.yml` 的文件夹（例如 `octopus`）：
```bash
cd octopus
```

### 2. 拉取最新镜像
从 Docker Hub 下载最新的 `bestrui/octopus` 镜像：
```bash
docker compose pull
```

### 3. 重启服务
此命令会自动停止旧容器（触发数据保存）并启动新版本容器：
```bash
docker compose up -d
```

### 4. 清理旧镜像（可选）
删除更新后留下的无用旧镜像，释放 VPS 空间：
```bash
docker image prune -f
```

---

## 📝 进阶：如果官方更新了配置文件
如果官方的 `docker-compose.yml` 结构发生了重大变化（例如新增了必要的环境变量），建议更新配置文件：

1. **备份当前配置**：
   ```bash
   cp docker-compose.yml docker-compose.yml.bak
   ```
2. **下载最新配置**：
   ```bash
   wget -O docker-compose.yml [https://raw.githubusercontent.com/bestruirui/octopus/refs/heads/dev/docker-compose.yml](https://raw.githubusercontent.com/bestruirui/octopus/refs/heads/dev/docker-compose.yml)
   ```
3. **重新应用**：
   ```bash
   docker compose up -d
   ```

## ✅ 验证更新
更新完成后，访问管理面板（默认 `http://ip:8080`），在页面底部或日志中确认服务运行正常。