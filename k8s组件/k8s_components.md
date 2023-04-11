# k8s 架构

  

![image.png](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/6ba9cac452f74bb483e7aaea63735125~tplv-em5hxbkur4-noop.image)

我们看下 k8s 集群的架构，从左到右，分为两部分，第一部分是 Master 节点（也就是图中的 Control Plane），第二部分是 Node 节点。

*   Master 节点一般包括四个组件，apiserver、scheduler、controller-manager、etcd，他们分别的作用是什么：
    
    *   Apiserver：上知天文下知地理，上连其余组件，下接ETCD，提供各类 api 处理、鉴权，和 Node 上的 kubelet 通信等，只有 apiserver 会连接 ETCD。
        
    *   Controller-manager：控制各类 controller，通过控制器模式，致力于 **将当前状态转变为期望的状态** 。
        
    *   Scheduler： **调度，打分，分配资源** 。
        
    *   Etcd：整个集群的数据库，也可以不部署在 Master 节点，单独搭建。
        
*   Node 节点一般也包括三个组件，docker，kube-proxy，kubelet
    
    *   Docker：具体跑应用的载体。
        
    *   Kube-proxy：主要负责网络的打通，早期利用 iptables，现在使用 ipvs技术。
        
    *   Kubelet：agent，负责管理容器的生命周期。
        
    *   Container runtime ：容器启动/容器运行时
        
    
    ![image.png](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c6875aa3ca7d423ab36bc034c95a24bc~tplv-em5hxbkur4-noop.image)
    

总结一下就是 k8s 集群是一个由两部分组件 Master 和 Node 节点组成的架构，其中 Master 节点是整个集群的大脑，Node 节点来运行 Master 节点调度的应用，我们后续会以一个具体的调度例子来解释这些组件的交互过程。
