官方文档地址： https://nats.io/

# 1.安装

## 1.deb包安装

下载地址 ：https://github.com/nats-io/nats-server/releases/

我下载的是deb包，下载好之后安装。

```shell
yantao@ubuntu20:~/下载$ ls |grep nats
nats-server-v2.10.5-amd64.deb
yantao@ubuntu20:~/下载$ sudo apt install ./nats-server-v2.10.5-amd64.deb
```

启动

```shell
yantao@ubuntu20:~$ nats-server
[31472] 2023/11/20 14:07:23.677782 [INF] Starting nats-server
[31472] 2023/11/20 14:07:23.677935 [INF]   Version:  2.10.5
[31472] 2023/11/20 14:07:23.677941 [INF]   Git:      [0883d32]
[31472] 2023/11/20 14:07:23.677945 [INF]   Name:     NAE5PYNCVVWPN5SF24VLSFFGHGPEPOIWKKE37WQXUL3PXX2XWGST5U3I
[31472] 2023/11/20 14:07:23.677949 [INF]   ID:       NAE5PYNCVVWPN5SF24VLSFFGHGPEPOIWKKE37WQXUL3PXX2XWGST5U3I
[31472] 2023/11/20 14:07:23.678659 [INF] Listening for client connections on 0.0.0.0:4222
[31472] 2023/11/20 14:07:23.679045 [INF] Server is ready

```



## 2.使用go install 安装

nats是golang开发的，可以这样安装

```shell
go install github.com/nats-io/nats-server/v2@latest
```

运行

```shell
yantao@ubuntu20:~/go/bin$ ls |grep nats
nats-server
yantao@ubuntu20:~/go/bin$ ./nats-server 
[29983] 2023/11/20 13:59:34.042395 [INF] Starting nats-server
[29983] 2023/11/20 13:59:34.042543 [INF]   Version:  2.10.5
[29983] 2023/11/20 13:59:34.042548 [INF]   Git:      [not set]
[29983] 2023/11/20 13:59:34.042552 [INF]   Name:     NAUORMY4A5J4RBT36SCS723PNUQI75QTYEL6HRZ7F7PJ5RD7ZO6KGX4H
[29983] 2023/11/20 13:59:34.042556 [INF]   ID:       NAUORMY4A5J4RBT36SCS723PNUQI75QTYEL6HRZ7F7PJ5RD7ZO6KGX4H
[29983] 2023/11/20 13:59:34.043204 [INF] Listening for client connections on 0.0.0.0:4222
[29983] 2023/11/20 13:59:34.043567 [INF] Server is ready
^C[29983] 2023/11/20 13:59:36.828728 [INF] Initiating Shutdown...
[29983] 2023/11/20 13:59:36.828901 [INF] Server Exiting..

```



## 3.使用docker安装

安装

```shell
sudo docker pull nats:latest
```

运行

```shell
sudo docker run -p 4222:4222 -ti nats:latest
```



## 4.启动参数

```shell
-a, --addr, --net <host>：绑定到主机地址（默认为 0.0.0.0）。
-p, --port <port>：用于客户端的端口（默认为 4222）。
-m, --http_port <port>：用于 http 监控的端口。
-c, --config <file>：配置文件。
-l, --log <file>：重定向日志输出的文件。
-D, --debug：启用调试输出。
-V, --trace：跟踪原始协议。
-js, --jetstream：启用 JetStream 功能。
-sd, --store_dir <dir>：设置存储目录。
--user <user>：连接所需的用户。
--pass <password>：连接所需的密码。
--auth <token>：连接所需的授权令牌。
--tls：启用 TLS，不验证客户端（默认为 false）。
--tlscert <file>：服务器证书文件。
--tlskey <file>：服务器证书的私钥。
--tlsverify：启用 TLS，验证客户端证书。
--tlscacert <file>：用于验证的客户端证书 CA。
```



### 1.启动http 监控的端口

```shell
yantao@ubuntu20:~/go/bin$ ./nats-server -m 8222
[9143] 2023/11/21 10:28:35.806779 [INF] Starting nats-server
[9143] 2023/11/21 10:28:35.806938 [INF]   Version:  2.10.5
[9143] 2023/11/21 10:28:35.806943 [INF]   Git:      [not set]
[9143] 2023/11/21 10:28:35.806946 [INF]   Name:     NBNHELYXYGH53SNDLEWMZLM3QPWT7CFZRCHGTZAXARYDQHNO2ZTXO22Q
[9143] 2023/11/21 10:28:35.806950 [INF]   ID:       NBNHELYXYGH53SNDLEWMZLM3QPWT7CFZRCHGTZAXARYDQHNO2ZTXO22Q
[9143] 2023/11/21 10:28:35.807700 [INF] Starting http monitor on 0.0.0.0:8222 #网页端口
[9143] 2023/11/21 10:28:35.807787 [INF] Listening for client connections on 0.0.0.0:4222
[9143] 2023/11/21 10:28:35.808847 [INF] Server is ready

```

使用浏览器打开网址 ：http://127.0.0.1:8222/



## 2.jetstream模式

使用jetstream模式，并且开启8222座位web端口。

```shell
yantao@ubuntu20:~/go/bin$ nats-server --jetstream -m 8222
[25372] 2023/12/08 16:51:46.102297 [INF] Starting nats-server
[25372] 2023/12/08 16:51:46.102358 [INF]   Version:  2.10.5
[25372] 2023/12/08 16:51:46.102361 [INF]   Git:      [not set]
[25372] 2023/12/08 16:51:46.102363 [INF]   Name:     NATCAAOL74KC3C7DCX6S4I536GC2U5CMBZPJ3EON4BXIJBS75TN3Y4ZU
[25372] 2023/12/08 16:51:46.102365 [INF]   Node:     UmHtm25Q
[25372] 2023/12/08 16:51:46.102367 [INF]   ID:       NATCAAOL74KC3C7DCX6S4I536GC2U5CMBZPJ3EON4BXIJBS75TN3Y4ZU
[25372] 2023/12/08 16:51:46.102682 [INF] Starting http monitor on 0.0.0.0:8222
[25372] 2023/12/08 16:51:46.102712 [INF] Starting JetStream
[25372] 2023/12/08 16:51:46.102775 [INF]     _ ___ _____ ___ _____ ___ ___   _   __  __
[25372] 2023/12/08 16:51:46.102777 [INF]  _ | | __|_   _/ __|_   _| _ \ __| /_\ |  \/  |
[25372] 2023/12/08 16:51:46.102780 [INF] | || | _|  | | \__ \ | | |   / _| / _ \| |\/| |
[25372] 2023/12/08 16:51:46.102782 [INF]  \__/|___| |_| |___/ |_| |_|_\___/_/ \_\_|  |_|
[25372] 2023/12/08 16:51:46.102783 [INF] 
[25372] 2023/12/08 16:51:46.102785 [INF]          https://docs.nats.io/jetstream
[25372] 2023/12/08 16:51:46.102789 [INF] 
[25372] 2023/12/08 16:51:46.102791 [INF] ---------------- JETSTREAM ----------------
[25372] 2023/12/08 16:51:46.102793 [INF]   Max Memory:      11.55 GB
[25372] 2023/12/08 16:51:46.102795 [INF]   Max Storage:     224.09 GB
[25372] 2023/12/08 16:51:46.102796 [INF]   Store Directory: "/tmp/nats/jetstream"
[25372] 2023/12/08 16:51:46.102797 [INF] -------------------------------------------
[25372] 2023/12/08 16:51:46.103058 [INF]   Starting restore for stream '$G > KV_mxsche'
[25372] 2023/12/08 16:51:46.103486 [INF]   Restored 0 messages for stream '$G > KV_mxsche' in 0s
[25372] 2023/12/08 16:51:46.103675 [INF]   Starting restore for stream '$G > yantao_v0_1_4_mxsche_tasks'
[25372] 2023/12/08 16:51:46.103985 [INF]   Restored 0 messages for stream '$G > yantao_v0_1_4_mxsche_tasks' in 0s
[25372] 2023/12/08 16:51:46.104069 [INF]   Starting restore for stream '$G > yantao_v0_1_4_mxsche_workflows'
[25372] 2023/12/08 16:51:46.104296 [INF]   Restored 0 messages for stream '$G > yantao_v0_1_4_mxsche_workflows' in 0s
[25372] 2023/12/08 16:51:46.104401 [INF]   Recovering 1 consumers for stream - '$G > yantao_v0_1_4_mxsche_tasks'
[25372] 2023/12/08 16:51:46.104903 [INF]   Recovering 3 consumers for stream - '$G > yantao_v0_1_4_mxsche_workflows'
[25372] 2023/12/08 16:51:46.105632 [INF] Listening for client connections on 0.0.0.0:4222
[25372] 2023/12/08 16:51:46.108019 [INF] Server is ready
```

