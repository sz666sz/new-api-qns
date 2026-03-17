# RUNBOOK

服务器 IP：`212.103.62.134`

## 发布新版本

```bash
# 本地：提交代码后删旧 tag、重打、推送触发构建
git tag -d v1.0.0
git push origin :refs/tags/v1.0.0
git tag v1.0.0
git push origin main
git push origin v1.0.0
```

构建进度：https://github.com/dev-longshun/new-api-qns/actions

## 服务器：更新镜像

```bash
cd ~/new-api
docker compose pull
docker compose up -d
```

## 服务器：常用运维

```bash
# 查看日志
docker compose logs -f new-api

# 重启
docker compose restart new-api

# 停止 / 启动
docker compose down
docker compose up -d

# 查看容器状态
docker ps -a

# 验证服务
curl http://localhost:3000/api/status
```

## 域名

- `https://www.qnsapi.com` → new-api
- `https://kiro.qnsapi.com` → kiro-rs 管理后台

## kiro-rs 运维

```bash
cd ~/kiro-rs

# 查看日志
docker compose logs -f

# 重启
docker compose restart

# 更新镜像
docker compose pull && docker compose up -d
```

## SSH 隧道（本地访问 kiro-rs 管理后台）

```bash
ssh -L 8990:127.0.0.1:8990 root@212.103.62.134
# 然后浏览器打开 http://localhost:8990/admin
```
