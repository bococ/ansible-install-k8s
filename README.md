# Kubernetes v1.16 高可用集群自动部署（离线版）
>### 确保所有节点系统时间一致
## 1、下载二进制包，并解压到工作目录
云盘地址：https://pan.baidu.com/s/1xhBfUm3vDKgDrUpFbcCgWQ
```
cd ansible-install-k8s
tar zxf binary_pkg.tar.gz
```
## 2、修改hosts文件
根据规划修改对应IP和名称。
```
vi hosts
```
## 3、修改group_vars/all.yml文件

添加证书可信任IP：
```
cert_hosts:
  k8s:
  etcd:
```
## 4、一键部署
### 架构图
单Master架构
![avatar](https://github.com/lizhenliang/ansible-install-k8s/blob/master/single-master.jpg)
多Master架构
![avatar](https://github.com/lizhenliang/ansible-install-k8s/blob/master/multi-master.jpg)
### 部署命令
单Master版：
```
ansible-playbook -i hosts single-master-deploy.yml -uroot -k
```
多Master版：
```
ansible-playbook -i hosts multi-master-deploy.yml -uroot -k
```

## 5、角色控制
如果安装某个阶段失败，可针对性测试.

例如：只运行部署插件
```
ansible-playbook -i hosts single-master-deploy.yml -uroot -k --tags addons
```
