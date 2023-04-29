# docker

通过docker批量或单独开设NAT服务器(Bulk or individual NAT server provisioning via docker)

默认使用debian系统，每个容器自带1个外网ssh端口，25个内外网一致端口

## 配置要求

系统可安装docker即可用，网络能连接Github的raw界面就能用，硬件配置只要不拉跨就行，空闲硬盘有3G就行

## 环境预设

- 检测环境
- 安装docker
- 下载预制脚本

```
curl -L https://raw.githubusercontent.com/spiritLHLS/docker/main/scripts/pre_build.sh -o pre_build.sh && chmod +x pre_build.sh && bash pre_build.sh
```

## 单独开设

下载脚本

```
curl -L https://raw.githubusercontent.com/spiritLHLS/docker/main/scripts/onedocker.sh -o onedocker.sh && chmod +x onedocker.sh
```

本地文件系统支持xfs才可使用disk限制，否则将开启失败

查询

```
lsmod | grep -q xfs
```

执行上述命令有输出才可限制disk，否则勿要填写disk

不支持xfs的系统开设的容器将共享母鸡的硬盘

```
./onedocker.sh name cpu memory sshport startport endport <disk>
```

### 示例

将开设1核512MB内存10G硬盘，SSH端口映射至外网2022，批量映射的端口区间为2023到2033，此区间内外网端口一致

```
./onedocker.sh test 1 512 2022 2023 2033 10
```

删除示例

```
docker rm -f test
```

进入示例

```
docker exec -it test /bin/bash
```

### 查询信息

```
cat 容器名字
```

## 批量开设

- 批量多次运行继承配置生成

```
curl -L https://raw.githubusercontent.com/spiritLHLS/docker/main/scripts/dockers.sh -o dockers.sh && chmod +x dockers.sh && bash dockers.sh
```
