# 2 修改模型以及重新提交

### 2.1 要先测试后再进行推送

```shell
# 构建镜像完成后，一定一定一定要进行运行后再进行tag和push
# 根据报错先进行修改，对于
docker run 6e7679a0365c /bin/bash run.sh
```

### 2.2 对于缺数据和找不到文件夹的情况，可以通过映射文件夹的形式来准备一些数据

```shell
# 此类报错实例
# No such file or directory: './tcdata/enso_round1_test_20210201/'
# 例如 -v 是通过本地的路径映射到镜像当中
docker run -v /tmp:/tcdata 6e7679a0365c /bin/bash run.sh
```

### 2.3 分数没能再进一步

由于基础实在是比较差，不仅没能提分，连负分都拿不到[一脸心酸]，坐等大佬们的分享

![image-20210225231950187](https://github.com/williamcharlieblue/img/main/img/image-20210225231950187.png)

### 2.4 在B战上找到了Datawhale的一个比较友好的系列视频

```shell
# 默默地从零开始的天池世界
https://www.bilibili.com/video/av242637682/
```



