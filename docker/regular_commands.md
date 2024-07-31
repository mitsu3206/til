# Docker
Dockerでよく使うコマンドを記載する。

#### docker-compose.ymlからコンテナを起動する
```
docker compose up -d
```

#### 滅びの呪文
コンテナ、イメージ、ボリューム、ネットワーク、全てを一括削除する。
```
docker compose down --rmi all --volumes --remove-orphans
```

#### コンテナを一覧表示する
```
docker ps -a
```

#### イメージを一覧表示する
```
docker images
```

#### 未使用イメージを一括削除する
```
docker rmi `docker images -q`
```

#### 不要なリソースを削除する
```
docker system prune
```

#### コンテナに入る
```
docker exec -it <container_name> /bin/bash
```

#### コンテナ内でコマンドを実行する
```
docker exec <container_name> <command>
```
