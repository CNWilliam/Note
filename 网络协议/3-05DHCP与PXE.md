# DHCP与PXE：IP是怎么来的，又是怎么没的？



## 如何配置IP地址？

### 使用net-tools:

```
$ sudo ifconfig eth1 10.0.0.1/24
$ sudo ifconfig eth1 up

```

### 使用iproute2:

```
$ sudo ip addr add 10.0.0.1/24 dev eth1
$ sudo ip link set up eth1

```



**Linux默认的逻辑是，如果这是一个跨网段的调用，它便不会直接将包发送到网络，而是企图将包发送到网关**

**不同系统的配置文件格式不同，但是无非就是CIDR、子网掩码、广播地址和网关地址**

## 动态主机配置协议(DHCP)

**如果是数据中心里面的服务器，IP一旦配置好，基本不会变，这就相当于买房自己装修。DHCP的方式就相当于租房。你不用装修，都是帮你配置好的。你在暂用一下，用完退租就可以了

## 解析DHCO的工作方式



![](https://static001.geekbang.org/resource/image/39/1f/395b304f49559034af34c882bd86f11f.jpg)





1.正确配置IP?

CIDR、子网掩码、广播地址和网关地址。

2.在跨网段调用中，是如何获取目标IP的mac地址的？

从源IP网关获取所在网关mac,
然后又替换为目标IP所在网段网关的mac,
最后是目标IP的mac地址

3.手动配置麻烦，怎么办？

DHCP！Dynamic Host Configuration Protocol！
DHCP, 让你配置IP，如同自动房产中介。

4.如果新来的，房子是空的(没有操作系统)，怎么办？

PXE， Pre-boot Execution Environment.
"装修队"PXE，帮你安装操作系统。

