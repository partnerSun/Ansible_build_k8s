# ansible部署二进制K8S集群



### 运行

* 在ansible控制主机上运行即可，保证控制主机与集群节点是可通信的

```shell
ansible-playbook playbook.yml -i hosts
```

### 注意
* service, pod的ip在k8s/vars/main.yml中配置
* etcd当前配置部署在3个master节点上，若需单独部署，需要修改etcd安装、配置和证书的部分
* hosts文件配置要部署的资产节点和登录信息
* 通过修改k8s/vars/main.yml变量文件

