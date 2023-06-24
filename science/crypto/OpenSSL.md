# 简介

OpenSSL是一款开源的软件库，提供了一系列用于加密、解密和安全通信的应用程序接口（API）和命令行工具。除了加解密算法与哈希函数，它还实现了SSL协议和TLS协议，提供了安全套接字层（SSL）和传输层安全（TLS）协议的支持。OpenSSL还提供了用于生成和管理数字证书的工具。

OpenSSL采用C语言作为开发语言，这使得它具有优秀的跨平台性能。它可以在多种平台上运行，包括Windows，Linux，Unix和Mac OS X等操作系统。

OpenSSL广泛应用于安全通信和加密领域，如网站加密，数字证书管理，虚拟私人网络和身份验证。许多Web服务器，包括Apache和Nginx，都使用OpenSSL来提供SSL / TLS加密的支持。OpenSSL也是许多其他安全软件的基础，例如OpenSSH和OpenVPN。

由于其广泛的应用和重要性，OpenSSL已成为重要的开源安全软件库之一。

# 官方文档资料查找

官网：https://www.openssl.org/

导航栏Docs》manual pages》显示OpenSSL的不同版本，选择相应版本》

- Commands:对于openssl的命令行命令
- Libraries：对于openssl的C库接口说明
- File Formats：主要是和openssl相关的配置文件
- Overviews: openssl概述，按照模块介绍openssl



中文手册：https://www.openssl.net.cn/

> 参考资料：
>
> 1. openssl官网文档资料 https://blog.csdn.net/MashiMaroJ/article/details/126186077

# 安装

## linux下安装

查看操作系统上是否已有OpenSSL：

```bash
$ rpm -ql openssl
```





查看openssl所在路径：

```bash
$ whereis openssl
```

```bash
openssl: /usr/bin/openssl /usr/include/openssl /home/r1206/anaconda3/bin/openssl /usr/share/man/man1/openssl.1ssl.gz
```

- /usr/bin/openssl：应用程序
- /usr/include/openssl：静态链接库，存的是开发用的头文件
- 