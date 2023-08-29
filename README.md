# ansible部署二进制K8S集群



## 运行

* 在ansible控制主机上运行即可，保证控制主机与集群节点是可通信的

```shell
ansible-playbook playbook.yml -i hosts
```

## 注意

* service, pod的ip在k8s/vars/main.yml中配置
* etcd当前配置部署在3个master节点上，若需单独部署，需要修改etcd安装、配置和证书的部分
* hosts文件配置要部署的资产节点和登录信息
* 通过修改k8s/vars/main.yml变量文件,包括主机名与ip映射等，这个文件中的变量部署之前最好都看一遍

## 目录结构

* playbook.yml是部署的总入口，选择部署资产和部署role.
* roles(eg: k8s)是某个项目的部署信息，有以下目录:
  
```shell
.
├── defaults #存放默认变量，可被vars或者传参覆盖，优先级最低.
├── files #固定文件，一般存放安装包或者固定不变的配置.
├── handlers  #触发任务，通过notify模块调用
├── meta #角色依赖
├── tasks #主要任务，部署的详细信息通过task描述
├── templates #存放以.j2结尾的可变配置文件，可引用变量，可使用for、if循环，使用template模块引用
├── tests 
└── vars #定义该role的变量
```

* 每个目录下都有一个main.yml文件作为该目录的入口文件(files目录除外)，可以添加其他的文件并通过include在main.yml中引用

