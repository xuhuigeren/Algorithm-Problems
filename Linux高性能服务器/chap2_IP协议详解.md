# 第二章 IP协议详解

IP协议是TCP/IP协议簇的核心协议, 是socket网络编程的基础之一
IP协议为上层协议提供无状态, 无连接, 不可靠的服务

IP数据报最大长度是65535(2^16 - 1)字节, 但是有MTU的限制

当IP数据报的长度超过MTU 将会被分片传输. 分片可能发生在发送端, 也可能发生在中转路由器, 还可能被多次分片. 只有在最终的目标机器上, 这些分片才会被内核中的ip模块重新组装

![](https://lsmg-img.oss-cn-beijing.aliyuncs.com/Linux%E9%AB%98%E6%80%A7%E8%83%BD%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BC%96%E7%A8%8B%E8%AF%BB%E4%B9%A6%E8%AE%B0%E5%BD%95/%E6%90%BA%E5%B8%A6ICMP%E6%8A%A5%E6%96%87%E7%9A%84IP%E6%95%B0%E6%8D%AE%E6%8A%A5%E8%A2%AB%E5%88%86%E7%89%87.png)

路由机制

![](https://lsmg-img.oss-cn-beijing.aliyuncs.com/Linux%E9%AB%98%E6%80%A7%E8%83%BD%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BC%96%E7%A8%8B%E8%AF%BB%E4%B9%A6%E8%AE%B0%E5%BD%95/%E8%B7%AF%E7%94%B1%E6%9C%BA%E5%88%B6.png)

给定了目标IP地址后, 将会匹配路由表中的哪一项呢? 分三个步骤

- 查找路由表中和数据报的目标IP地址完全匹配的主机IP地址. 如果找到就使用该路由项. 否则下一步
- 查找路由表中和数据报的目标IP地址具有相同网路ID的网络IP地址 找到....... 否则下一步
- 选择默认路由项, 通常意味着下一跳路由是网关