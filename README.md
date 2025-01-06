# 部署 clickhouse
## 拉取编排文件
git clone git@github.com:shelchin2023/clickhouse-deploy.git

## 创建环境变量 
```
cd clickhouse-deploy
touch .env
export CLICKHOUSE_PASSWORD=$(openssl rand -hex 16)
echo "CLICKHOUSE_PASSWORD=$CLICKHOUSE_PASSWORD" >> .env
```

## 创建 compose override 文件
```
cat > override.yml << EOF
services:
  events_db:
    environment:
      - CLICKHOUSE_PASSWORD
    ports:
      - 127.0.0.1:19000:9000
EOF
```

## 运行服务
docker compose -f compose.yml -f override.yml up -d 