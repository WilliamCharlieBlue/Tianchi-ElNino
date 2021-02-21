# 1 构建镜像提交到天池

#### 根据datawhale提供的baseline结果，构建镜像提交到天池

### 1.1 baseline结果展示

```shell
mlp_predict.py
requirements.txt
run.sh
Dockerfile
```

### 1.2 具体文件展示

```shell
#File：requirements.txt
numpy
tensorflow==2.2.0
```

```shell
#File：run.sh
python3 mlp_predict.py
```

```dockerfile
#File：Dockerfile
# Base Images
## 从天池基础镜像构建
# FROM registry.cn-shanghai.aliyuncs.com/tcc-public/python:3
FROM registry.cn-shanghai.aliyuncs.com/tcc-public/tensorflow:latest-cuda10.0-py3

## 把当前文件夹里的文件构建到镜像的根目录下（.后面有空格，不能直接跟/）
ADD . /

## 指定默认工作目录为根目录（需要把run.sh和生成的结果文件都放在该文件夹下，提交后才能运行）
WORKDIR /

## Install Requirements（requirements.txt包含python包的版本）
## 这里使用清华镜像加速安装
RUN pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip install --no-cache-dir -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

## 镜像启动后统一执行 sh run.sh
CMD ["sh", "run.sh"]
```

### 1.3 构建镜像

```shell
# 构建镜像
docker build -t baseline:v1.0.0 .
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225214.png)

```shell
# 查看一下所有镜像里有没有刚建好的镜像
docker images
# 镜像建失败时也有一个<None>的记录，可以通过docker rmi -f 命令删除
docker rmi -f 6e7679a03xxx
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225249.png)

### 1.4 查看镜像

```shell
# 可以开启一个容器查看镜像
# exit 或 Ctrl+D退出
docker run -it baseline:v1.0.0 /bin/bash
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225338.png)

### 1.5 tag和push 镜像

```shell
# 把建好的镜像tag一下，这里可以使用镜像ID 标记 为阿里云镜像服务
# 要先tag才能push
docker tag 6e7679a0365c registry.cn-shanghai.aliyuncs.com/williamcharlieblue/elnino:baseline
# push到阿里云镜像服务
docker push registry.cn-shanghai.aliyuncs.com/williamcharlieblue/elnino:baseline
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225406.png)

### 1.6 提交镜像结果，并查看成绩

```shell
# 进入比赛主页，把阿里云镜像提交
# 配置路径，如果是私有镜像库，记得每次都需要输入以下密码(多次配置时，密码并不会自己记录)
https://tianchi.aliyun.com/competition/entrance/531871/information
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225439.png)

```shell
# 配置完成并且提交后，会
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225456.png)

```shell
# 提交完成后，可以在“我的成绩板块进行查看成绩”，以及历史提交记录
```

![img](https://raw.githubusercontent.com/williamcharlieblue/img/main/img/20210221225506.png)