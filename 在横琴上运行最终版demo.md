# 在横琴上运行最终版demo

通过容器应用运行一个单机并行版，基于“最终版”代码。
首先基于“最终版”代码，生成镜像，名字为命名为”sustech-ligy/master-evals:v2“

点击横琴上的“容器服务”--“容器应用”--“添加应用”
选择规格“sustech-ligy-30c30g”

添加第一个容器，选择镜像”sustech-ligy/master-evals:v2“，命名为master，cpu（5，10），内存（5，10），硬盘30gb。
添加端口10080和10081，设置启动参数
```bash
java -jar /usr/local/all/master-router-1.3.6-SNAPSHOT.jar --server.port=10080 --master.ip=localhoat --master.port=10081
```

添加第二个容器，选择镜像”sustech-ligy/master-evals:v2“，命名为eval1，cpu（5，10），内存（5，10），硬盘30gb。
添加端口10083，设置启动参数
```bash
python /usr/local/all/evaluatorWintimeFile/server_client.py --masterhost localhost --masterport 10081 --host localhoat --port 10083
```

添加第三个容器，选择镜像”sustech-ligy/master-evals:v2“，命名为eval2，cpu（5，10），内存（5，10），硬盘40gb。
添加端口10084，设置启动参数
```bash
python /usr/local/all/evaluatorWintimeFile/server_client.py --masterhost localhost --masterport 10081 --host localhost --port 10084
```

选择下一步，服务选择映射容器端口，创建应用服务。
应用创建成功后，查看容器端口10080对应的外网访问端口，通过
```
外网ip:外网端口/result
```
进入demo展示页面。

demo运行流程：选择数据--”最终版“下mc_demo/data/accident.txt,选择并行度2（不能超过eval容器数目），然后运行。
过一段时间后，应该可以通过监控查看到三个容器又内存和网络的明显增长。

本示例目前运行在横琴平台，可通过“容器服务“--”容器应用“--”lgy-mc-whole“查看。
目前的访问地址是“http://120.236.247.203:30339/result”